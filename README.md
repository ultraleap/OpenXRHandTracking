# Ultraleap OpenXR Hand Tracking API Layer

An implementation of the OpenXR `XR_EXT_hand_tracking` extension.

This library is implemented as a OpenXR API layer named `XR_APILAYER_ULTRALEAP_hand_tracking`, which adds
`XR_EXT_hand_tracking` support to an existing OpenXR runtime which may or may not already support it. If an existing
runtime already supports `XR_EXT_hand_tracking`, this API layer takes precedence and overrides it.

This API layer supports any Ultraleap or Leap Motion tracking devices supported by the existing
[Leap Motion v4 Software](https://developer-archive.leapmotion.com/downloads/external/v4-developer-beta/windows), such
as the [Leap Motion Controller](https://www.ultraleap.com/product/leap-motion-controller/).

## Requirements

### OpenXR Runtime

You will require an OpenXR runtime to be installed to use this API layer. The correct runtime will depend on your
platform and XR hardware, some of the most common platforms are listed below:

 * [Microsoft Windows Mixed Reality](https://docs.microsoft.com/en-us/windows/mixed-reality/openxr-getting-started)
 * [Valve SteamVR](https://store.steampowered.com/newshub/app/250820/view/2396425843528787269)
 * [Oculus OpenXR](https://developer.oculus.com/documentation/native/pc/dg-openxr/)
 
### Ultraleap Software

You will require the current
[Leap Motion v4 Software](https://developer-archive.leapmotion.com/downloads/external/v4-developer-beta/windows) to be
installed to run any applications that use this API layer with OpenXR.

## Downloading

The latest version of this API layer can be installed from the
[Releases](https://github.com/ultraleap/OpenXRHandTracking/releases) page.

## Installing

Once downloaded follow the following steps to install the API layer.

 - Extract the downloaded `.zip`
 - Right click the `Install.cmd` script and select "Run as administrator"
 - Type "Yes" at the prompts accept the license agreement and to start the installation
 - Wait for the installation to complete.
 
You can verify that the installation has been successfully completed by installing the
[Microsoft Mixed Reality OpenXR Developer Tools App](https://www.microsoft.com/store/productId/9n5cvvl23qbt) from the
Microsoft Store. Once this is opened, navigate to the "System Status" tab, and you should see `XR_EXT_hand_tracking`
listed in the Extensions section, and `XR_APILAYER_ULTRALEAP_hand_tracking` listed under the API Layers section.

This method of verification has only been confirmed with the Windows Mixed Reality OpenXR runtime, but should work with
others as well.
 
## Setup

The API layer will report hand-tracking as supported when this API layer is installed. To be able to actively use the
hand tracking the following must all be true:

 - Leap Motion v4 Software installed and running
 - Ultraleap hand-tracking device attached and operating correctly
 - User's hands visible to the Ultraleap hand-tracking device.

## Configuration

### Mounting, Position & Tilt

The Ultraleap tracking device should be mounted on the front of your HMD in a suitable position, via a secure mounting
method such as the [Ultraleap VR Developer Mount](https://www.ultraleap.com/product/vr-developer-mount/).

The position of the Ultraleap tracking device, relative to your view position can be configured using the following
environment variables (position relative to the interpupillary line).

![Leap Mounting Diagram](https://developer.leapmotion.com/documentation/v4/HMD_Mounting.png)

These environment variables must be set prior to the OpenXR application starting, if they are left unset,
the default values (in brackets) are used:

 - `ULTRALEAP_OPENXR_POS_X` - Position in X in meters (default: 0.0m)
 - `ULTRALEAP_OPENXR_POS_Y` - Position in Y in meters (default: 0.0m)
 - `ULTRALEAP_OPENXR_POS_Z` - Position in Z in meters (default: -0.08m/-8cm)
 - `ULTRALEAP_OPENXR_TILT_ANGLE` - Tilt angle downwards in degrees from the forward facing horizontal (default 0)
 
### Temporal Warping

The position of the hands in the scene is interpolated to compensate for differences between the captured hand-tracking
frame and the update time of the user's view. This is controlled by two variables:

 - `ULTRALEAP_OPENXR_TIME_WARP_HAND` - +/- timestamp offset in milliseconds for the hand position (default: +10ms)
 - `ULTRALEAP_OPENXR_TIME_WARP_VIEW` - +/- timestamp offset in milliseconds for the view position (default: -25ms)
 
These parameters can be different for each different headset runtime and can be tuned appropriately. These can help
stabilise the hand-position in space if the view position is moved rapidly.
 
## Disabling the API layer

If you wish to disable the API layer, this can be achieved by defining the
`DISABLE_XR_APILAYER_ULTRALEAP_HAND_TRACKING_1` environment variable to any value.

## Uninstalling

You can remove the API layer by right clicking the included `Uninstall.cmd` script and selecting "Run as administrator".
This will remove the installed files and registry keys.

## Known issues

Known issues in this release, as well as previously fixed issues are tracked in `CHANGELOG.md` included with this
release.

## Reporting issues

If you encounter an issue with this release, please report it as an issue on our
[GitHub project](https://github.com/ultraleap/OpenXRHandTracking/issues).

## Licensing

This project is licensed under the terms in `LICENSE.md` included with this release.
