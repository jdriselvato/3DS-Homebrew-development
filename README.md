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

Which meant we needed an 3DS emulator to test the executable.

## SDK Documentation

coming soon

# Resources

- Introduction link: https://xem.github.io/3DShomebrew/
- Installing the SDK: hhttps://devkitpro.org/wiki/Getting_Started
