# Release Schedule

## Summary

Defining the Schedule and rules for new releases and management of branches

## Motivation

It's important to have clearly defined and sustainable long-term plans for both end-users and maintainers.
Different People/Users have different needs as it relates to stability and new features which are competing goals.
This RFC aims to find a suitable compromise which satisfies all of our users, but also will show us what our users
actually need and want. With this RFC we then also have something for devleopers to reference when contributing and
to resolve disagreements about Releases, timing and what gets into them.

## Detailed Explanation

With this RFC we will define terminology for semantic versioning and rules by which we will build new releases and
manage repo branches and guidelines by which we decide what kind of changes get when merged into which release branch.

### Terminology

Versioning shall follow semver.org guidelines with these tailored definitions:

- MAJOR version when you make incompatible API changes
  - public methods with changed signatures (e.g. new required parameter)
  - removed code that may still be used by some (e.g. unused lib/Zend code or IE8 compat)
  - rename things that could affect users (e.g. xml namespace)
  - dependencies updated in major ways (e.g. dropping support of MySQL 5.6)
    - PHP engine requirements are an exception to this rule if they are effectively enforced by Composer.
- MINOR version when you add functionality in a backwards compatible manner
  - changed code that is very unlikely to have any effect on large majority of users although not guaranteed
  - typical usage is not expected to be affected, only if user was not following best practices
  - no regressions foreseen, but there is always a risk a new feature affects some in unexpected ways
  - performance/stability is improved significantly with little or no negative impacts expected
  - dependencies updated to fix bugs or bring in minor improvements
    - PHP engine requirement changes must be reflected correctly in composer.json so that Composer can select the correct OpenMage version depending on the user's platform
- PATCH version when you make backwards compatible bug fixes
  - best case: fix has zero negative impact
  - worst case: security fix is urgent enough to justify potentially breaking user's stores in a small way (e.g. improving malicious string filtering)
  - functionality: if it doesn't fix a significant regression, it doesn't get a PATCH
  - security/stability: if it doesn't warrant a CVE, it doesn't get a PATCH

### Rules

Given the definitions above, the rules for creating PRs, merging, branching and tagging releases shall be as follows:

- Release timing is flexible (determined by volunteer time availability/motivation/activity) but ideally:
  - roughly 6-12 MINOR releases per year
  - no more than two MAJOR releases per year (since each major release carries some overhead for PATCH updates)
- All new PRs are based on either "main" branch for MINOR and PATCH updates or "next" branch for MAJOR updates
  - If the determination of MINOR vs MAJOR changes, the PR should be updated (possibly rebased) by the author or another maintainer before merging
  - The definition of MINOR and MAJOR should be consulted to determine "which branch?" - If there is disagreement that is
    not quickly (~one week) resolved by discussion, then the de-facto should be the simple majority vote or if majority
    is unclear then it is treated as MAJOR ("next") - OpenMage maintainers may also use discretion to override non-maintainers
- The "next" branch should periodically be updated by merging the latest "main" branch - if urgent, any community member
  may create a PR to merge the latest "main" or port a change into "next" from "main" and this should be accepted without hassle
  - It is not the responsibility of the PR author of a MINOR patch to also maintain the "next" branch
  - OpenMage maintainers may merge "main" into "next" without a PR
- A newly tagged release on "main" bumps the MINOR version and no new branch is created
- Just before a MAJOR release is tagged:
  - Create a new branch from "main" named after the current latest MAJOR version number (e.g. v21 if last release was 21.x.x)
  - Merge "main" into "next" and fast-forward "main" to "next" (so the two should have the exact same head)
  - When a MAJOR release is tagged there should **not** also be a new MINOR release as well, the MAJOR release becomes the
    very next version after the last MINOR release
    - It is possible that to obtain some MINOR updates a user might be required to update to the newest release even if it
      is a MAJOR version bump - or worst case they could specify a commit hash just before "next" was merged
- Only significant security patches or regression fixes can be released immediately in a PATCH release; MINOR and MAJOR
  updates should wait for the next release (e.g. there should not be two MINOR releases in the same month)
  - Users who need features immediately after they are merged should be encouraged to use either "dev-main" or "dev-next"
    and not ask maintainers for quicker releases
- PATCH fixes will *only* be back-ported to MAJOR versions that are less than 2 years (730 days) old - this is the sole
  purpose of the "v*" branches
  - Backporting to old releases can be done by a maintainer directly on the appropriate branches or by the community via a PR
  - The maintenance branches (v19, v20, etc.) may be deleted by any maintainer after they are no longer eligible to receive
    PATCH updates - users should be discouraged from using these branches in production (e.g. `"dev-v19"`) - there is no reason
    to do this because they can just use `"^19"` to always get the latest from the v19 branch until it is EOL at which point
    they must update to a newer MAJOR version

The "next" branch serves as a pre-release area for MAJOR changes in case there should be multiple MAJOR changes merged in
a short period while allowing "main" to continue to be "stable" for users wanting only the latest MINOR updates. It is
expected that most activity will occur in "main".

#### Example

As of now the current releases are 19.4.21 and 20.0.18. The next release containing only MINOR features would be 20.1.0, then 20.2.0
until a MAJOR feature is released so 21.0.0 and so forth. If there is then a security patch it would be merged into "main" and "next"
and released for the latest version (e.g. 21.0.1) and only backported to 20.2.1 (via a branch called v20) and 19.4.22 (via a branch called v19) in this case
if those branches were less than two years old at the time.

### Effects

- Relegates v19 to PATCH-only going forward and v19 basically becomes EOL in 2 years.
- All new releases are at least MINOR versions so it is understood there is basically always a small upgrade risk. This resolves 
  the common issue where a feature is BC breaking but in a very small way - this is always acceptable.
- MINOR releases are as easy as tagging the latest "main" with a new release number. 
- Bleeding-edge users and can easily use "dev-main" or "dev-next" via composer indefinitely.
- Active users of tagged releases can upgrade as new releases are announced using the major/minor numbers as guidance as per semver standards.
- Users wanting minimal upgrade hassle always have at least 2 years to get up to date to the latest major version for another two years or more.

## Implementation

- Create a "main" branch from "20.0" and designate it as the "default" branch in GitHub admin
- Create a "next" branch that is a copy of "main"
- Create a "v19" branch from "1.9.4.x"
- Create a "v20" branch from "20.0"
- Add branch protection rules for "main", "next", and "^v\d+$"
- Add branch protection rule to lock old branches ("1.9.4.x" and "20.0") to avoid accidental merges
- Codify the strategy into the main project `README.md` file using the descriptions above
- Announce new release strategy in a blog post
- Update all existing PRs to the appropriate branch (can be done gradually - enlist the help of community members)
- Delete "1.9.4.x" and "20.0" once there are no more PRs dependent on them (or will PRs just default to "main"?)


## Notes

Accepted via voting on https://github.com/OpenMage/rfcs/pull/10


| **Name**         | **Yes** | **No** |
|------------------|:-------:|:------:|
| fballiano        | ✔️      |        |
| colinmollenhour  | ✔️      |        |
| justinbeaty      | ✔️      |        |
| ADDISON74        | ✔️      |        |
| elidrissidev     | ✔️      |        |
| kiatng           | ✔️      |        |
| FredericMartinez | ✔️      |
| barbanet         | ✔️      |        |
| orsifrancesco    | ✔️      |        |
| MGAndreasen      | ✔️      |        |
| clotted          | ✔️      |        |
