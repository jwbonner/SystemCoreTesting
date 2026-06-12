# CTR-Electronics Phoenix 6

Please read through the requirements and basic example before utilizing the vendordep.

## Requirements

Due to the volatile nature of versions and breaking changes, the below list is provided to clarify compatible WPILib version, compatible Phoenix 6 API version and compatible firmware version.

### WPILib to Phoenix 6 API

- WPILib `2027_alpha5` compatible releases
  - Phoenix 6 `26.50.0-alpha-1`
- WPILib `2027_alpha1` and `2027_alpha2` compatible releases
  - Phoenix 6 `25.90.0-alpha-1`
  - Phoenix 6 `25.90.0-alpha-2`

### Phoenix 6 API to Firmware

- `26.50.0-alpha-1` compatible Phoenix 6 firmware
  - Firmware `26.X` (any 2026 firmware release)
- `25.90.0-alpha-1` and `25.90.0-alpha-2` compatible Phoenix 6 firmware
  - Firmware `25.90.0.0`

## Python Usage

It is highly recommended to explicitly pin the Python dependency in your `project.toml`.

```
requires = [
    "phoenix6==26.50.0a1"
]
```

## Basic Example

SystemCore CAN buses can be used by using the `CANBus.systemCore(int busId)` static function.

So to initialize a device on the SystemCore bus, you would use 

```java
// Use the CANivore named "swag"
public static final TalonFX m_motor = new TalonFX(0, new CANBus("swag"));

// Use the 5th (0-indexed) CAN bus
public static final TalonFX m_motor = new TalonFX(0, CANBus.systemCore(4));

// If no parameter is provided, it will use can_s0
public static final TalonFX m_motor = new TalonFX(0);
```

## Changelog

### 26.50.0-alpha-1

Changelog is available [here](https://api.ctr-electronics.com/changelog).

### 25.90.0-alpha-2

#### Changes

- **BREAKING**: Removed the device overload that takes a string parameter. Construct a `CANBus` object instead. This should improve clarity and reduce confusion.

#### Fixes

- Fixed Signal Logger auto-logging.
  - When auto logging is enabled, logging is started by any of the following (whichever occurs first):
    - The robot is enabled.
    - It has been at least 5 seconds since program startup (allowing for calls to `setPath`), and the Driver Station is connected to the robot.
  - After auto logging has started the log once, logging will not be automatically stopped or restarted by auto logging.

#### Known Issues

Please see [known issues](https://api.ctr-electronics.com/changelog#known-issues-20260613).
<hr/>

### 25.90.0-alpha-1

- Devices no longer implement sendable as it has been removed from WPILib.

#### Known Issues

- Phoenix 5 is unavailable.
- An offline installer is unavailable.
- Signal logger does not auto-start on FMS.
- Signal logger does not rename files to include the match name when connected to FMS.
- Tuner cannot deploy a temporary diagnostic server to the SystemCore. To use Phoenix Tuner X functionality, deploy a blank robot program with a Phoenix 6 device initialized. No other Tuner functionality is affected.

## Download

* Vendordep: Select from the vendor JSON repository in VS code

* canivore-usb-kernel Package: https://ctre.download/files/systemcore/canivore-usb-kernel_1.18_aarch64.ipk

* canivore-usb Package: https://ctre.download/files/systemcore/canivore-usb_1.16_aarch64.ipk