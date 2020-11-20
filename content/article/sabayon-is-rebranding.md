+++
title = "Sabayon project is rebranding to MocaccinoOS"
description = ""
date = "2020-11-20"
categories = [ "sabayon" ]
tags = [
"development",
"sabayon",
]
+++

Howdy! 

It’s been quite a long time since we have made an official post, so here we are, almost at the end of 2020 discussing Sabayon's future and upcoming changes.

Let’s be frank, we are nearing the end of Sabayon as we’ve known it, and we are looking back at what was great, and what could be improved upon. We haven’t been the best at communication - there has been radio silence for almost a year. 

That doesn’t mean we weren’t active, or that we’ve abandoned the project… on the contrary! 

For us this has been a very busy year. We have been building up a new toolset for upcoming releases, and trying to innovate and renew the project for the future. There are big changes coming soon, and now is the right time for us to finally share what’s coming next with you.

## Sabayon project is rebranding to [MocaccinoOS](https://www.mocaccino.org/).

(This won’t be our final logo, we’re looking for contributors for artwork!)

Migration to MocaccinoOS will work from any flavour of Sabayon, and we will keep pushing updates on the Sabayon Linux main repo until MocaccinoOS is fully bootstrapped and officially released to the world.

At the moment of writing, MocaccinoOS is not ready yet for daily usage, and we suggest you do not attempt to migrate any machine you rely upon just yet. That said, we welcome everyone to test out Mocaccino on any spare hardware you might have, or in virtual machines and provide feedback on where we might improve it.

Sabayon users will keep receiving updates on the sabayonlinux.org repositories, but the sabayon-weekly repositories have been frozen already. [See here for instructions for switching between these repositories](https://wiki.sabayon.org/index.php?title=En:Entropy#enabling_a_different_repository_or_mirror).


## New package manager

From 2019 we have been working on a new brand package manager, called [Luet](https://github.com/mudler/luet), which will eventually replace Entropy. It is designed to solve some of the limitations and issues that we have observed while working with Entropy.
Building packages 

Entropy has proven to work well over the years, but it had some big limitations on the maintainer side. For example, it needs a central server to build packages, and packages have been maintained by hand for many years.

This might sound fine, but this approach has several drawbacks:

No easy way to have reproducible builds
No easy way to have divergent packages (e.g. community repositories)
No native distributed compilation (without resorting to something like distcc)
The build server is a single point of failure
Only one person can work on the build server at a time
Special knowledge and tools needed around infrastructure
No way to track changes on the build server in a human readable way (e.g. to backtrack problems)
The power of containers


To address the above mentioned issues, Luet provides an abstraction layer on top of container technologies, like Docker, which let us build packages without having a central server building packages.

Images used to build packages are shared via Docker registries, so they can be reused later on, not only by our main build infrastructure, but also by anyone that wishes to build their own packages against the same environment - or who just wants to inspect the build environment.

Our new package manager solves these disadvantages. We can run reproducible builds, across a wide range of build infrastructure, and the process is much more open to contributors, or for folks to build their own packages using the same tools we use.

### Where Luet comes to play

So why not use just Docker to build packages? 
While this might sound familiar, this is even more familiar to us. We have been using Docker into our infrastructure for more than 5 years already for building ISO images and community repositories.

We encountered a few pitfalls of using Docker directly, which have been addressed in Luet:
No first class representation of a package definition. 
It’s up to you to maintain reverse dependencies of docker images, which images need updating when a base image changes
Images can be based on only a single base image; you can’t have package A coming from Image B and C unless you handle that manually.
No structured way to represent a tree of related images


Luet provides an abstraction layer on top of the container image layer to make the package a first class construct. A package definition and all its dependencies are translated by Luet to Dockerfiles which can then be built anywhere that docker runs.
Dependency resolution
To resolve the dependency tree Luet uses a SAT solver and no database. It is responsible for calculating the dependencies of a package and to prevent conflicts. The Luet core is still young, but it has a comprehensive test suite that we use to validate any future changes.

## Pluggable system
Luet can be extended in 2 ways, by extensions and plugins. 

Extensions expand Luet featureset horizontally, so for example, “luet geniso” will allow you to build an iso using luet, without this needing to be part of the luet core.

Plugins instead are expanding Luet vertically by hooking into internal events. Plugins and Extensions can be written in any language, bash included!

## Musl branch
We are building a Musl LFS branch. It is completely from scratch and has just a few packages, which you can see [here](https://packages.mocaccino.org/mocaccino-musl-universe) and [here](https://packages.mocaccino.org/mocaccino-micro) . The big advantage with Luet here, is that you can build and fork the entire tree and build it locally without any target chroot - Luet will take care of that for you.

## Statically built
And finally, Luet is written entirely in Go and comes as a single static binary. This has a few advantages:
Easy to recover. You can use luet to bootstrap the system entirely from the ground-up. 
Package manager has no dependencies on the packages that it installs. There is no chance of breaking the package manager by installing a conflicting package, or uninstalling one.
Portable - it can run on any architecture


And that’s not all, there’s even more exciting news still to come!


## Call for contributors

We are always looking to grow our community, and to share knowledge and experiences with Linux and computer technology, don’t hesitate to engage and reach us via [slack and discourse](https://www.mocaccino.org/community/)!

## Call for artwork contributions

As we are rebranding into MocaccinoOS we are in need of new artwork! If you have ideas and want to contribute, [reach to us over slack!](https://www.mocaccino.org/community/)
