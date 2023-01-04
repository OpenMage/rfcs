# Migrate openmage.readthedocs.io to Awesome OpenMage

## Summary

This RFC proposes to remove https://openmage.readthedocs.io and migrate its contents to the ["awesome" format](https://github.com/sindresorhus/awesome).

## Motivation

OpenMage's readthedocs has some basic info about the project and a list of modules/extensions, but it doesn't look very modern, the navigation is not really quick and most of all it has [almost zero contributions](https://github.com/OpenMage/documentation/pulls).

This RFC aims to re-create the same "concept" with a different tool, which is considered a de-facto standard (the awesome format) which would provide a more modern look, an easier way for people to interact and contribute and overall a better image for OpenMage.
 
## Detailed Explanation

Every developer is used to the awesome format, it is widely used for every kind of topics.
The look and feel is the standard GitHub's markdown formatting, which is clean and modern and "standard".
When developers come across an "awesome" repository they know they can contribute easily just by adding a line to a list, so it's gonna be much easier that people will contribute to the list.

Removing openmage.readthedocs.io we would also spare hosting costs/resources (which somebody is not paying/offering), which is a good thing since wasting resources is never good. Not relying on a hosting donation also allows OpenMage to be even more independent.

**Why is people not contributing to openmage.readthedocs.io?**

- since it looks like a website, you (as a contributor) think it's gonna be difficult to contribute, maybe I'll have to read some HTML code and respect certain formatting rules that I don't know, maybe github is not the right place because maybe the entries are stored in a database... this kind of psycological processes.
- In order to know what to modify when creating a PR, you've to go to https://github.com/OpenMage/documentation and understand the folder/file structure, which is not hard but for sure way harder than an "awesome" format. There's some python code, a .bat file, mixed stuff not everybody wants to read in order to understand how to contribute.

## Rationale and Alternatives

There is an alternative, which is to work on the openmage.readthedocs.io repository and website to make it better looking and easier to contribute to. But I don't think we have the manpower for that and the end result still wouldn't loo as "standardized" as the "awesome" format.

## Implementation

1. Since [this Awesome OpenMage](https://github.com/fballiano/awesome-openmage/) already exists (although it's far from being complete) my suggestion is to fork it under the OpenMage main account (in order to have it as github.com/OpenMage/awesome-openmage) and continue from there.
2. Remove all the content from openmage.readthedocs.io and just implement a 301 redirect to the awesome-openmage repository.
3. Link the awesome-openmage in the main repo's README file (and in the openmage.org website) for easy finding.
