# CTRE

Cross The Road Electronics (CTRE) provides FRC-focused motor controllers and sensors with advanced on-controller features. Their Phoenix framework integrates tightly with WPILib/RobotPy and the CAN bus ecosystem.

## System Architecture

```mermaid
graph TD
    A[RoboRIO] --> B[CAN Bus]
    B --> C[Talon FX (Falcon 500)]
    B --> D[Talon SRX]
    B --> E[Victor SPX]
    B --> F[CANcoder]
    
    A --> G[PWM]
    A --> H[DIO]
    A --> I[Analog]
    
    subgraph Optional
      J[CANivore CAN FD]
    end

    J -. USB .- A
    J --> B

    C --> C1[Onboard PID]
    C --> C2[Motion Magic]
    F --> F1[Absolute Position]
    
    style J fill:#ff5722
    style C fill:#4caf50
```

## Phoenix Tools
- Phoenix Tuner: device configuration, firmware, diagnostics
- Signal logging: capture telemetry for tuning
- Self-test snapshot: quick device health check

## Common Devices
- [Talon FX](./talonfx.md): integrated encoder, onboard control, Motion Magic
- [CANivore](./canivore.md): secondary CAN FD network for high-bandwidth systems
- CANcoder: absolute encoder for mechanisms (see ctre/cancoder.md)

## Integration Tips
- Use consistent CAN IDs and naming in Tuner
- Prefer on-controller control (PID/Motion Magic) to reduce loop latency
- If bus utilization is high, consider moving high-rate devices to CANivore

{{#authors lmaxwell24}}
