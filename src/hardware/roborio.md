# RoboRIO

The RoboRIO is the central control computer for FRC robots. It runs your RobotPy code, interfaces with hardware, and connects to the field network.

## I/O and Buses

```mermaid
graph TD
    A[RoboRIO] --> B[CAN]
    A --> C[PWM]
    A --> D[DIO]
    A --> E[Analog]
    A --> F[USB]
    A --> G[Ethernet]

    B --> B1[Motor Controllers]
    B --> B2[Sensors]
    C --> C1[Servos]
    D --> D1[Limit Switches]
    D --> D2[Quadrature Encoders]
    E --> E1[Pressure Sensor]
    F --> F1[Cameras]
    G --> G1[Radio]
```

## Deployment and Runtime
- Code entry point: `robot.py` with `wpilib.run(MyRobot)`
- Typical control loop: 50Hz periodic methods (TimedRobot, CommandScheduler)
- Use `mdbook-repl` here only for learning; real robot code deploys via pyfrc or VS Code WPILib tools

## Networking
- mDNS names: `roborio-XXXX-frc.local`
- Static IP convention: `10.TE.AM.2`
- NetworkTables: primary telemetry channel to dashboards and coprocessors

## Best Practices
- Keep CAN IDs unique and documented
- Use brownout-friendly current limits on motor controllers
- Log critical telemetry for post-match analysis

{{#authors lmaxwell24}}
