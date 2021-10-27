# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres
to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## 1.0.0-beta.4

### Fixed

- Fixed issue with API layer initialisation when more than one API layer is enabled. This would result in a crash if
  this API layer was enabled first.
- Fixed issue with reporting the layer's API layer version information.

## 1.0.0-beta.3

### Added

- Signed Windows installer to replace the previous PowerShell based installer. Installation will remove previous 
  versions of the API Layer.
- Added support for the `XR_EXT_hand_joints_motion_range` extension. Since Ultraleap hand-trackers are optical-based
  systems, the returned hand pose is always based on the unobstructed joint locations.
- Added support for the linear velocity reporting of the palm joint (`XR_HAND_JOINT_PALM_EXT`).

### Changed

- Updated Ultraleap tracking client to v5.2.0.
- Updated OpenXR SDK to v1.0.20.
- OpenXR API layer DLL is now signed.
- Use `XR_KHR_win32_convert_performance_counter_time` or `XR_KHR_convert_timespec_time` extensions for accurate internal
  timestamp conversions.
- Removed configurations variables `ULTRALEAP_OPENXR_TIME_WARP_HEAD` and `ULTRALEAP_OPENXR_TIME_WARP_VIEW` as they are
  no longer required now that [Issue #6](https://github.com/ultraleap/OpenXRHandTracking/issues/6) is resolved.
- Removed 32-bit support as the Ultraleap tracking client v5 doesn't currently have support for Windows 32-bit.

### Fixed

- Correct wrist position (was incorrectly reporting the elbow position as the wrist position).
  [Issue #10](https://github.com/ultraleap/OpenXRHandTracking/issues/10)
- Fixed temporal warping so that the user's hands no longer move when held static and the user's head is rapidly
  moved. [Issue #6](https://github.com/ultraleap/OpenXRHandTracking/issues/6)

## 1.0.0-beta.2

### Added

- The uninstaller is included with the install as `UninstallOpenXR.cmd` to allow easy uninstallation. An entry is also
  added to Windows add/remove programs list.
- The License, Readme, Changelog and version information are all now included in an installation for easy reference.
- Added log file output (to complement existing `XR_EXT_debug_utils` support) only warnings and errors are logged by
  default, but this can be controlled with the `ULTRALEAP_OPENXR_DEBUG` environment variable.
- Clarified in the Readme that this is an implicit OpenXR api layer, and does not need explicitly enabling.

### Changed

- Removed SteamVR <1.14 specific workaround for `xrGetSystemProperties` extension support.
  [Issue #5](https://github.com/ultraleap/OpenXRHandTracking/issues/5)

### Fixed

- Fixed support for UWP/AppContainer applications, including WebXR, when used in conjunction with the
  [Ultraleap 4.1 Tracking SDK](https://developer-archive.leapmotion.com/downloads/external/v4-1-hand-tracking/windows?version=4.1.0)
  .
  [Issue #8](https://github.com/ultraleap/OpenXRHandTracking/issues/8)

## 1.0.0-beta.1

### Added

- Initial support for the `XR_EXT_hand_tracking` extension

### Known Issues

- This API layer does not currently report the linear or angular velocity of the hand joints other than the palm. If
  requested, the XrHandJointVelocitiesEXT structure will be returned with the validity bits unset.
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
