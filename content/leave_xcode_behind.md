+++
title = "Leaving Xcode behind"
date = 2019-07-15
description = "Using command line tools instead of xcode"
draft = true
in_search_index = true

[taxonomies]
categories = ["swift"]
tags = ["swift","debugging","xcode","lldb"]
authors = ["ThangaAyyanar"]
+++

I want to explore, What is the current status of deploying iOS apps without opening xcode

Sometimes xcode seems overkill for me so need some alternative when xcode
didn't work as i intented.

## Source Code Editor
- I like neovim and plugins that i use
    - swift highlighting(https://github.com/keith/swift.vim)
    - IDE functionalities AKA code intelligence
        - Conquer of Completion with coc-swift
- VSCode has the same functionalities

## Building targets(Apps)
- Shell script using xcodebuild tool
- Use `XCPretty` tool for human readable compile instructions
Cons
    - No incremental build (as far as i know of)

## List Simulator and devices with versions
```
xcrun xctrace list devices
```

## Managing Simulator
Tools to make simulator
- iSimulator
Commands to 
```
xcrun simctl
```

## Debugging
well we can lldb which comes default with xcode.
other tools which make it better
- chisel
- voltron

using -w option along with above command will wait for debugger to attach
xcrun simctl launch -w --console-pty booted <Bundle Identifier>

then in other window `lldb -n <processname> -w`

Cons
    - Breakpoint from editor

## Logs

- Running xcrun with --pty-console will provide logs
```
xcrun simctl launch --console-pty booted <Bundle Identifier>
```

## Installing to device
idevice

## Workflow
Tmux 
window 1: neovim (project)
window 2: logs + debugger

## Additional Tools
Optional: Bagel
Xcodeproj generation using [Xcodegen](https://github.com/yonaskolb/XcodeGen)

## Dwarfdump
```
xcrun dwarfdump --uuid <PATH_TO_APP_EXECUTABLE>
```

Surprise
xcrun - tool that manage other utility.
