# Translatable strings management rule

## Summary

In OpenMage PHP files we've a lot of translatable strings, used to send messages to users, these strings and then translated though CSV files.

What happens when we need to change one of these translatable strings (eg: because of a typo)?
We need a clear rule for developers to follow in order to avoid re-discussing the topic every time a PR involves a translatable string.

## Motivation

There have been too many discussions (about this specific topic) and it's not useful to keep doing it over and over again, we need to vote on this matter and decice a clear strategy once and for all.

## Detailed Explanation

Some of the discussions we had about the topic:
- https://github.com/OpenMage/magento-lts/discussions/2590
- https://github.com/OpenMage/magento-lts/discussions/2585
- https://github.com/OpenMage/magento-lts/discussions/2429

Issues where we had to discuss translations related stuff:
- https://github.com/OpenMage/magento-lts/search?q=csv+language+pack&type=issues

Why are all this discussions happening? Because we do not control language packs, there are many, they're usually pretty old and they have many different maintainers.
Every time we add/change a translatable string in OpenMage's PHP files we're breaking all the language packs out there.

Enless discussions create friction and I'm sure we want everything but that for our community.

## Rationale and Alternatives

### 1. Do not modify translatable strings in PHP files, only in CSV files

**PRO**: It doesn't break language packs, which, important to re-state, we do not have control over.

**CON**: It doesn't look as clean as option 2. Language packs will still be technically working but they may need a "refinement" update anyway.

**Exception**: if changing a translatable string changes its meaning significantly, then this solution shouldn't be applied and the change should be considered a breaking change.
Example (extreme, for the sake of argument): changing "this product can be added to the cart" to "this product cannot be added to the cart" should be changed in both PHP/CSV files and considered a breaking change.

### 2. Keep translatable strings in sync between PHP and CSV files

**PRO**: it is for sure nice to have all translatable strings in a coherent state, between PHP and CSV files.

**CON**: Every change breaks all language packs.

## Implementation

There's nothing to technically implement for this RFC.
