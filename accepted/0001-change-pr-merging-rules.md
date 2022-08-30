# Change the rules of merging a PR into OpenMage core

## Summary

Speed up the process of accepting and merging PRs.

## Motivation

At the moment, for a PR to be merged, it needs to be reviewed by 2 project maintainers, no automatic merge is ever happening. Non-maintainers can review a PR but it doesn't mean the PR will get approved.

OpenMage has more than 190 open PRs. Some of them should be closed without merging (that's a topic for another RFC) but this RFC is about speeding the process of  approval/merge, which feels too slow now.

A new rule for PR approval/merging will:
- speed up development
- give contributors quicker feedback to engage them more
- allow PRs to move quicker avoiding stagnant PRs
- hopefully make OpenMage better and more alive

## Detailed Explanation

A PR should be considered "approved" when:
- has 2 positive reviews by 2 maintainers (2 green checks)
- has 1 positive review by a maintainer and at 2 by normal users (1 green check + 2 gray checks)
- has 4 positive reviews by normal users (4 gray checks)

## Rationale and Alternatives

There could be some alternatives:
- having a maintainers meeting every few weeks, to have them all check some PRs during the meeting, but I think nobody will be able to attend those meetings because of timezones and other commitments.
- creating a group of users that had some PRs already merged and give them maintainer-like privileges regarding PR-review but it's probably not even possible with the github features.

## Implementation

I created a scripts that processes all PRs and all reviews and marks the PRs that meet the new requirements, so that it would be really easy for maintainers to identify the PRs that should be merged and merge them.

This is the script:

```php
<?php

$username = 'GITHUB_USERNAME';
$access_token = 'GITHUB_ACCESS_TOKEN';
$maintainers = ['colinmollenhour', 'Flyingmana', 'sreichel']; // this list needs to be updated manually

function get_json_from_url($url, $username, $access_token)
{
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_USERAGENT, $username);
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER,1);
  curl_setopt($ch, CURLOPT_USERPWD, "$username:$access_token");
  $return = curl_exec($ch);
  curl_close($ch);
  return json_decode($return);
}

$pull_requests = array_merge(
  get_json_from_url("https://api.github.com/repos/OpenMage/magento-lts/pulls?state=open&per_page=100&page=1", $username, $access_token),
  get_json_from_url("https://api.github.com/repos/OpenMage/magento-lts/pulls?state=open&per_page=100&page=2", $username, $access_token)
);
foreach ($pull_requests as $pull_request) {
  $pr_url = $pull_request->_links->self->href;
  $reviews = get_json_from_url("{$pr_url}/reviews", $username, $access_token);
  $maintainers_reviews = $users_reviews = 0;
  $checks = $reviews_usernames = [];

  foreach ($reviews as $review) {
    $review_username = $review->user->login;
    if ($review->state == 'APPROVED') {
      $reviews_usernames[$review_username] = true;
    } else {
      unset($reviews_usernames[$review_username]);
    }
  }
  foreach ($reviews_usernames as $review_username=>$status) {
    if (in_array($review_username, $maintainers)) {
      $maintainers_reviews++;
      $checks[] = 'M';
    } else {
      $users_reviews++;
      $checks[] = 'U';
    }
  }
  asort($checks);
  $pull_request->openmage_checks = implode(' ', $checks);
  $pull_request->openmage_is_ready = (($maintainers_reviews > 1) or ($maintainers_reviews > 0 and $users_reviews > 1)  or ($users_reviews > 3)) ? "READY" : "";
}

?>
<html>
<style>
  tr:hover {background: #eee}
</style>
<h1>OM PRs status</h1>
<table border=1 cellspacing=0>
  <tr>
    <th>PR</th>
    <th>Reviews</th>
    <th>Status</th>
  </tr>
  <?php
    foreach ($pull_requests as $pull_request) {
      echo "<tr><td><a href='{$pull_request->html_url}' target=_blank>{$pull_request->title}</a></td><td>{$pull_request->openmage_checks}</td><td>{$pull_request->openmage_is_ready}</td></tr>\n";
    }
  ?>
</table>
</html>
```

and this is the output:  
<img width="951" alt="Schermata 2021-12-20 alle 15 01 47" src="https://user-images.githubusercontent.com/909743/146787868-4d859c83-dd6c-4bf4-ad5c-283d2434b47b.png">

Once hosted on a server, this page could also help users identify which PRs need a review to get approved and maybe make more people review code (which is needed anyway because most of the PRs wouldn't meed the new "merge ready" criteria anyway).

I've temporary hosted the script on my server and it's available at this address: https://fabrizioballiano.com/om/pr_status.html (note:data should be updated every 6 hours).

## Notes

Accepted via voting on https://github.com/OpenMage/rfcs/issues/5


| **Name**         | **Yes** | **No** | **Comment**                                               |
|------------------|:-------:|:------:|-----------------------------------------------------------|
| kiatng           | ✔️      |        |                                                           |
| ADDISON74        | ✔️      |        |                                                           |
| Flyingmana       | ✔️      |        |                                                           |
| f1-outsourcing   | ✔️      |        |                                                           |
| elidrissidev     | ✔️      |        |                                                           |
| luigifab         | ✔️      |        |                                                           |
| tmotyl           | ✔️      |        | As long as the maintainer who merges stuff is responsible |
| simbus82         | ✔️      |        |                                                           |
| collinmollenhour | ✔️      |        | as long as the merge is happening by a maintainer         |

