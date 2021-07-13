# Change the rules of merging a PR into OpenMage core

## Summary

TDB

## Motivation

At the moment, for a PR to be merged, it needs to be reviewd by 2 project maintainers,  no automatic merge is ever happening. Non-mainteiners can review a PR but it doesn't mean the PR will get approved.

OpenMage has >180 open PRs, while some of them should be closed (that's a topic for another RFC) but this RFC is about speeding the process of PR apporval/merge, which feels too slow now.

A new rule for PR approvation/merging will:
- speed up development
- give contributors quicker feedback to engage them more
- allow PRs to move quicker avoiding stagnat PRs

## Detailed Explanation

- Any contributor with at least 5 merged PRs becomes part of the "reviewers group".
- If a PR has 2 positive reviews made by 2 maintainer it will be considered approved (actual situation).
- If a PR has 1 positive review made by a maintainer and at least another one made by a person part of the "reviewers group" it will be considered approved.

When enough reviews are in, the merge should be automatic.

## Rationale and Alternatives

There could be some alternatives:
- having a maintainers meeting every few weeks, to have them all check some PRs during the meeting, but I think nobody will be able to attend those meetings because of timezones and other commitments.
- allowing "normal" users to have more priviliges in approving PRs (eg: 2 users + 1 mantainer to approve a PR) but I feel that the "having 5 merged PRs" requirement is an important filter to avoid possible "noise" in the approval process by random people.

## Implementation

It should be just a matter of changing some project settings from the project's settings page.
