# RobotPy

RobotPy is a set of Python modules that allows for the development of robot code for the FIRST Robotics Competition (FRC) in Python. It provides a powerful and easy-to-use framework for controlling the robot's hardware and implementing complex autonomous and teleoperated behaviors.

## Architecture Overview

```mermaid
graph TD
    A[Robot.py] --> B[RobotContainer]
    B --> C[Subsystems]
    B --> D[Commands]
    B --> E[Controller Bindings]
    
    C --> C1[Drivetrain]
    C --> C2[Intake]
    C --> C3[Shooter]
    C --> C4[Elevator]
    
    D --> D1[Default Commands]
    D --> D2[Autonomous Sequences]
    D --> D3[Command Groups]
    
    C1 --> H1[Motor Controllers]
    C1 --> H2[Encoders]
    C1 --> H3[Gyro]
    
    subgraph Telemetry
      T1[NetworkTables]
      T2[AdvantageScope]
      T3[Elastic]
    end
    
    C --> T1
    D --> T1
```

Key concepts covered in this section:
- Command-Based Programming: organizing behaviors via composable commands
- Subsystems: hardware abstraction with periodic updates and state
- Controllers: PID, Bang-Bang, Ramsete, profiled controllers
- Path Following: PathPlanner integration and trajectory tracking
- Telemetry and Logging: AdvantageScope, Elastic dashboards

See also:
- [Robot file structure](./file.md)
- [Subsystems](./subsystem.md)
- [Commands](./commands.md)
- [Controllers](./controller/README.md)
- [NetworkTables](./nettables.md)
- [PathPlanner](./pp.md)

This project uses `pipenv` for dependency management and `black`/`prettier` for formatting. See the [Tools](../README.md) section.

For comprehensive reference, visit the official RobotPy docs: https://robotpy.readthedocs.io/
