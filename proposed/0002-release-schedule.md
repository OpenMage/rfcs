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

### Alternative 1.1

We will follow the Example of nginx.
We will have two parallel Versions/Branches, *stable* and *mainline*, with new Major Releases every year.
mainline will contain all the latest changes and additions, while stable is each year branched from mainline, and then only gets bugfix releases.


#### Visualization of the nginx Release cycle

![nginx release stragey visualized](../assets/nginx-release-strategy.png?raw=true "nginx release stragey visualized")

### Alternative 1.2

An additional *legazy* release branch, which provides support for the previous stable branch for ~1 more year.


### Alternative 1.3

same as previous ones, but with a different timeframe instead of a year. (not clearly defined yet)

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

{{Give a high-level overview of implementation requirements and concerns. Be specific about areas of code that need to change, and what their potential effects are. Discuss which repositories and sub-components will be affected, and what its overall code effect might be.}}

{{THIS SECTION IS REQUIRED FOR RATIFICATION -- you can skip it if you don't know the technical details when first submitting the proposal, but it must be there before it's accepted}}

## Prior Art


{{This section is optional if there are no actual prior examples in other tools}}

{{Discuss existing examples of this change in other tools, and how they've addressed various concerns discussed above, and what the effect of those decisions has been}}

## Unresolved Questions and Bikeshedding

{{Write about any arbitrary decisions that need to be made (syntax, colors, formatting, minor UX decisions), and any questions for the proposal that have not been answered.}}

{{THIS SECTION SHOULD BE REMOVED BEFORE RATIFICATION}}
