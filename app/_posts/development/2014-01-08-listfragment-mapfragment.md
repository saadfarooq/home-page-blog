---
layout: post
title: Using ListFragment and MapFragment with Tab Switching
publish: false
---

## Using a ListView without Extending ListFragment
I use Dagger for dependency injection and have some custom architecture stuff defined in a `BaseFragment` class (for e.g. all fragment return a tab title value that is used if they are in a tabs activity). Due to this I want to have my ListView be part of standard fragment and not a `ListFragment`.

