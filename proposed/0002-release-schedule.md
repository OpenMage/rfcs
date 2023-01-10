# Release Schedule

## Summary

Defining the Schedule and rules for new releases

## Motivation

Its important to have a reliability for long term plans, we can offer this by following a consistent schedule with hard rules.
Different People/Users have different needs. This RFC allows to find a middleground, which satisfies all of our users, but also will show us, what our users actually need and want, providing a base for a decision which will be seen as good enough to not need a bigger change for at least a few years.
With this RFC we then also have something to reference in case of future arguments about Releases and what gets into them.

## Detailed Explanation

With this RFC we will define a basic scheme with rules by which we will do releases, have and create release branches, and also by which we decide what kind of changes get when merged into which release branch.

## Rationale and Alternatives


{{Discuss 2-3 different alternative solutions that were considered. This is required, even if it seems like a stretch. Then explain why this is the best choice out of available ones.}}

### Alternative 1

- All new PRs are based on "main" branch (resolves confusion about where to submit PRs)
- Release timing is flexible (determined by volunteer time availability/motivation) but ideally no more than 1 MAJOR release per year and roughly one MINOR release per month
  - This may require timing the merging of multiple MAJOR features or using a temporary branch to prepare a MAJOR release
- Feature releases must be either MINOR or MAJOR as determined by PRs being merged (tag PRs that should result in major release with "MAJOR")
- Only significant security patches or regression fixes can be released immediately in a PATCH release
- PATCH fixes will *only* be back-ported to MAJOR versions that are less than 2 years (730 days) old
- Old major releases get their own branch only for the purpose of back-porting PATCH fixes (v19, v20, v21, etc)

#### Example

As of now the current releases are 19.4.21 and 20.0.18. The next release containing only MINOR features would be 20.1.0, then 20.2.0
until a MAJOR feature is released so 21.0.0 and so forth. If there is then a security patch it would be released for the latest version
(e.g. 21.0.1) and only backported to 20.2.1 (via a branch called v20) and 19.4.22 (via a branch called v19) in this case
if those branches were less than two years old at the time.

#### Effects

- Relegates v19 to security-only going forward and it basically becomes EOL in 2 years.
- All new releases are at least minor versions so it is understood there is basically always a small upgrade risk. This resolves 
  the common issue where a feature is BC breaking but in a very small way - this is always acceptable.
- The "which branch?" debate is resolved because all PRs go to "main" which is also indefinitely the default checkout branch.
- Minor releases are as easy as tagging the latest "main" with a new release number. 
- Bleeding-edge users and can easily use "dev-main" via composer indefinitely.
- Active users can upgrade as new releases are announced using the major/minor numbers as guidance.
- Users wanting minimal upgrade hassle always have at least 2 years to get up to date to the latest major version for another two years or more.

### Alternative 2

We will follow the example of Ubuntu, which bases the Major Version Number on the Year.  
And also has a specific Rythmus of an LTS version every 4 Releases,
adding bigger experimantal features in the Major Release after an LTS version.

But we will go with just one Major Release each year, which results in one LTS Release every 4 years.


#### Visualization of the Ubuntu Release cycle

![ubuntu release stragey visualized](../assets/Ubuntu_release_cycle_Ubuntu.png?raw=true "ubuntu release stragey visualized")

### Alternative 3.1

Have one Minor Release each month, do Major Releases every time a BC break is part of the Release. Only one currently supported Branch.

### Alternative 3.2

Have one Minor Release every Quarter


## Implementation

- Vote on the alternatives above and choose the winner
- Designate the appropriate "default" branch in GitHub admin
- Rename and/or delete inactive branches as necessary (perhaps after some time after an announcement in case they are being actively used)
- Update all existing PRs to the appropriate branch (can be done gradually)
- Codify the strategy into the main project `README.md` file
- Announce new release strategy in a blog post

## Unresolved Questions and Bikeshedding

{{Write about any arbitrary decisions that need to be made (syntax, colors, formatting, minor UX decisions), and any questions for the proposal that have not been answered.}}

{{THIS SECTION SHOULD BE REMOVED BEFORE RATIFICATION}}
