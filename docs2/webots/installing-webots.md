# Installing Webots

This chapter explains how to install Webots.

## Sections

- [System requirements](system-requirements.md)
- [Verifying your graphics driver installation](verifying-your-graphics-driver-installation.md)
- [Installation procedure](installation-procedure.md)

## System Requirements

The following hardware is required to run Webots:

- A fairly recent PC or Mac computer with at least a 2 GHz dual core CPU clock speed and 2 GB of RAM is a minimum requirement.
  A quad-core CPU is however recommended.
- An NVIDIA or AMD OpenGL (minimum version 3.3) capable graphics adapter with at least 512 MB of RAM is required.
  We do not recommend any other graphics adapters, including Intel graphics adapters, as they often lack a good OpenGL support which may cause 3D rendering problems and application crashes.
  Nevertheless, in some cases, the installation of the latest Intel graphics driver can fix such problems and let you use Webots.
  However, we don't provide any guarantee on this.
  For Linux systems, we recommend only NVIDIA graphics cards.
  Webots works well on all the graphics cards included in fairly recent Apple computers.

The following operating systems are supported:

- Linux: Webots is ensured to run on the latest Ubuntu Long Term Support (LTS) releases, including versions 22.04 and 20.04.
  But it is also known to run on most recent major Linux distributions, including RedHat, Mandrake, Debian, Gentoo, Arch, SuSE, and Slackware.
  We recommend using a recent version of Linux.
  Webots is provided for Linux 64 (x86-64) systems only.
  Webots doesn't run on Ubuntu versions earlier than 20.04.
- Windows: Webots runs on Windows 11 and Windows 10 (64-bit versions only).
- Mac: Webots runs on macOS 11 "Big Sur", macOS 12 "Monterey" and macOS 13 "Ventura".

Webots may work but is not officially supported on earlier versions of the above mentioned operating systems.

Other versions of Webots for other UNIX systems may be available upon request.

## Verifying your Graphics Driver Installation

### Supported Graphics Cards

Webots officially supports only recent NVIDIA and AMD graphics adapters.
So it is recommended to run Webots on computers equipped with such graphics adapters and up-to-date drivers provided by the card manufacturer (i.e., NVIDIA or AMD).
Such drivers are often bundled with the operating system (Windows, Linux and Mac OS X), but in some cases, it may be necessary to fetch it from the website of the card manufacturer.

### Unsupported Graphics Cards

Webots may nevertheless work with other graphics adapters, in particular the Intel graphics adapters.
However, this is unsupported and may or may not work, without any guarantee.
Some users reported success with some Intel graphics cards after installing the latest version of the driver.
Graphics drivers from Intel may be obtained from the [Intel download center website](http://downloadcenter.intel.com).
Linux graphics drivers from Intel may be obtained from the [Intel Linux Graphics website](http://intellinuxgraphics.org).
If some graphical bugs subsist, changing the "RTT preferred mode" from the Webots OpenGL Preferences from "Framebuffer Object" to "Pixelbuffer Object" or "Direct Copy" may fix the problems.
However, this may also impact the 3D performance.

### Upgrading your Graphics Driver

On Linux and Windows, you should make sure that the latest graphics driver is installed.
On the Mac, the latest graphics drivers are automatically installed by the *Software Update*, so Mac users are not concerned by this section.
Note that Webots can run up to 10x slower without the appropriate driver.
Updating your driver may also solve various problems, i.e., odd graphics rendering or Webots crashes.

#### Upgrading the GPU Driver on Linux

On Linux, use this command to check if a hardware accelerated driver is installed:

```sh
glxinfo | grep OpenGL
```

If the output contains the string "NVIDIA", "AMD", or "Intel", this indicates that a hardware driver is currently installed:

```sh
$ glxinfo | grep OpenGL
OpenGL vendor string: NVIDIA Corporation
OpenGL renderer string: GeForce 8500 GT/PCI/SSE2
OpenGL version string: 3.0.0 NVIDIA 180.44
...
```

If you read "Mesa", "Software Rasterizer" or "GDI Generic", this indicates that the hardware driver is currently not installed and that your computer is currently using a slow software emulation of OpenGL:

```sh
$ glxinfo | grep OpenGL
OpenGL vendor string: Mesa project: www.mesa3d.org
OpenGL renderer string: Mesa GLX Indirect
OpenGL version string: 1.4 (1.5 Mesa 6.5.2)
...
```

In this case you should definitely install the hardware driver.

On Ubuntu the driver can usually be installed automatically from the `Additional Drivers` tab of the `Software & Update` window.
Otherwise you can find out what graphics hardware is installed on your computer by using this command:

```sh
$ lspci | grep VGA
01:00.0 VGA compatible controller: nVidia Corporation GeForce 8500 GT (rev a1)
```

Then you can normally download the appropriate driver from the graphics hardware manufacturer's website: [http://www.nvidia.com](http://www.nvidia.com) for an NVIDIA card or [http://www.amd.com](http://www.amd.com) for a AMD graphics card.
Please follow the manufacturer's instructions for the installation.

### Hardware Acceleration Tips

#### Linux: Disable Desktop Effects

Depending on the graphics hardware, there may be a huge performance drop of the rendering system (up to 10x) when *compiz* desktop effects are on.
Also these visual effects may cause some display bug where the main window of Webots is not properly refreshed.
Hence, on Ubuntu (or other Linux) we recommend to deactivate the desktop effects.
You can easily disable them using some tools like *Compiz Config Settings Manager* or *Unity Tweak Tool*.
