<p align="center">
  <a href="https://github.com/leisim/awesome-fuchsia">
    <img src="Art/awesome-fuchsia.svg" width="750px">
  </a>
</p>
<p align="center">
  <img src="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg" />
  <a href="https://travis-ci.com/leisim/awesome-fuchsia">
    <img src="https://img.shields.io/travis/com/leisim/awesome-fuchsia.svg" />
  </a>
  <a href="https://stackoverflow.com/questions/tagged/fuchsia?sort=votes">
    <img src="https://img.shields.io/stackexchange/stackoverflow/t/fuchsia.svg?color=orange&label=StackOverflow" />
  </a>
  <a href="https://github.com/topics/fuchsia">
    <img src="https://img.shields.io/badge/Repos-13-brightgreen.svg" />
  </a>
</p>

A curated list of awesome Fuchsia resources, tools and information. If you find anything interesting that belongs on the list, please create a pull request 👍

## What is Fuchsia?
Fuchsia is a modular, capability-based operating system. Fuchsia runs on modern 64-bit Intel and ARM processors.
It is created by Google and completely [open source](https://fuchsia.googlesource.com). Currently it has not been officially announced by Google but it is expected to be revealed at the [IO 2019](https://events.google.com/io/).

## Contents
- [Latest news](#Latest-News)
- [Architecture](#Architecture)
- [Development](#Development)
- [Emulators](#Emulators)
- [Community](#Community)


# Latest News
- [Fuchsia on Android Emulator](https://www.r3pwn.com/blog/2019/05/01/fuchsia_aemu) *[01/05/19]* - How to run fuchsia on android emulator
- [Fuchsia Press Weekly - Newsletter](https://www.xriblu.com/fuchsia-press-weekly) *[Weekly]* - Hand-picked round up of the best Fuchsia development links every week
- [JavaScript app support](https://www.androidpolice.com/2019/03/19/google-working-to-bring-javascript-app-support-to-fuschia/) *[03/19/19]* Google working to bring JavaScript app support to Fuchsia
- [Fuchsia on AMD Chromebooks](https://9to5google.com/2019/03/01/google-fuchsia-amd-chromebooks/) *[03/01/19]* - Google is working on bringing Fuchsia OS to AMD-based Chromebooks
- [Android app support](https://9to5google.com/2019/01/02/android-runtime-app-support-fuchsia/) *[01/02/19]* - Fuchsia OS confirmed to have Android app support via Android Runtime
- [Android Emulator supports Fuchsia](https://9to5google.com/2018/12/05/android-emulator-fuchsia-zircon/) *[12/05/18]* - The official Android Emulator is picking up support for Fuchsia’s Zircon kernel
- [Huawei testing Fuchsia](https://www.xda-developers.com/huawei-testing-fuchsia-os-kirin-970-honor-play/) *[11/23/18]* - Huawei begins testing Fuchsia OS on the Honor Play
- [Fuchsia tested on Home Hub](https://arstechnica.com/gadgets/2018/10/google-home-hub-under-the-hood-its-nothing-like-other-google-smart-displays/) *[10/10/18]* - Google Home hub is reported to be a Fuchsia OS Test Device


# Architecture
- [Fuchsia Glossary](https://fuchsia.googlesource.com/fuchsia/+/master/docs/glossary.md) - Provides short definitions for a collection of technical terms used in Fuchsia
- [Layers of Fuchsia](https://9to5google.com/2018/03/16/fuchsia-friday-the-four-layers-of-fuchsia/) - Short but complete 9To5Google Article
- [Fuchsia Overview](https://www.androidcentral.com/fuchsia) - Introduction to Fuchsia and outlook to it's possible future

![](Art/layers.jpg)

## Zircon (microkernel)
Zircon is the core platform that powers the Fuchsia OS. Zircon is composed of a microkernel as well as a small set of userspace services, drivers, and libraries necessary for the system to boot, talk to hardware, load userspace processes and run them, etc.

- [Quick Start Recipes](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/docs/getting_started.md) - Build Zircon on your machine
- [Concepts](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/docs/concepts.md) - Zircon Kernel Concepts
- [Documentation](https://fuchsia.googlesource.com/zircon/+/HEAD/README.md) - Official Zircon Documentation
- [Source](https://fuchsia.googlesource.com/zircon/+/refs/heads/master/system/) - Zircon source code

## Garnet 
Garnet is the first Fuchsia layer above the kernel. It contains a variety of low-level things that every OS needs including device drivers (network, graphics, etc) and software installation. The Garnet UI services are called `Mozart`.

### Scenic (graphics engine)
Scenic is a Garnet service that composes graphical objects from multiple processes into a shared scene graph. The objects can cast shadows or reflect light onto each other, even if the originating processes have no knowledge of each other.
- [Introduction](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/docs/ui/scenic.md) - Explains concepts of Scenic including `Nodes`, `Scenes` and `Compositors`
- [Source](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/lib/ui/scenic/) - Scenic source code

#### Gfx
Gfx owns the scene graph and is responsible for rendering.
- [Source](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/lib/ui/gfx/) - Gfx source code

#### Input
Input is responsible for routing input events to clients, which also involves coordinating gesture recognition across clients
- [Introduction](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/docs/ui/input.md) - How RootPresenter and Scenic process visually-related input
[Source](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/lib/ui/input/) - Input source code

#### Escher
Escher is a Vulkan-based rendering library used by the *Gfx* system
- [Source](https://fuchsia.googlesource.com/garnet/+/master/public/lib/escher/) - Escher source code

### Amber (updater)
Amber is an update system with the ambition of updating all components running on a Fuchsia system whether that component is a kernel, a bootloader, a system service, an application, etc.
- [Introduction](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/go/src/amber/README.md) - Short introduction to Amber
- [The Update Framework](https://theupdateframework.github.io ) - Basis for Amber's update distribution
- [9To5Google Article](https://9to5google.com/2018/03/09/fuchsia-friday-amber-keeps-fuchsia-up-to-date-and-secure/) - This article gives an easy to understand introduction to Amber
- [Source](https://fuchsia.googlesource.com/garnet/+/refs/heads/master/go/src/amber/) - Amber source code

## Peridot
Peridot provides the services needed to create a cohesive, customizable, multi-device user experience assembled from modules, stories, agents, entities, and other components.

### Modular
Modular is the application framework for Fuchsia. It manages user experiences by composing UI, data, and users from a diverse set of components into logical and visual containers called Stories.
- [Overview](https://fuchsia.googlesource.com/peridot/+/refs/heads/master/docs/modular/overview.md) - Basic concepts of Modular
- [Simple Example](https://fuchsia.googlesource.com/peridot/+/refs/heads/master/examples/simple/) - Simple Fuchsia program (C++) using the modular framework

### Ledger (cloud sync)
Ledger is a distributed storage system for Fuchsia.
Each application running on behalf of a particular user has a separate data store managed by Ledger. It is transparently synchronized across devices of its user by cloud providers.  
The goal of ledger is that the user does not notice it while it 
- [Ledger state](https://fuchsia-ledger.firebaseapp.com/) - View all data collected by your ledger
- [Cloud provider interface](https://fuchsia.googlesource.com/peridot/+/refs/heads/master/public/fidl/fuchsia.ledger.cloud/cloud_provider.fidl) - Definition of a cloud service that can be used by ledger
- [Firestore cloud provider](https://fuchsia.googlesource.com/peridot/+/refs/heads/master/bin/cloud_provider_firestore/) - A Firestore-based implementation of the cloud provider interface
- [Life of a put](https://fuchsia.googlesource.com/peridot/+/HEAD/docs/ledger/life_of_a_put.md) - Explanation how Ledger works by following the mechanics of a single Put operation
- [Source](https://fuchsia.googlesource.com/fuchsia/+/refs/heads/master/src/ledger/) - Ledger Source code

## Topaz
Topaz contains four major categories of software: modules, agents, shells, and runners.  
For example, modules include the calendar, email, and terminal modules, shells include the base shell and the user shell, agents include the email and chat content providers, and runners include the Web, Dart, and Flutter runners.
- [Simple App](https://fuchsia.googlesource.com/topaz/+/HEAD/examples/ui/simple_flutter) - Very simple Flutter App for Fuchsia
- [Mine Sweeper](https://fuchsia.googlesource.com/topaz/+/HEAD/examples/mine_digger/) - Flutter implementation of minesweeper for Fuchsia
- [Source](https://fuchsia.googlesource.com/topaz/+/refs/heads/master) - Topas source code


# Development

## Build Fuchsia
You can build and run Fuchsia yourself.
- [Getting Started](https://fuchsia.googlesource.com/docs/+/refs/heads/dart-docs/getting_started.md) - First steps on building Fuchsia
- [Get Fuchsia Source](https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/source_code/README.md) - How to get the Fuchsia Source 
- [Bazel](https://bazel.build) - Build tool for Fuchsia

## SDK
The Fuchsia Core SDK contains a small set of libraries and tools required to start building and running programs that target Fuchsia
- [Introduction](https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/sdk/README.md) - Introduction to the Fuchsia SDK
- [Download SDK](https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/sdk/download.md) - Download the Core SDK package, Bazel and Qemu

## Flutter
Flutter allows you to build beautiful native apps on iOS, Android and Fuchsiafrom a single codebase.
- [Get Started](https://flutter.dev/docs/get-started/install) - Install Flutter on your machine
- [Dart Pub](https://pub.dartlang.org/) - All Flutter packages and libraries
- [Awesome Flutter Packages](https://github.com/leisim/awesome-flutter-packages) - Collection of the best Flutter packages (with images)
- [Awesome Flutter](https://github.com/Solido/awesome-flutter) - Collection of Flutter packages, articles and resources

## FIDL
The **F**uchsia **I**nterface **D**efinition **L**anguage is the language used to describe interprocess communication (IPC) protocols used by programs running on the Fuchsia Operating System.
- [Official Tutorial](https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/languages/fidl/tutorial/README.md) - Best resource to start FIDL development
- [FIDL examples](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/host/fidl/examples) - List of easy to understand examples

## Fuchsia Packages
A Fuchsia package is one or more collections of files that provide one or more programs, components or services for a Fuchsia system.
- [Introduction](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/go/src/pm/README.md#structure-of-a-fuchsia-package) - Introduction to Fuchsia packages
- [Developing a Package](https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/workflows/package_update.md) - Basics of a package-driven workflow in Fuchsia


# Emulators
- [Qemu](https://www.qemu.org/) - A generic machine emulator and virtualizer that works with Fuchsia
- [Fuchsia Web Demo](https://mgoulao.github.io/fuchsia-web-demo/) - Fuchsia Demo running in your browser
- [Armadillo APK](https://mega.nz/#!r88zVaBS!gr6dcaWVd6y9lIAiIcMmeiKHCia0fjaa_IHVLa37wr8) - An APK of the (outdated) Armadillo UI


# Community
- [r/Fuchsia](https://www.reddit.com/r/Fuchsia/) - Fuchsia subreddit with news and information about Fuchsia
- [Fuchsia OS 中文社区](https://t.me/FuchsiaOSzh) - Fuchsia China Telegram Group with news and information about Fuchsia


## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, Simon Leier has waived all copyright and related or neighboring rights to this work.
