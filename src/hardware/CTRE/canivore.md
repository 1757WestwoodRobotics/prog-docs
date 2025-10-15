# CANivore

The CANivore is a USB-to-CAN-FD adapter that adds a second, high-bandwidth CAN network to your robot. Typical use cases include swerve drive modules, high-rate sensor networks, and offloading bandwidth from the RoboRIO CAN bus.

## Why CANivore
- Increased bandwidth (CAN FD) for high-frequency control loops
- Isolate critical devices from main bus traffic
- Improved robustness via bus segmentation

## Wiring and Naming
- Connect CANivore via USB to the RoboRIO
- Daisy-chain CAN FD devices to the CANivore port
- Name the CANivore in Phoenix Tuner (e.g., "canivore") and use that name in code

## Usage in RobotPy

```python
import ctre

# The name must match Phoenix Tuner device name for the CANivore
CANIVORE_BUS_NAME = "canivore"

# Device on the CANivore bus
talon_on_canivore = ctre.WPI_TalonFX(1, canbus=CANIVORE_BUS_NAME)

# Device on the default RoboRIO CAN bus
talon_on_rio = ctre.WPI_TalonFX(2)  # No canbus specified
```

## Diagnostics
- Use Phoenix Tuner to verify device presence on the CANivore bus
- Check bus utilization and error counters
- Keep firmware versions consistent across all CTRE devices

{{#authors lmaxwell24}}
