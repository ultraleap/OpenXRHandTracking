# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres
to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2022-04-01

### Added

- Support for Qualcomm XR2 based Android systems.

### Changed

- `isTrackingSupported` is now reported based on if the Ultraleap Tracking Service is installed and running on the
  system, as opposed to attempting a connection to the service to avoid startup delay and possible timeouts.

### Fixed

- Fixed an issue which could cause a hang when hand-trackers were created and destroyed very rapidly, such as
  during the `XR_EXT_hand_tracking` conformance test.
- Fixed an issue where permissions were not always correctly set on the logs directory during installation.

### Known Issues

- This API layer does not currently report the linear or angular velocity of the hand joints other than the palm. If
  requested, the XrHandJointVelocitiesEXT structure will be returned with the validity bits unset.
  [Issue #1](https://github.com/ultraleap/OpenXRHandTracking/issues/1)

- The underlying Ultraleap service currently return the same joint radius for all joints.
  [Issue #2](https://github.com/ultraleap/OpenXRHandTracking/issues/2)


## [1.0.1] - 2021-12-17

## Changed

- Updated Ultraleap tracking client to v5.3.0.
- Increase timeout on initial tracking service connection, to increase tolerance to slower tracking server response.

### Fixed

- Fixed an issue which could cause a hang when all created hand-trackers were destroyed.
- Fixed an issue with error handling that could cause tracking to stop working if the first tracking event was an error.

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


## [1.0.0] - 2021-11-11

### Fixed

- The API layer will now disable its function intercepts if the `XR_EXT_hand_tracking` extension is not requested by the application [Issue #14](https://github.com/ultraleap/OpenXRHandTracking/issues/14).
- Fixed issue causing non-conformance when running [OpenXR Conformance Test Suite](https://github.com/KhronosGroup/OpenXR-CTS).

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


## [1.0.0-beta.4] - 2021-10-27

### Fixed

- Fixed issue with API layer initialisation when more than one API layer is enabled. This would result in a crash if
  this API layer was enabled first.
- Fixed issue with reporting the layer's API layer version information.


## [1.0.0-beta.3] - 2021-10-27

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


## [1.0.0-beta.2] - 2020-10-07

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
  [Ultraleap 4.1 Tracking SDK](https://developer-archive.leapmotion.com/downloads/external/v4-1-hand-tracking/windows?version=4.1.0).
  [Issue #8](https://github.com/ultraleap/OpenXRHandTracking/issues/8)


## [1.0.0-beta.1] - 2020-07-09

### Added

- Initial support for the `XR_EXT_hand_tracking` extension

[1.1.0]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.1.0
[1.0.1]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.1
[1.0.0]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.0
[1.0.0-beta.4]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.0-beta.4
[1.0.0-beta.3]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.0-beta.3
[1.0.0-beta.2]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.0-beta2
[1.0.0-beta.1]: https://github.com/ultraleap/OpenXRHandTracking/releases/tag/1.0.0-beta
