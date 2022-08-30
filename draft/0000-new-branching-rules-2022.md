# 2022 update to naming and rules regarding branches in OpenMage

## Summary

Rename the active branches and change which one if the default.

## Motivation

### 1.
Up to now differences between v19 and v20 were minor and the default branch was 1.9.4.x. Almost everything was committed to the 1.9.4.x and, at release time, forward ported to the 20.0 branch.
This was ok for the first years of the project but I think it should be changed now in 2022.
Pushing the OpenMage development forward we need to promote v20 more and leave v19 behind (modified only for strictly necessary things).
We also need a working version of the 20.0 branch at all times, now it could be outdated for weeks.

### 2.
We're constantly working on cleaning the code on a big scale, removing redundant code, fixing docblocks, fixing phpstan alerts, reformatting files for a better readability.
We're now doing everything on v19 and forward port to v20.
When v19 will reach EOL we'll find out that some of this work is not complete on v20, which may have more or less files that were not considered in thos PRs.
So, with the current approach, our latest version is always the less polished.

## Detailed Explanation

1. Rename branch `20.0` to `main`.
2. Rename branch `1.9.4.x` to `v19`.
3. Make `main` the default branch.
4. State that new PRs should be opened against `main` branch (unless absolutely necessary).
5. Forbid maintainers and contributos (whoever can write to the `magento-lts` repository) from creating new branches, the only allowed branches should be `v19`, `main` and all the actively maintained branches that correspond to released version (eg: next year we free `v20` to its own branch and `main` represents `v21`) and remove all the branches that do not comply with this rule.

## Rationale and Alternatives

Every software I know of has the most advanced version as the main developing branch, OpenMage is the only one I know that's works the other way around.

About point #5 of the "Detailed Explanation" section, having an uncontrolled amount of branches creates in [OpenMage's packagist page](https://packagist.org/packages/openmage/magento-lts) and this should be avoided as it doesn't contribute to create the sense of professionalism that we want OpenMage to have.

## Implementation

A maintainer has to modify the branches settings from the github web interface.
