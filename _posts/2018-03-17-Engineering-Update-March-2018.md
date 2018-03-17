---
layout: post
title:  "Engineering Update March 2018"
date:   2018-03-17 1:00:00 -0700
author: Input Club
tags: update engineering keyboards firmware case pcb configurator fun
---

<hr>

Here at Input Club we tend to do a lot more than what gets publicized in our product and Kickstarter updates.
And while all our code and designs are opensource and up on [GitHub][github-kiibohd] it can be overwhelming (even for engineers!) to figure out what we’ve actually been working on.
So the engineering team here at [Input Club][inputclub] is going to start publishing monthly updates on what we’ve been working on!

<hr>

First off, introductions of the team are in order.


### [HaaTa][github-haata] - Jacob Alexander

Before turning this into a biography, let’s just say HaaTa has too many projects :laughing:.
He works on a bit of everything at Input Club.
Inventor of KLL, main firmware engineer for Input Club, [keyboard collector][flickr-haata], measurer of [force curves][plotly-haata], [Hako][hako-true]/[Halo][halo-true] switch inventor and designer of keyboards at Input Club.
He’s been in the keyboard community since 2009 and is always excited to talk about keyboards.


### [Parak][github-parak] - Gennadiy Nerubayev

At Input Club, Parak is responsible for PCB design and all-around [KiCad][kicad] wizard.
He keeps PCB fabs on their toes with his stringent manufacturing checklist (we’ve qualified a lot more pcb fabs than we’d care to admit here at Input Club :sweat_smile:).
Parak, the [ebay][ebay] master responsible for most of HaaTa’s keyboard collection, is a proficient collector in tools of great quality (such as [IBM keyboards][deskthority-ibm-parak]) in his own right.


### [Over^Kill][github-overkill] - Brandon Muzzin

Ever wonder how Input Club makes their simple, but beautiful, cases.
By going Over^Kill, that’s how :stuck_out_tongue:.
Over^Kill deftly designs the cases, not just to look good (as an engineer), but designed to be manufactured to keep the quality high and the failures low (because he’s a manufacturing wizard).
Lately he's been really into using [IronCAD][ironcad].
Over^Kill also helped turn HaaTa's proposed force curve in the final [Hako][hako-kono] and Halo switches.


### [jbondeson][github-jbondeson] - Jeremy Bondeson

Master of the [configurator][web-configurator] and all things related to the web, jbondeson is a connoisseur of keycaps.
He has all sorts of cool things planned out for the desktop configurator all in the name of [R, G and B][ktype-rgb].
In his quest for quality, he rewrites code about just as much as HaaTa does :metal:.


### [smasher816][github-smasher] - Rowan Decker

While the most recent addition to the Input Club team, smasher816 has been helping out since before the [Infinity 60%][infinity-60] first shipped out in 2015 :cat:.
Proficient in both PCB and firmware design.

<hr>


# Git Repos

Next up, git repos! [Open Source][what-is-opensource] is very important to Input Club :tropical_drink:.
It likens back to a day where you got a [service manual][ibm-service-manual] with your keyboard (1970s IBM) and you could just lookup the part :memo: that was not working correctly.
Or better yet, figure out how to build your own!

Unless otherwise specified, we use [GPLv3][gplv3] for software and the [CERN OHL v1.2][cern-ohl-v1.2] for things we work on.
Or if we're contributing back to another [project][bossa], we maintain that [license][bossa-license] (and usually try to [upstream changes][bossa-upstream]).

All the Input Club git repos can be found on [GitHub][github-kiibohd].


## [controller.git][controller-git]

The controller git repo contains all the code that goes onto the keyboard as firmware.
For those that are not familiar, firmware is compiled software that is stored on a non-volatile device (like inside a keyboard’s flash storage).
This repo contains both the :truck: driver code for various keyboard MCUs ([microcontrollers][microcontroller]) as well as the implementation of [KLL][kll-inputclub].
This is the repo you should be watching if you’re interested in new keyboard features and bug-fixes.

The code here is mainly written in [C][c-prog] with a [CMake][cmake] build system.

Both [Travis-CI][travis-ci-controller] and [Appveyor][appveyor-controller] are used to make sure the firmware can be compiled for Windows ([Cygwin][cygwin]/[Bash][windows-linux]), Linux and macOS.
The recommended way to compile the firmware manually is through [Docker][kiibohd-docker].


### Some fun facts

