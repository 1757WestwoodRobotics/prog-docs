# Ramsete

The Ramsete controller is a controller that is specifically designed for path following with a differential drivetrain. It is a nonlinear controller that is able to track a path with a high degree of accuracy, even in the presence of disturbances.

The Ramsete controller works by calculating the error between the robot's current pose and the desired pose on the path. It then uses this error to calculate the linear and angular velocities that will move the robot closer to the path.

WPILib provides a `RamseteCommand` that makes it easy to use the Ramsete controller.

### Example: Following a Trajectory with RamseteCommand

This example shows how to create a trajectory and follow it using `RamseteCommand`.

```python
import commands2
import wpilib.controller
import wpimath.kinematics
from wpimath.trajectory import TrajectoryGenerator, TrajectoryConfig
from wpimath.geometry import Pose2d, Rotation2d

# Assume you have a Drivetrain subsystem with the following:
# - getPose() -> Pose2d
# - getWheelSpeeds() -> DifferentialDriveWheelSpeeds
# - tankDriveVolts(left_volts, right_volts)
# - kinematics -> DifferentialDriveKinematics
# from subsystems.drivetrain import Drivetrain

class MyRobot(wpilib.TimedRobot):
    def autonomousInit(self):
        self.drivetrain = Drivetrain() # Your drivetrain subsystem
        
        # 1. Create a trajectory to follow
        config = TrajectoryConfig(maxVelocity=3, maxAcceleration=1.5)
        config.setKinematics(self.drivetrain.kinematics)
        trajectory = TrajectoryGenerator.generateTrajectory(
            start=Pose2d(0, 0, Rotation2d.fromDegrees(0)),
            interiorWaypoints=[],
            end=Pose2d(2, 0, Rotation2d.fromDegrees(0)),
            config=config
        )

        # 2. Create the RamseteCommand
        ramsete_command = commands2.RamseteCommand(
            trajectory, # The trajectory to follow
            self.drivetrain.getPose, # A function to get the robot's pose
            wpilib.controller.RamseteController(b=2, zeta=0.7), # The Ramsete controller
            self.drivetrain.kinematics, # The drivetrain's kinematics
            self.drivetrain.tankDriveVolts, # A method to control the motors by voltage
            [self.drivetrain] # The drivetrain subsystem, for requirements
        )

        # 3. Schedule the command
        # The command will run and automatically finish when the trajectory is done.
        ramsete_command.schedule()
```

For more information, see the RobotPy Ramsete controller documentation: [https://robotpy.readthedocs.io/en/stable/wpilib/wpilib.controller.RamseteController.html](https://robotpy.readthedocs.io/en/stable/wpilib/wpilib.controller.RamseteController.html)
