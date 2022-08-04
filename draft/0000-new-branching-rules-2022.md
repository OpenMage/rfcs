# 2022 update to naming and rules regarding branches in OpenMage

## Summary

Rename the active branches and change which one if the default.

## Motivation

Up to now differences between v19 and v20 were minor and the default branch was 1.9.4.x. Almost everything was committed to the 1.9.4.x and, at release time, forward ported to the 20.0 branch.
This was ok for the first years of the project but I think it should be changed now in 2022.
Pushing the OpenMage development forward we need to promote v20 more and leave v19 behind (modified only for strictly necessary things).
We also need a working version of the 20.0 branch at all times, now it could be outdated for weeks.

## Detailed Explanation

* Rename branch `20.0` to `main`.
* Rename branch `1.9.4.x` to `v19`.
* Make `main` the default branch.
* State that new PRs should be opened against `main` branch (unless absolutely necessary).
* Forbid maintainers and contributos (whoever can write to the `magento-lts` repository) from creating new branches, the only allowed branches should be `v19`, `main` and all the actively maintained branches that correspond to released version (eg: next year we free `v20` to its own branch and `main` represents `v21`) and remove all the branches that do not comply with this rule.

## Rationale and Alternatives

## Implementation

A maintainer has to modify the branches settings from the github web interface.
