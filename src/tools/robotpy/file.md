# Robot File Structure

Team 1757's RobotPy projects follow a structured architecture based on the Command-Based programming paradigm. Here's the file structure from our 2026-Rebuilt repository:

```
2026-Rebuilt/
├── robot.py                    # Main robot class (MentorBot)
├── robotcontainer.py           # Central configuration and initialization
├── operatorinterface.py        # Controller mappings and input handling
├── physics.py                  # Robot physics simulation
├── constants/                  # Organized constants by subsystem
│   ├── __init__.py
│   ├── drive.py               # Drivetrain physical constants
│   ├── oi.py                  # Operator interface constants
│   ├── motors.py              # Motor and encoder constants
│   ├── vision.py              # Vision system constants
│   ├── auto.py                # Autonomous constants
│   └── ...
├── subsystems/                # Hardware abstraction layers
│   ├── drive/
│   │   ├── drivesubsystem.py  # Main drivetrain subsystem
│   │   └── swervemodule.py    # Individual swerve module
│   ├── vision/
│   │   └── visionsubsystem.py # Vision processing
│   └── loggingsubsystem.py    # Data logging
├── commands/                  # Robot behaviors and actions
│   ├── drive/                 # Drive-related commands
│   │   ├── absoluterelativedrive.py
│   │   ├── fieldrelativedrive.py
│   │   └── ...
│   ├── drivedistance.py       # Autonomous drive command
│   └── defensestate.py        # Defensive positioning
├── util/                      # Utility functions and helpers
│   ├── simtalon.py           # Simulation motor wrapper
│   ├── controltype.py        # Controller abstraction
│   └── ...
├── deploy/                    # PathPlanner paths and configs
│   └── pathplanner/
└── tests/                     # Unit tests
```

## Key Architecture Components

### **robot.py** - Entry Point
```python
class MentorBot(commands2.TimedCommandRobot):
    def robotInit(self):
        self.container = RobotContainer()
    
    def getAutonomousCommand(self):
        return self.container.getAutonomousCommand()
```

### **robotcontainer.py** - Central Hub
- Instantiates all subsystems
- Sets up default commands
- Configures button bindings
- Manages autonomous chooser
- Initializes logging and telemetry

### **operatorinterface.py** - Input Abstraction
```python
class OperatorInterface:
    class Drive:
        reset_gyro = ControlButton(0, 16)
        defense_state = ControlButton(2, 24)
        
        class ChassisControls:
            class Translation:
                y = SignSquare(Invert(Deadband(ControlAxis(0, 1)(), kDeadband)))
```

### **constants/** - Modular Organization
Unlike a single `constants.py` file, Team 1757 organizes constants by functional area:

- **`drive.py`**: Physical robot dimensions, motor IDs, PID gains, swerve module positions
- **`oi.py`**: Controller deadbands and input thresholds
- **`motors.py`**: Encoder pulse counts and motor specifications
- **`vision.py`**: Camera configurations and pipeline settings

## Development Patterns

### **Subsystem Design**
- Each subsystem inherits from `commands2.SubsystemBase`
- Hardware initialization in `__init__()`
- State updates in `periodic()`
- High-level methods for command interface

### **Command Structure**
- Commands inherit from `commands2.Command`
- Organized by functional area (drive/, auto/, etc.)
- Clear lifecycle methods: `initialize()`, `execute()`, `isFinished()`, `end()`

### **Simulation Support**
- `physics.py` for robot physics simulation
- `util/simtalon.py` wraps motor controllers for sim/real compatibility
- Comprehensive simulation testing capabilities

## Best Practices from 2026-Rebuilt

1. **Modular Constants**: Organize constants by subsystem for maintainability
2. **Controller Abstraction**: `OperatorInterface` provides clean input handling
3. **Simulation First**: Built-in simulation support from day one
4. **Comprehensive Logging**: Dedicated logging subsystem for data analysis
5. **PathPlanner Integration**: Modern path planning with deploy directory structure

For the complete codebase, see our [2026-Rebuilt repository](https://github.com/1757WestwoodRobotics/2026-Rebuilt).
