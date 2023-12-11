---
title: "cuic"
summary: CUSP Urban Imaging Capture

tags:
- imaging
- c
- c++
- python

date: "2017-12-12T21:42:55-05:00"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: CUIC
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: Follow
  url: https://github.com/Mohitsharma44/cuic

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---

## Introduction
This project is aimed at developing a streamlined framework/pipeling for using
different cameras and their different SDKs (Software Development Kits) for
performing different operations on the cameras.

Most high performance SDKs provided by camera manufacturers is written
in C or sometimes in C++. The aim of this project is to use the different SDKs
that are in use at NYU CUSP and write a complete multi-threaded application
for performing the following tasks:

- Connecting to the camera(s).
- Changing the camera and image configurations programmatically (such as exposure,
gain, focus, framerate, etc).
- Capturing the image and buffering it to the RAM (tmpfs / ramfs).
- Having the "image-saving" be performed in a separate thread.
- Have fail-safe techniques to make sure that in rare occurences, if the camera
disconnects or the application crashes, it can come back automatically once.
the link to the camera is re-established (which may require physical intervention)
- Images be timestamped with high precision.
- Should be able to save 1 RAW (bayer GB8 or similar)
image every 10 seconds (at-least).
- System should be able to 'plug-in' to the existing parallel
[CUIP - Cusp Urban Image Processing Pipeline](https://sharmamohit.com/project/cuip) project


Performing these may get a little complicated in C, so writing a C++ (11 or higher)
Python wrapper (or a mix of both) is required.

## Current State
The CUIC project is currently hosted on [GitHub](https://github.com/Mohitsharma44/cuic)
and is being actively developed using two SDKs at the time of writing
Following are the SDK's currently in use:

| SDK       | Website                                                                                | Cameras Driven                |
|-----------|----------------------------------------------------------------------------------------|-------------------------------|
| Pleora    | https://supportcenter.pleora.com/s/article/eBUS-SDK-Software-and-Release-Notes-Dwnload | Baumer LXG-200C (x2)          |
| Teledyne  | https://www.teledynedalsa.com/imaging/support/downloads/package/132/                   | Teledyne Dalsa Genie TS-C4096 |
| CEmergent*| https://emergentvisiontec.com/products/esdk/                                           | Emergent HS12000C             |

*Another similar project [CEmergent](https://github.com/Mohitsharma44/CEmergent) is
hosted on Github as well which deals with a special SFP+ connectivity based
scientific camera.


## Working
### Using_Pleora
Using the pleora SDK is pretty straight-forward.
This module has libconfig as a dependency on top of having pleora SDK. This
is to assist in making the configuration file for the camera more readable
as it follows the generic json-like format.

Any configuration setting should be added to the `configuration.cfg` file and
must be placed at `/opt/pleora/ebus_sdk/Ubuntu-14.04-x86_64/share/samples/cuic/using_pleora/src/`*.
This is just a silly way of making sure you have installed pleora SDK.


When the module is started for the first time, it reads out the camera
settings from the camera's memory and dumps it to the file (whose name is
same as the camera's MAC address.


One of the other dependency for this project is [spdlog](https://github.com/gabime/spdlog)
which is used for multi-threaded logging (to console and to the file). By default
all the logs are written to `/var/log/cuic/cuicCapture` and gets backed-up daily
at midnight.


To transfer the images securely, we use lsyncd (live Syncing Daemon) which basically
monitors a particular directory (hardcoded as /mnt/ramdisk in the cpp code which is
basically a tmpfs of 1GB size) for new images and uses an existing `ssh` tunnel
to transfer those images using `rsync` to a remote target/ server.


**Utils**

To make sure the code keeps running and is resilient to crashes, we use supervisord,
a python process control system module for restarting the cuic module in case
of a crash, retry in case of network issues and number of times to retry starting
the cuic module in case there is a system issue. We also use `crontab` for starting
and stopping our processes (via supervisor) at certain times to take images.

The configuration for lsyncd and supervisord can be found in the [utils](https://github.com/Mohitsharma44/cuic/tree/master/using_pleora/utils) subdirectory

>- *cuic  is where you clone this repo
>-  Make sure you have write permissions in `/var/log/cuic/` for logging

### Using_Teledyne

Unlike Pleora SDK which can work with any camera manufacturer (as long as you buy
a license from them), teledyne SDK only works with the cameras that are manufactured
by Teledyne Dalsa. Moreover their support is primarily for Windows based Sapera SDK.
However, they do provide a .. what I would call a .. `partially documented` SDK
for linux distribution. So getting this thing up and running quite frankly took me
a bit of time. Their demo code infact refused to compile on my Ubuntu Linux 16.04
(running kernel 4.10) and required some modifications.


Anyway, the major plus of using this SDK is that it doesn't lock up the camera
after let's say a seg fault or a memory reference error. This is something that is
horrible with Pleora or CEmergent for that matter. Unlike the other SDKs, the teledyne
dalsa SDK releases the camera in case the code crashes and the camera can be
re-connected to the daemon in ~10-20 seconds (after the code that was using the
camera crashes). So thumbs up to those guys!!


The current version of the [README](https://github.com/Mohitsharma44/cuic/tree/master/using_teledyne/README.md)
file can be used to setup the system and get things up and running. One major thing
to remember is that this module uses [plog](https://github.com/SergiusTheBest/plog)
logging library (I just wanted to test this library's speed..
its good but does miss the logs at times when the logs are flowing at speed of ~1/sec)
Also, this module strictly uses CmakeLists files for compiling (for ease of portability)
so your project should follow this structure:

``` bash
- capture_code
  | - cpp file
  | - archdefs.mk
  | - corenv.h
  | - CMakeLists.txt
  [] - Makefile*
  | - cmake
    | - Modules
      | - ...
- common
  | - GevUtils.c
  | - SapExUtil.c
  | - SapExUtil.h
  | - SapX11Util.h
  | - X_Display_utils.c
  | - X_Display_utils.h
- plog
  | - <...>.h
  | - ...

```

A major difference between this module vs all the others is that
this one is a prototype for using AMQP (Advanced Messaging Queue Protocol)
to serve the RPC (Remote Procedure Call) requests over the network
so that the cameras can be interfaced with the
[UOController](https://github.com/Mohitsharma44/UOController) commandline tool (
and hopefully someday using chatbot or voice command)


**Installation**

This code also requires `boost` library, rabbitmq and `rabbitmq-c` (the C implementation
of the `rabbitmq`). The `boost` library needs to be installed manually with
`system` and `chrono` libraries. `rabbitmq-c` is installed by the `cmake` module

For more installation instructions, refer the [README](https://github.com/Mohitsharma44/cuic/blob/master/using_teledyne/README.md)
file


**Execution Examples**

To run the code:

- Clone the repo and create a `build` directory inside `using_teledyne`.
- `cd` into `build` and  run `cmake ..`
- If everything succeded, then run `make`
- Now, execute `./capture_demo/genicam_cpp_demo`

To send commands via rabbitmq broker:

- `cd` into `amqpcpp_example` and create a `build` directory.
- `cd` into the `build` and run `cmake ..`
- If everything succeded, then run `make`
- Now, execute `./rpc_client 5` (to take 5 images)

The rpc_client (well, the capture code actually) supports following commmand-line
arguments:

- 'a': To abort any function
- '?': To print help function / return help function
- 't': To see if your machine supports turbo-mode
- 'g': for capturing images forever at max speed (fps)
- 's': To stop acquiring images
- 'q': To quit
- '\<integer\>': To capture that many images at max speed (fps)
