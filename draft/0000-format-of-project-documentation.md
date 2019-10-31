# Formate of Project Documentation

## Summary

Defining the format and place the projects documentation is hold

## Motivation

As a project with a rather big amount of code and Features, and possibly differences at one point between versions,
we would strongly benefit of having a place and format for working on this documentation.

Excamples:
* https://symfony.com/doc/current/index.html
* https://devdocs.magento.com/#/individual-contributors
* https://laravel.com/docs/6.x

{{Why are we doing this? What pain points does this resolve? What use cases does it support? What is the expected outcome? Use real, concrete examples to make your case!}}

## Detailed Explanation

{{Describe the expected changes in detail, }}

## Rationale and Alternatives

Alternative 1: extend the phpdoc blocks and use them as base to render the documentation

pros:
* already existing in parts
cons:
* closly bound to code
  - harder to build code independent documentation
  - creates a big amount 

Alternative 2: via Github Pages rendering

pros:
* low efort
cons:
* low flexibility

{{Discuss 2-3 different alternative solutions that were considered. This is required, even if it seems like a stretch. Then explain why this is the best choice out of available ones.}}

## Implementation

a popular free hoster for such documentations is https://readthedocs.org/

It is using Sphinx ( http://www.sphinx-doc.org/en/master/ ), a software specialized and battletested for documentation.

Best place is probably a separate repository

{{Give a high-level overview of implementation requirements and concerns. Be specific about areas of code that need to change, and what their potential effects are. Discuss which repositories and sub-components will be affected, and what its overall code effect might be.}}

{{THIS SECTION IS REQUIRED FOR RATIFICATION -- you can skip it if you don't know the technical details when first submitting the proposal, but it must be there before it's accepted}}

## Prior Art

{{This section is optional if there are no actual prior examples in other tools}}

{{Discuss existing examples of this change in other tools, and how they've addressed various concerns discussed above, and what the effect of those decisions has been}}

## Unresolved Questions and Bikeshedding

{{Write about any arbitrary decisions that need to be made (syntax, colors, formatting, minor UX decisions), and any questions for the proposal that have not been answered.}}

{{THIS SECTION SHOULD BE REMOVED BEFORE RATIFICATION}}