* [TMK][tmk] (where [QMK][qmk] was derived from late [2014][qmk-contributors]) was started back in [2010][tmk-contributors] by  [hasu][hasu] and the kiibohd controller firmware, by HaaTa, early [2011][controller-contributors].
Both were designed as protocol converters, and both started with the [PJRC Teensy 2.0][teensy-2.0].
:stars: [Soarer][soarer], [hasu][hasu-gh] and [dfj][dfj] all conspired on the [GeekHack][gh] [IRC channel][gh-irc] (#geekhack@irc.freenode.net) to develop what we know today as USB NKRO that works across Windows, Linux and macOS.

* Soarer developed his own [protocol converter for XT/AT/PS2/Terminal keyboards][soarer-converter] to USB (using a Teensy [2.0][teensy-2.0] or [2.0++][teensy-2.0++]).
dfj, while not well known, developed one of the [first custom Model F capacitive sense][dfj-controller] controllers a couple years before :boat: [xwhatsit][xwhatsit-controller].
You can find the schematic for one of the later versions of the capsense controller on our [GitHub][dph-pcb] (was originally hosted on [Gitorious][dph-gitorious] which [closed][gitorious]) which was named DPH for dfj, parak and HaaTa.

* The Input Club [Infinity 60%][infinity-60], which shipped in early 2015, was likely the first production keyboard to support USB NKRO on Windows, Linux and macOS out of the box with no extra drivers or configuration necessary :godmode:.

* The [Infinity Ergodox][infinity-ergodox] interconnect runs at 4.5 [megabaud][baud].
With a symbol size of 8 bits, that would put the link at a 562 500 Hz [polling rate][polling-rate] :rocket:.
USB 2.0 FS is only polls for new data at 1000 Hz :turtle: and even USB 3.1 Gen 2 at 8000 Hz :rabbit:.
For reference, a standard USB 2.0 LS keyboard only polls data at 125 Hz :no_good:.

* Work on the [K-Type][k-type] started (at least the KLL portion) started even before the Infinity 60% launched (just a few days prior) back in October 2014 while HaaTa was flying to Japan (to go drinking with hasu again :beers:).

* While the firmware was originally based on the Teensy 2.0 and [3.0][teensy-3.0] codebases the original [schematics][mchck-schematic] and [bootloader][mchck-bootloader] were forked from the [McHCK project][mchck].

* The K-Type animations run at [100 fps][k-type-100fps].
The original goal was 30 fps :sunglasses:.
Both the WhiteFox and Infinity Ergodox hardware also support 100 fps animations.

* The LEDs in any Input Club keyboard will not turn on until USB has been fully negotiated.
This means if the LEDs turn on, the firmware is doing something :thumbsup:.


## [kll.git][kll-git]

This repo contains the KLL compiler source code.
KLL is the [DSL][dsl] that HaaTa wrote to define keyboard functionality in a distinct and widely compatible way.
It uses a powerful :muscle: `Trigger:Result` mapping idiom design to smoothly compile down into code that can be compiled for a microcontroller.

The compiler is written in [Python][python] and is based on [funcparserlib][funcparserlib].

The KLL compiler supports multiple [emitters][kll-emitters], so while it currently supports kiibohd, KLL (yes it can regenerate back to a KLL file) and none (syntax checking), it is possible to add KLL support to other keyboard firmwares just by adding a new emitter.

[Travis-CI][travis-ci-kll] is used to test the KLL compiler against a variety of Python 3 versions.


### Some fun facts

* The KLL compiler supports multiple [emitters][kll-emitters].
Therefore it’s possible to add KLL support to other keyboard firmwares or anything that supports key mapping.

* For the K-Type (and LED support) the KLL compiler was :persevere: [entirely rewritten][kll-rewrite] as a multi-staged parsing compiler.
Parsing rules first determine what kind of expression before extracting detailed information.
This makes it much easier to write parsing rules and not break unrelated rules.

* The Python funcparserlib parsing expressions resemble [xBNF grammars][xbnf].

* The KLL compiler was started in the [summer of 2014][kll-contributions] while the KLL spec has origins all the way back to 2011 :bookmark:.


## [kll-spec.git][kll-spec-git]

The kll-spec repo contains the KLL spec (written in [LaTex][latex]).
If you’re interested in seriously understanding KLL you’ll definitely want to read the spec.
So far only [0.3d][kll-spec-0.3d] is fully implemented; however, much of [0.5][kll-spec-0.5c] has been added (i.e. LED support).
The major feature left to implement in KLL 0.5 is state-scheduling (e.g. tap-keys, short/long presses).

Overleaf was used to compile/maintain the docs in the past.
Unfortunately there have been some issues :cry: lately so all compilation hosting is done on [GitHub][kll-spec-release] now (using [Travis-CI][travis-ci-kll-spec]).


### Some fun facts

* KLL (0.2c) was first unveiled at the 7th Kiibohd Bay Area keyboard meetup (in San Francisco) on May 31st, 2014, hosted by [keyboard.io][keyboardio].
The KLL spec already had provisions for analog keyboards.

* No compiler was made for KLL 0.2 and lower.


## [configurator.kll][configurator-git]

This is the :fire: [awesome desktop app][configurator-youtube] that jbondeson has been working on.
It was designed to handle both layout mapping as well as LED configuration for you keyboard.
Rather than attempting to bundle a compilation environment, the configurator uses a KiiConf server to handle firmware generation.

Written mainly in [Clojure][clojure].

Both [Travis-CI][travis-ci-configurator] and [Appveyor][appveyor-configurator] are used to automate the release generation.
All of the releases (including release notes) can be found on [GitHub][configurator-releases].


## [KiiConf.git][kiiconf-git]

Originally started by :shipit: [matt3o][matt3o] for the [WhiteFox keyboard][whitefox], KiiConf is the [web-based configuration utility][web-configurator] for our keyboards.
Using your configuration it generates a KLL file.
Which the configurator backend then uses to generate a [firmware][firmware] bundle.

Written mainly in [JavaScript][javascript] but also contains quite a bit of [PHP][php] and [Shell code][bash] as well.

[Travis-CI][travis-ci-kiiconf] is used, in combination with [docker][docker-project], to make sure releases keep on working!


## [kiidrv.git][kiidrv-git]

This is a relatively new repo forked from [libwdi][libwdi] by smasher816.
It contains the code for the upcoming automated [Zadig][zadig] driver installation (no more messing with Zadig!).

Written in [C][c-prog] and [C++][c++-prog].

[Appveyor][appveyor-kiidrv] is used to generated automated builds.

Do remember that for drivers Win32 vs. x64 really does matter.


## [case.git][case-git]

The cases of Input Club are :triangular_ruler: designed by Over^Kill using [IronCAD][ironcad].
We generally opensource ([CERN OHL][cern-ohl-v1.2]) the design around 30 days (usually because we’re really busy :horse_racing: trying to ship the keyboard, haha) after the first units of a design ships.
There are a few reasons for this, though the most important is to make sure we release files that are the same as what ships.

The files can be opened using any 3d model/cad program that can work with .step files (e.g. [FreeCAD][freecad]).


## [pcb.git][pcb-git]

Input Club’s [pcb][pcb] are :triangular_ruler: designed by Parak using [KiCad][kicad].
We opensource ([CERN OHL][cern-ohl-v1.2]) the [schematic][schematic], [layout][pcb-layout], BOM (bill of materials) as well as the :cake: [gerbers][gerbers] used to manufacture the pcbs.
These are generally released around the same time as the case.
Historically we generally revise the pcb between runs more often than the case.

[KiCad][kicad] can be used to view the schematics, layout and gerbers (though we recommend [gerbv][gerbv] on Windows and Linux for viewing gerbers).


## [dfu-util.git][dfu-util-git]

A small :fork_and_knife: fork of [dfu-util][dfu-util] to maintain a [macOS binary release](https://github.com/kiibohd/dfu-util/releases) of dfu-util.

Written in [C][c-prog].

Uses [Travis-CI][travis-ci-dfu-util] to publish releases.


## [kii-dfu.git][kii-dfu-git]

This is the :older_man: old Windows GUI front-end for [dfu-util][dfu-util].
It has been long deprecated, please use the configurator instead.
While it also works for macOS and Linux it is tricky to package correctly for all distributions.

Written in [C++][c++-prog] and [Qt5][qt5].


## [manufacturing.git][manufacturing-git]

This repository contains both some scripts used in keyboard :construction_worker: manufacturing ([bootloader][bootloader] flashing) as well as a detailed [wiki](https://github.com/kiibohd/manufacturing/wiki) on the tools and processes needed to flash and validate shipping keyboards.
The wiki also has details on how to build a bootloader flashing adapter which is useful if you’re trying to manufacture your own pcb.

If you’re interested in how we manufacture keyboards, definitely reach out to HaaTa on [Discord][discord].


## [programmer.git][programmer-git]

A fork of the :sheep: [McHCK][mchck] [SWD][swd] flashing utility for the [BusPirate](https://github.com/mchck/mchck/wiki/Getting-Started#bus-pirate).
Contains some small updates for the [Kinetis][kinetis] [mk20dx256vlh7][mk20dx256vlh7] MCU as well as some additional debugging used in manufacturing.

This isn’t needed unless you’re looking at flashing the bootloader on your keyboard with a BusPirate in SWD mode.
Also, don’t worry, you don’t need a bootloader update (you’re not missing out on any keyboard features).

Written in [Ruby][ruby].


## [openocd.git][openocd-git]

This is a small fork of :octopus: [OpenOCD][openocd-upstream] which contains patches for using openocd with a BusPirate and the [SWD][swd] protocol.
The [BusPirate][buspirate] and OpenOCD are used in manufacturing, though we use [JTAG][jtag] if possible (same cable, much faster but is not supported by all MCUs).

Written mainly in [C][c-prog] and [TCL][tcl].


## [force.git][force-git]

While not particularly useful for most of you, this repo contains the firmware source as well as algorithms used for :ram: [HaaTa’s force gauge][problem-with-mechanical-switch-reviews].

It also contains the code which publishes the graph data onto [Plotly][plotly-haata].

Written mainly in [C][c-prog] (firmware) and [Python][python] (algorithms and web interaction).


## [BOSSA.git][bossa]

This is a relatively new repository fork.
:dancer: [BOSSA][bossa] is a tool used to flash MCUs with the [SAM-BA][sam-ba] integrated bootloader which will be used for manufacturing of [SAM4S][sam4s] keyboards.
It has GUI and command line releases for Windows, Linux and macOS.

Written mainly in [C++][c++-prog].

<hr>


# Recent Development


## [Configurator][configurator-git]

The latest version of the configurator (it’s auto-updating! :v:) can always be found on [GitHub][configurator-releases].
Our most recent release is [v0.4.1](https://github.com/kiibohd/configurator/releases/tag/v0.4.1).

The configurator is comprised of two parts, the UI (the configurator download) and the [KiiConf][kiiconf-git] server (which handles generating the firmware image).
We update these two pieces separately as we qualify stable firmware for the configurator rather than just releasing the latest (and possibly unstable) firmware.

Manufacturing before :confetti_ball: [Chinese Lunar New Year][chinese-lunar-new-year] has put a damper on configurator development, but it should start to ramp-up again soon. The next two new features to help simplify firmware downloading.

The first would be, auto-downloading of [dfu-util][dfu-util] binaries.
Not all computers have a working version of dfu-util available so if the configurator can’t find one on the system the configurator will download a known working dfu-util for your system.
This is particularly helpful for both Windows and macOS.

The second is automating the [Zadig][zadig] driver installation.
Using the new kiidrv project by smasher816, we can automatically determine whether you need to install the Zadig driver and handle it for you.
No more accidentally installing the driver on the wrong interfaces!


## [Firmware][controller-git]

We’ve been hard at work on the keyboard firmware since the [K-Type][k-type] launched working on :bug: bugs and adding new :full_moon_with_face: features.

One of the major improvements to the firmware was moving from a single execution loop to two concurrent threads.
Prior to the K-Type, the only heavy lifting the MCU had to do was [scan keys](https://en.wikipedia.org/wiki/Keyboard_matrix_circuit), send updates to USB and occasionally update some peripherals (e.g. LCD screen, change LED :high_brightness: brightness, etc.).
However, to fully utilize the RGB’ness of the K-Type a high frame rate required using the majority of the CPU time servicing animations...instead of scanning for keypresses.

After thinking about the problem for a while, HaaTa decided to rewrite a large portion of the firmware and split execution into two different paths.
You can think of it as two different [threads][threads]: one that runs consistently and reliably for key scanning and the other as :dash: fast as it can to deal with animations.
[Periodic](https://github.com/kiibohd/controller/blob/fdeba952b058968682316edbb5beb0ebf01c9110/main.c#L66) and [polling](https://github.com/kiibohd/controller/blob/fdeba952b058968682316edbb5beb0ebf01c9110/main.c#L125), respectively.

To prevent flickering, each LED frame must be serviced as quickly as possible.
Which means you need to spend as little time away from the LED processing as possible.
And, instead of scanning all the keys, then processing all the LEDs, just process one strobe (matrix column) of keys at a time.
Then process one frame of LEDs, then onto the next strobe.

For those that are curious, the `periodic` [cli command][cli-debugging] will let you adjust, in real time, how many cycles to wait between periodic scans.

Work has been done to fix issues with KLL macros as well as some offset errors which were causing some keyboards to reset (yep, [off by 1 bug][off-by-one]).
These were all fixed using the new the :scroll: **Self-Testing KLL** build feature.

The other large project going on right now is preparing the firmware for Kira.
This will be the first keyboard design since 2015 to use a new [MCU][microcontroller]! More [SRAM][sram] for code, more [flash][flash] for animations, more :japanese_ogre: [Hz][cpu-frequency] for spamming USB packets over the interwebs.
All-in-all, just better.
However, we’re moving away from [NXP][nxp]’s (originally [Freescale][freescale]’s) [Kinetis][kinetis] [K20][k20] line and onto [Microchip][microchip]’s (originally [Atmel][atmel]’s) [SAM4S][sam4s] line of MCUs.
Also, before you say anything :speak_no_evil:, no, this isn’t an [AVR][avr], it’s a full blown [ARM][arm] [Cortex-M4][cortex-m4], just like the Kinetis K20 series.


## [KLL Compiler][kll-git]

Recently there have been a lot of changes in the KLL compiler in regards to [JSON][json] output.
JSON is used by both the [configurator][configurator-git]/[KiiConf][kiiconf-git] as well as [host-side KLL][host-side-kll] to gather more information that is available to the KLL compiler, but not the final output generated by the KLL compiler.
This includes things such as all defined KLL capabilities, per-layer `trigger:result` pairs and physical keymapping.

Another recent change was classifying some capabilities as :guardsman: [thread-safe][thread-safe].
With the recent change in the controller firmware to use 2 threads of execution (periodic and poll) some capabilities may need to access resources that are not thread-safe.
Capabilities that are thread-safe may be called immediately inside the periodic thread, while non-thread-safe capabilities must be queued up for the polling thread.


## [KLL Spec][kll-spec-git]

As we’re still trying to catch-up and finish the [KLL 0.5][kll-spec-0.5c] support, there hasn’t been a lot of action on the KLL spec.
However, there are a few things that will likely sneak into the KLL 0.5 spec before it is complete.
Something that will make it for KLL 0.5 are lock LED triggers.
These are useful for triggering off of things such as :see_no_evil: CapsLock and NumLock.

<hr>


# Recent Projects


## [kiidrv][kiidrv-git]

If you use one of our keyboards on Windows, you probably recognize this.

![](https://i.imgur.com/2j6hcOi.jpg)

And if you’ve been unlucky :hear_no_evil:, you’ve probably messed up and had to uninstall the driver as well (which is a bit tricky).
[Zadig][zadig] is a great tool, but why can’t it just be done for you (like on macOS and Linux) and just work.
That’s the goal of kiidrv, to make flashing your keyboard on Windows more seamless.

smasher816 integrated both [libwdi][libwdi], the library used to create Zadig and [devcon][devcon], an API to work with the Device Manager, to create kiidrv.
This means we can not only install the correct driver for your keyboard, but also validate that you’ve only installed it correctly (in case you used Zadig on the wrong device by :hurtrealbad: mistake; really easy to do btw).

Feel free to use kiidrv in your own projects :smiley_cat: as it’s fully opensource under [GPLv3][gplv3] and [LGPLv3][lgplv3], and just a useful tool in general.
Make sure to download the correct architecture for your version of Windows.

* [Instructions](https://github.com/kiibohd/kiidrv/tree/master/kiidrv)
* [Release](https://github.com/kiibohd/kiidrv/releases)


## Self-Testing KLL

For a long time HaaTa has had a difficult time :rage1: testing [KLL][kll-git].
By design, KLL supports an enormous number of configurations :rage3: multiplied by the number of keyboards that support it.
Sadly, this means it’s also :rage4: impossible to test every configuration ahead of time.

But, KLL has a very :suspect: interesting design aspect to it.
The `trigger:result` pairs that define what you pressed and what should happen when you press.
Or said a different way, both input and outputs are known ahead of time :godmode:!
This means KLL defines what we’re expecting to happen, which for those software engineers out there means that this is actually a constrained problem that can be unit tested.

{% highlight bash %}
# Pressing key, 0x10, should result in A
S0x10 : U"a";

# Pressing key, 0x24, should result in B
S0x24 : U"b";

# Pressing abc, should result in xyz
'abs' : 'xyz';
{% endhighlight %}

So, back in 2016 HaaTa began his port of the KLL firmware to :computer: [x86][x86].
Instead of setting up a complicated hardware setup, the KLL firmware implementation relies entirely on CPU instructions, so no emulation is required for the `trigger:result` macro logic.
Then, to support all of the hardware specific calls, Python callbacks were implemented with [Scan](https://github.com/kiibohd/controller/tree/master/Scan/TestIn) and [Output](https://github.com/kiibohd/controller/tree/master/Output/TestOut).
The goal of this shared library :green_book: (`kiibohd.so`) was to be able to control the KLL processing :bicyclist: cycle-by-cycle in order to construct any sort of situation that may occur on a keyboard.
Even the ones that are basically impossible to trigger on a physical keyboard (e.g. press 10 keys in a row exactly 10 us apart for 3 ms each).

The tests not only require interaction with the newly generated `kiibohd.so`, but also what the input and outputs of `trigger:result` pairs are.
Instead of re-parsing the KLL files, the KLL compiler generates a `kll.json` file which contains detailed information about the compiled KLL layout.
With this information a test can be generated for each possible key combination on each layer and what the result of each test should be.

Inputting trigger information is fairly straightforward as each trigger currently defines a scancode.
This scancode is then sent as a pressed scancode.
Next, the library is indicated it may process a single loop.
Before checking the result, the trigger cleanup must begin.
The trigger scancode is released, as to simulate an extremely quick press/release on a keyboard.

Validating :microscope: the result is a bit trickier as results are actually KLL capabilities (i.e. C functions).
Some of these functions, such as USB, will output a USB code that is easy to validate as a press/release event.
However, some capabilities trigger hardware that is not available to the shared library.
In this case a capability history buffer is maintained.
This history buffer is compared to what was expected, using the `kll.json` information.

While this is only a start, self-testing KLL should be working for all macros (sequence and combo) currently supported by the firmware.

Now, it’s possible to :tada: [self-test your own KLL files][controller-testin-selftest].
While this functionality is currently limited to compiling the firmware yourself, it will be added to the configurator as well in the future.
Not only does it give you an indication on which expressions are having issues, it also provides developers with more information on what the problem actually is (the trickiest part when reporting a bug is providing enough relevant and detailed information to actually solve the issue).

Really though, all this work was done in order to :door: prepare for state scheduling testing (also known as short/long press or tap keys).
State scheduling provides so many customization options and timing options that are just not possible to test reliably on a physical keyboard.
So we’re now one more step closer to achieving full KLL 0.5 support.

### Some useful reading

* [Keyboards][controller-keyboards]
* [Build Architecture][controller-buildarch]
* [Test Architecture][controller-testarch]
* [Tests][controller-tests]

If you’re curious as to what the output looks like, take a look at this [Travis-CI job][controller-testin-job].


## [Kira Status][kira]

We’re :construction: hard-at-work on both the next [prototype][prototype] case and pcb revisions (with big news in less than a week!).
Much of the work on the case has been figuring out how to injection mold the bottom foot.
The pcb has so many components on it that it has been tricky to place posts for screw holes.
This is extra tricky due to the hotswap pcb needing to be braced against the steel plate without having any switches inserted.

The pcb is our first :bridge_at_night: design using the [SAM4S][sam4s] so we’re using all the experience we gained designing the [K-Type][k-type] and [Type C WhiteFox][whitefox] to make the Kira even better.
Something that people tend to forget, is why old keyboards had bezels.
Keyboards used to have big bezels because you could place your keyboard controller chips in those areas.
It was a simpler time then.
But now, with our :bullettrain_front: sleek and streamlined keyboards, with no arrow cluster or spaced function row, there are very few places to put components on the pcb that won't interfere with the keyboard switches.
Fortunately, there’s a lot of room under the spacebar and a bit near the shift keys.

One cool feature of the SAM4S is the :doughnut: built-in [bootloader][bootloader] [SAM-BA][sam-ba].
While we’ll still be using a custom [dfu][dfu] bootloader to handle layout flashing, this built-in bootloader means that we’ll no longer need an external tool to update to bootloader.
But don’t worry, you’ll have to fully open up the case and follow some special instructions (won’t be labeled) in order to activate the built-in bootloader.

<hr>


# Upcoming Projects

And to finish off, some things to look forward to :shaved_ice: in the coming months.

* [Lock LED][controller-hidled] animations (e.g. CapsLock animations).
* Linked animations (using animations as triggers).
* State Scheduling (e.g. short vs. long triggers; full KLL 0.5 support).
* Trigger isolation (map special expressions that override others so you don’t get multiple key presses, e.g. Ctrl+A macro that overrides A and doesn’t send it).
* [HID-IO][hidio], will be the topic of a future update.

<hr>


# Final Notes

And that’s it for this update!
We're going to try and put out at least one update ever 1-2 months (though maybe not quite this long :sleeping:).



[x86]: https://en.wikipedia.org/wiki/X86
[dfu]: https://en.wikipedia.org/wiki/USB#Device_Firmware_Upgrade
[kira]: https://kono.store/products/kira-mechanical-keyboard
[prototype]: https://en.wikipedia.org/wiki/Prototype
[thread-safe]: https://en.wikipedia.org/wiki/Thread_safety
[host-side-kll]: https://github.com/kiibohd/controller/tree/master/Scan/TestIn
[json]: https://www.json.org/
[arm]: https://en.wikipedia.org/wiki/ARM_architecture
[cortex-m4]: https://developer.arm.com/products/processors/cortex-m/cortex-m4
[avr]: https://en.wikipedia.org/wiki/Atmel_AVR
[atmel]: https://en.wikipedia.org/wiki/Atmel
[microchip]: https://www.microchip.com/
[k20]: https://www.nxp.com/products/processors-and-microcontrollers/arm-based-processors-and-mcus/kinetis-cortex-m-mcus/k-seriesperformancem4/k2x-usb:K20_USB_MCU
[freescale]: https://en.wikipedia.org/wiki/Freescale_Semiconductor
[nxp]: https://www.nxp.com/
[cpu-frequency]: https://en.wikipedia.org/wiki/Clock_rate
[flash]: https://en.wikipedia.org/wiki/Flash_memory
[sram]: https://en.wikipedia.org/wiki/Static_random-access_memory
[off-by-one]: https://en.wikipedia.org/wiki/Off-by-one_error
[cli-debugging]: https://github.com/kiibohd/controller/wiki/Debugging
[threads]: https://en.wikipedia.org/wiki/Multithreading_(computer_architecture)
[chinese-lunar-new-year]: https://en.wikipedia.org/wiki/Chinese_New_Year
[sam-ba]: http://www.microchip.com/DevelopmentTools/ProductDetails.aspx?PartNO=Atmel%20SAM-BA%20In-system%20Programmer
[sam4s]: http://www.microchip.com/design-centers/32-bit/sam-32-bit-mcus/sam-4s-mcus
[problem-with-mechanical-switch-reviews]: https://input.club/the-problem-with-mechanical-switch-reviews/
[pcb-layout]: https://en.wikipedia.org/wiki/Printed_circuit_board
[schematic]: https://en.wikipedia.org/wiki/Schematic_capture
[gerbv]: http://gerbv.geda-project.org/
[bootloader]: https://wiki.openwrt.org/doc/techref/bootloader
[pcb]: https://learn.sparkfun.com/tutorials/pcb-basics
[gerbers]: https://en.wikipedia.org/wiki/Gerber_format
[pcb-git]: https://github.com/kiibohd/pcb
[dfu-util-git]: https://github.com/kiibohd/dfu-util
[travis-ci-dfu-util]: https://travis-ci.org/kiibohd/dfu-util
[dfu-util]: http://dfu-util.sourceforge.net/
[kii-dfu-git]: https://github.com/kiibohd/kii-dfu
[qt5]: http://doc.qt.io/qt-5/qt5-intro.html
[manufacturing-git]: https://github.com/kiibohd/manufacturing
[programmer-git]: https://github.com/kiibohd/programmer
[discord]: https://discord.gg/9tpgDGS
[mk20dx256vlh7]: https://www.nxp.com/part/MK20DX256VLH7
[kinetis]: https://www.nxp.com/products/processors-and-microcontrollers/arm-based-processors-and-mcus/kinetis-cortex-m-mcus:KINETIS
[ruby]: http://www.ruby-lang.org/
[buspirate]: http://dangerousprototypes.com/docs/Bus_Pirate
[jtag]: https://wiki.segger.com/index.php?title=JTAG
[swd]: https://wiki.segger.com/index.php?title=SWD
[openocd-upstream]: https://github.com/ntfreak/openocd
[openocd-git]: https://github.com/kiibohd/openocd
[force-git]: https://github.com/kiibohd/force
[lgplv3]: https://www.gnu.org/licenses/lgpl-3.0.en.html
[devcon]: https://github.com/kiibohd/kiidrv/tree/master/devcon
[controller-testin-selftest]: https://github.com/kiibohd/controller/tree/master/Keyboards#self-testing-a-kll-layout
[controller-testin-job]: https://travis-ci.org/kiibohd/controller/jobs/343725717#L2364
[controller-tests]: https://github.com/kiibohd/controller/tree/master/Scan/TestIn/Tests
[controller-testarch]: https://github.com/kiibohd/controller/blob/master/Documentation/TestArchitecture.md
[controller-buildarch]: https://github.com/kiibohd/controller/blob/master/Documentation/BuildArchitecture.md
[controller-keyboards]: https://github.com/kiibohd/controller/tree/master/Keyboards
[controller-hidled]: https://github.com/kiibohd/controller/issues/230
[hidio]: https://github.com/hid-io/hid-io
[appveyor-configurator]: https://ci.appveyor.com/project/kiibohd/configurator/branch/master
[appveyor-controller]: https://ci.appveyor.com/project/kiibohd/controller/branch/master
[appveyor-kiidrv]: https://ci.appveyor.com/project/kiibohd/kiidrv
[bash]: https://en.wikipedia.org/wiki/Bash_(Unix_shell)
[baud]: https://en.wikipedia.org/wiki/Baud
[bossa-license]: https://github.com/kiibohd/BOSSA/blob/master/LICENSE
[bossa-upstream]: https://github.com/shumatech/BOSSA/pull/67
[bossa]: https://github.com/kiibohd/BOSSA
[c++-prog]: https://en.wikipedia.org/wiki/C%2B%2B
[c-prog]: https://en.wikipedia.org/wiki/C_(programming_language)
[case-git]: https://github.com/kiibohd/case
[cern-ohl-v1.2]: https://www.ohwr.org/licenses/cern-ohl/license_versions/v1.2
[clojure]: https://clojure.org/
[cmake]: https://cmake.org/
[configurator-git]: https://github.com/kiibohd/configurator
[configurator-releases]: https://github.com/kiibohd/configurator/releases
[configurator-youtube]: https://www.youtube.com/watch?v=4uQ4NRtGgAE
[controller-contributors]: https://github.com/kiibohd/controller/graphs/contributors
[controller-git]: https://github.com/kiibohd/controller
[cygwin]: https://www.cygwin.com/
[deskthority-ibm-parak]: https://deskthority.net/photos-f62/ibm-6019303-t8502.html
[dfj-controller]: https://geekhack.org/index.php?topic=21459.0
[dfj]: https://geekhack.org/index.php?action=profile;u=4346
[docker-project]: https://www.docker.com/
[dph-gitorious]: https://gitorious.org/ibm-capsense-pcb/ibm-capsense-pcb.git/
[dph-pcb]: https://github.com/kiibohd/pcb/tree/master/DPH
[dsl]: https://en.wikipedia.org/wiki/Domain-specific_language
[ebay]: https://www.ebay.com/
[firmware]: https://en.wikipedia.org/wiki/Firmware
[flickr-haata]: https://www.flickr.com/photos/triplehaata/collections/72157635417889224/
[freecad]: https://www.freecadweb.org/
[funcparserlib]: https://github.com/vlasovskikh/funcparserlib
[gh-irc]: https://kiwiirc.com/client/irc.freenode.net/#geekhack
[gh]: https://geekhack.org/
[github-haata]: https://github.com/haata
[github-jbondeson]: https://github.com/jbondeson
[github-kiibohd]: https://github.com/kiibohd
[github-overkill]: https://github.com/OvahKeel
[github-parak]: https://github.com/parak
[github-smasher]: https://github.com/smasher816
[gitorious]: https://en.wikipedia.org/wiki/Gitorious
[gplv3]: https://www.gnu.org/licenses/gpl-3.0.en.html
[hako-kono]: https://kono.store/products/hako-mechanical-switches
[hako-true]: https://input.club/the-comparative-guide-to-mechanical-switches/tactile/hako-true/
[halo-true]: https://input.club/the-comparative-guide-to-mechanical-switches/tactile/halo-true/
[hasu-gh]: https://geekhack.org/index.php?action=profile;u=3412
[hasu]: https://github.com/tmk
[ibm-service-manual]: http://bitsavers.org/pdf/ibm/3270/fe/S126-0029-0_3276_3278_Keyboard_Assembly_Parts_Catalog_Jan83.pdf
[infinity-60]: https://input.club/devices/infinity-keyboard/
[infinity-ergodox]: https://input.club/devices/infinity-ergodox/
[inputclub]: https://input.club
[ironcad]: http://www.ironcad.com/
[javascript]: https://www.javascript.com/
[k-type-100fps]: https://www.youtube.com/watch?v=UCVXgRHDaqY
[k-type]: https://input.club/k-type/
[keyboardio]: https://shop.keyboard.io/
[kicad]: http://kicad-pcb.org/
[kiibohd-docker]: https://github.com/kiibohd/controller/tree/master/Dockerfiles
[kiiconf-git]: https://github.com/kiibohd/KiiConf
[kiidrv-git]: https://github.com/kiibohd/kiidrv
[kll-contributions]: https://github.com/kiibohd/kll/graphs/contributors
[kll-emitters]: https://github.com/kiibohd/kll/tree/master/emitters
[kll-git]: https://github.com/kiibohd/kll
[kll-inputclub]: https://input.club/kll/
[kll-rewrite]: https://github.com/kiibohd/kll/commit/f610d0fb150de0d5ac795a84e8dd122b419e45cd
[kll-spec-0.3d]: https://github.com/kiibohd/kll-spec/releases/download/v0.3d/kll-spec-v0.3d.pdf
[kll-spec-0.5c]: https://github.com/kiibohd/kll-spec/releases/download/v0.5c/kll-spec-v0.5c.pdf
[kll-spec-git]: https://github.com/kiibohd/kll-spec
[kll-spec-release]: https://github.com/kiibohd/kll-spec/releases
[ktype-rgb]: https://twitter.com/InputClub/status/944319010199371776
[latex]: https://en.wikipedia.org/wiki/LaTeX
[libwdi]: https://github.com/pbatard/libwdi
[matt3o]: https://github.com/cubiq
[mchck-bootloader]: https://github.com/mchck/mchck/tree/master/bootloader
[mchck-schematic]: https://github.com/mchck/mchck/wiki/Schematic-and-layout
[mchck]: https://mchck.org/
[microcontroller]: https://en.wikipedia.org/wiki/Microcontroller
[php]: http://www.php.net/
[plotly-haata]: https://plot.ly/~haata
[polling-rate]: https://blog.codinghorror.com/mouse-dpi-and-usb-polling-rate/
[python]: https://www.python.org/
[qmk-contributors]: https://github.com/qmk/qmk_firmware/graphs/contributors
[qmk]: https://github.com/qmk/qmk_firmware
[soarer-converter]: https://geekhack.org/index.php?topic=17458.0
[soarer]: https://geekhack.org/index.php?action=profile;u=4274
[tcl]: https://en.wikipedia.org/wiki/Tcl
[teensy-2.0++]: https://www.pjrc.com/store/teensypp.html
[teensy-2.0]: https://www.pjrc.com/store/teensy.html
[teensy-3.0]: https://www.pjrc.com/store/teensy3.html
[tmk-contributors]: https://github.com/tmk/tmk_keyboard/graphs/contributors
[tmk]: https://github.com/tmk/tmk_keyboard
[travis-ci-configurator]: https://travis-ci.org/kiibohd/configurator
[travis-ci-controller]: https://travis-ci.org/kiibohd/controller
[travis-ci-kiiconf]: https://travis-ci.org/kiibohd/KiiConf
[travis-ci-kll-spec]: https://travis-ci.org/kiibohd/kll-spec
[travis-ci-kll]: https://travis-ci.org/kiibohd/kll
[web-configurator]: https://input.club/configurator/
[what-is-opensource]: https://opensource.com/resources/what-open-source
[whitefox]: https://input.club/whitefox/
[windows-linux]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
[xbnf]: http://www.csci.csusb.edu/dick/maths/intro_ebnf.html
[xwhatsit-controller]: https://geekhack.org/index.php?topic=58192
[zadig]: http://zadig.akeo.ie/

