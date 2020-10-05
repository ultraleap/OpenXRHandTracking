# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## 1.0.0-beta2
### Fixed

 - Fixed support for UWP/AppContainer applications, including WebXR, when used in conjunction with the
   [Ultraleap 4.1 Tracking SDK](https://developer-archive.leapmotion.com/downloads/external/v4-1-hand-tracking/windows?version=4.1.0).
   [Issue #8](https://github.com/ultraleap/OpenXRHandTracking/issues/8)

### Added

 - The uninstaller is included with the install as `UninstallOpenXR.cmd` to allow easy uninstallation. An entry is also
   added to Windows add/remove programs list.
 - The License, Readme, Changelog and version information are all now included in an install for easy reference.
 - Added log file output (to complement existing `XR_EXT_debug_utils` support) only warnings and errors are logged by
   default, but this can be controlled with the `ULTRALEAP_OPENXR_DEBUG` environment variable.
 - Clarified in the Readme that this is an implicit OpenXR api layer, and does not need explicitly enabling.

### Changed

 - Removed SteamVR <1.14 specific workaround for `xrGetSystemProperties` extension support.
   [Issue #5](https://github.com/ultraleap/OpenXRHandTracking/issues/5)

## 1.0.0-beta1
### Added

 - Initial support for the `XR_EXT_hand_tracking` extension
 
### Known Issues

 - This API layer does not currently report the linear or angular velocity of the hands.
   If requested, the XrHandJointVelocitiesEXT structure will be returned with the validity bits unset.
   [Issue #1](https://github.com/ultraleap/OpenXRHandTracking/issues/1)

 - The underlying Ultraleap service currently return the same joint radius for all joints.
   [Issue #2](https://github.com/ultraleap/OpenXRHandTracking/issues/2)

 - `XrSystemHandTrackingPropertiesEXT.supportsHandTracking` will always return `XR_TRUE` when this API layer is enabled,
   regardless of if a device is connected. `XrHandJointLocationsEXT.isActive` indicates if hand-tracking information is
   currently available for the requested hand-tracker.
   [Issue #3](https://github.com/ultraleap/OpenXRHandTracking/issues/3)
   
 - The user's virtual hands may appear to move relative to the head when the head is moved quickly, even when the user's
   hands are remaining still. This is due to the temporal warping settings and the fact that the hand position and view
   position are updated at different rates.
   [Issue #6](https://github.com/ultraleap/OpenXRHandTracking/issues/6)

 - Unreal Engine 4.25 currently ships with version 1.0.0 of the OpenXR loader which has a
   [known issue](https://github.com/KhronosGroup/OpenXR-SDK-Source/pull/91) which prevents OpenXR API layers from
   functioning correctly. This will be resolved when Unreal Engine ships with a newer OpenXR loader, or the existing
   OpenXR loader DLLs are manually updated.
   [Issue #4](https://github.com/ultraleap/OpenXRHandTracking/issues/4)