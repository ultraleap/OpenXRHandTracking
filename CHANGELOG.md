# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## 1.0.0-beta

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

 - There is a known issue with the SteamVR OpenXR runtime 1.13.9
   [not correctly honouring](https://steamcommunity.com/app/250820/discussions/8/2523653167130760453/)
   the `XrSystemHandTrackingProperties` as an extension to the `xrGetSystemProperties` call.
   This API layer includes a work-around that detects and corrects this behaviour.
   [Issue #5](https://github.com/ultraleap/OpenXRHandTracking/issues/5)