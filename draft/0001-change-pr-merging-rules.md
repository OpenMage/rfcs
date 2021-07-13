# Change the rules of merging a PR into OpenMage core

## Summary

At the moment, for a PR to be merged, it needs to be reviewd by 2 project maintainers, but anyway no automatic merge is ever happening. Non-mainteiners can review a PR but it doesn't mean the PR will get approved.

## Motivation

OpenMage has >180 open PRs, while some of them should be closed (that's a topic for another RFC) this RFC is about speeding the process of PR apporval/merge, which feels too slow now.

## Detailed Explanation

The new process would consider a PR approved when at least 2 users review (approving) the PR, at least 1 (of the 2 approving reviews) has to be done by a maintainer.

When enough reviews are in, the merge should be automatic.

## Rationale and Alternatives



## Implementation

It's just a matter of changing some project setting
