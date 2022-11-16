# Introduction

A couple years back I really got into [Nintendo DS homebrew development](https://github.com/jdriselvato/NDS-Development). It was very easy to break into considering the SDKs had existed for nearly a decade and emulators were near perfection. I hadn't any interest in learning 3DS homebrew development yet because Nintendo console lifecycle wasn't over. 

Earlier this year Nintendo announced that it would be closing the eshop, it's app store, March 27, 2023. and as of August 29, 2022 no one can add funds to their account to purchase from the eshop. This also meant that the 3DS would soon stop getting updates and the Nintendo Switch will be their biggest focus. I can safely say to my moral standards the lifecycle has ended.

Last month I finally decided to hack my 3DS with custom firmware and with Outdoorsy Lab day, I am finally getting a chance to mess around with homebrew development on the system. This repo is write up of the research and progress I made onf the first Lab day (Nov 16th, 2022).

# Lab Day 1

## SDK installation process

I followed the instructions found here: https://devkitpro.org/wiki/Getting_Started

1. Ensured `xcode-select --install` was up to date
2. Used the pkg installer to install devkitPro pacman.
3. Use dkp-pacman to install the 3DS pacman `sudo dkp-pacman -S 3ds-dev`

To test that the SDK worked I found [this repo](https://github.com/devkitPro/3ds-examples) with 3DS examples.

I found a hello world app down in `Programming/3DS Homebrew/3ds-examples-master/graphics/printing/hello-world`, ran `make` and immediately received this error:

```
Johns-Computer:hello-world$ make
make[1]: *** ~/Programming/3DS: Is a directory.  Stop.
make: *** [all] Error 2
```

I knew it couldn't be easy. so went searching for where the install went wrong. After messing with path variables and other random ideas, I finally dug into the make file and couldn't find anything creating a random `3DS directory`. Turns out the problem is my file path has a space in it `Programming/**3DS Homebrew**/3ds-examples-master/`

So `mv "3DS Homebrew"/ 3DS_Homebrew`

and 

```
Johns-Computer:hello-world$ make
main.c
linking hello-world.elf
built ... hello-world.smdh
built ... hello-world.3dsx
```

SDK and test compiling done. phew.

### Emulating the 3DS

Now we compiled the code and made a couple of files. After looking what each one was here's a breakdown:

```
[appname].3dsx: The executable.
[appname].smdh: The icon/metadata.
```

Which meant we needed an 3DS emulator to test the executable. I could probably test it on console at this point but the moving of files between SD cards and booting the system and installing will make for a terribly slow testing process. 

The most popular 3DS emulator is [Citra](https://citra-emu.org) 

> Notice: Citra does NOT support Macs with M1 chipsets. Our Mac builds may run through Rosetta, but you WILL encounter various issues that we won't provide support for. We may eventually support M1 Macs, but not at this time.

Fortunately, I'm still running a 2017 Intel MacBook Pro but that isn't enough. Cause trying to load our hello world, I get this error:

```
Your GPU may not support OpenGL 4.3, or you do not have the latest graphics driver.
```

Turns out MacOS has support for really outdated OpenGL and latest Citra has drop compatability until further notice. The forums recommend downloading this build instead: https://github.com/citra-emu/citra-nightly/releases/tag/nightly-1782


Emulation is working on nightly-1782, nice hello world:

![hello world](./images/helloworld.png)

## The project

Since this is a 3DS and all, there are 3 goals I want to accomplish on this lab day

1. Using the touch screen + keyboard to type into an input box
2. Using the Networking code to speak to an API
3. Display API results.

Naturally, since this is an Outdoorsy Lab day, let's talk to our public search API by Keyword (which just happens to the same requirements for the iOS interview code test). I wish we could easily show images but because this is a video game console that expects sprite sheets in the form of .t3x or .bin, this app will have to be text based only.






## SDK Documentation

coming soon

# Resources

- Introduction link: https://xem.github.io/3DShomebrew/
- Installing the SDK: hhttps://devkitpro.org/wiki/Getting_Started
