# Ultraleap OpenXR Hand Tracking API Layer

An implementation of the OpenXR `XR_EXT_hand_tracking` extension.

This library is implemented as a OpenXR API layer named `XR_APILAYER_ULTRALEAP_hand_tracking`, which adds:
- `XR_EXT_hand_tracking`
- `XR_EXT_hand_joints_motion_range`
support to an existing OpenXR runtime which may or may not already support it. If an existing
runtime already supports `XR_EXT_hand_tracking`, this API layer takes precedence and overrides it.

This API layer supports any Ultraleap or Leap Motion tracking devices supported by the existing
[Ultraleap Tracking Software](https://developer.leapmotion.com/tracking-software-download), such as the
[Leap Motion Controller](https://www.ultraleap.com/product/leap-motion-controller/) or the
[Ultraleap Stereo IR 170](https://www.ultraleap.com/product/stereo-ir-170/).

This API layer is an *implicit* API layer, and as-such, it requires **no** modification to an application to enable
support. Any application which uses the `XR_EXT_hand_tracking` or any of the other above extensions will be able to use
this layer with no modification.

## Requirements

### OpenXR Runtime

You will require an OpenXR runtime to be installed to use this API layer. The correct runtime will depend on your
platform and XR hardware, some of the most common platforms are listed below:

#### Windows

* [Microsoft Windows Mixed Reality](https://docs.microsoft.com/en-us/windows/mixed-reality/openxr-getting-started)
* [Valve SteamVR](https://store.steampowered.com/newshub/app/250820/view/2396425843528787269)
* [Oculus OpenXR](https://developer.oculus.com/documentation/native/pc/dg-openxr/)

#### Required OpenXR Extensions

Your OpenXR runtime is required to support the `XR_KHR_win32_convert_performance_counter_time` (Windows) or
`XR_KHR_convert_timespec_time` (Unix) extensions. All major runtimes (including those listed above) support these.

### Ultraleap Software

You will require the current [Ultraleap Tracking Software](https://developer.leapmotion.com/tracking-software-download)
to be installed to run any applications that use this API layer with OpenXR.

## Downloading

The latest version of this API layer can be installed from the
[Releases](https://github.com/ultraleap/OpenXRHandTracking/releases) page.

## Windows Installation & Setup

### Installing

Once downloaded run the EXE installer to installer the API layer.

You can verify that the installation has been successfully completed by installing the
[Microsoft Mixed Reality OpenXR Developer Tools App](https://www.microsoft.com/store/productId/9n5cvvl23qbt) from the
Microsoft Store. Once this is opened, navigate to the "System Status" tab, and you should see `XR_EXT_hand_tracking`
listed in the Extensions section, and `XR_APILAYER_ULTRALEAP_hand_tracking` listed under the API Layers section.

This method of verification has only been confirmed with the Windows Mixed Reality OpenXR runtime, but should work with
others as well.

### Setup

The API layer will report hand-tracking as supported when this API layer is installed. To be able to actively use the
hand tracking the following must all be true:

- Leap Motion v5 Software installed and running
- Ultraleap hand-tracking device attached and operating correctly
- User's hands visible to the Ultraleap hand-tracking device.

### Configuration

#### Mounting, Position & Tilt

The Ultraleap tracking device should be mounted on the front of your HMD in a suitable position, via a secure mounting
method such as the [Ultraleap VR Developer Mount](https://www.ultraleap.com/product/vr-developer-mount/).

The position of the Ultraleap tracking device, relative to your view position can be configured using the following
environment variables (position relative to the interpupillary line).

![Ultraleap Mounting Diagram](https://developer.leapmotion.com/documentation/v4/HMD_Mounting.png)

These environment variables must be set prior to the OpenXR application starting, if they are left unset, the default
values (in brackets) are used:

- `ULTRALEAP_OPENXR_POS_X` - Position in X in meters (default: 0.0m)
- `ULTRALEAP_OPENXR_POS_Y` - Position in Y in meters (default: 0.0m)
- `ULTRALEAP_OPENXR_POS_Z` - Position in Z in meters (default: -0.08m/-8cm)
- `ULTRALEAP_OPENXR_TILT_ANGLE` - Tilt angle downwards in degrees from the forward facing horizontal (default 0)

#### Logging

The layer will log to `%PROGRAMDATA%\Ultraleap\OpenXR\UltraleapOpenXR.log` with errors and warnings generated during
application usage of OpenXR. The logging location, and level can be controlled by the following environment variables:

- `ULTRALEAP_OPENXR_LOG_LEVEL` - The logging level, supported levels are `all`, `debug`, `info`, `warn`, and `error`
  (default: "warn")

#### Disabling the API layer

If you wish to disable the API layer, this can be achieved by defining the
`DISABLE_XR_APILAYER_ULTRALEAP_HAND_TRACKING_1` environment variable to any value.

## Uninstalling

Uninstallation can be performed from the Windows "Add or Remove Programs" area of the system settings.

## Known issues

Known issues in this release, as well as previously fixed issues are tracked in `CHANGELOG.md` included with this
release.

## Reporting issues

If you encounter an issue with this release, please report it as an issue on our
[GitHub project](https://github.com/ultraleap/OpenXRHandTracking/issues).

## Licensing

This project is licensed under the terms in `LICENSE.md` included with this release.
