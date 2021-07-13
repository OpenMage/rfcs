# Change the rules of merging a PR into OpenMage core

## Summary

At the moment, for a PR to be merged, it needs to be reviewd by 2 project maintainers, but anyway no automatic merge is ever happening. Non-mainteiners can review a PR but it doesn't mean the PR will get approved.

## Motivation

OpenMage has >180 open PRs, while some of them should be closed (that's a topic for another RFC) this RFC is about speeding the process of PR apporval/merge, which feels too slow now.

## Detailed Explanation

The new process would consider a PR approved when at least 2 users review (approving) the PR, at least 1 (of the 2 approving reviews) has to be done by a maintainer.

When enough reviews are in, the merge should be automatic.

## Rationale and Alternatives

There could be some alternatives:
- having a maintainers meeting every few weeks, to have them all check some PRs during the meeting, but I think nobody will be able to attend those meetings because of timezones and other commitments.
- having 1 maintainer and 2 users reviewing a PR instead of 1 maintainer and 1 user.

## Implementation

It should be just a matter of changing some project settings from the project's settings page.
