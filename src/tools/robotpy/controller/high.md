# Higher order controllers

Higher-order controllers are controllers that use more than just the error, the sum of the errors, and the rate of change of the error to calculate the output. These controllers can be used for more complex systems that cannot be controlled effectively with a simple PID or PIDF controller.

Some examples of higher-order controllers include:

-   **State-space controllers:** These controllers use a mathematical model of the system to calculate the optimal output.
-   **Fuzzy logic controllers:** These controllers use a set of rules to calculate the output, rather than a mathematical formula.
-   **Neural network controllers:** These controllers use a neural network to learn the optimal control law for the system.

Higher-order controllers can be very powerful, but they can also be more difficult to design and tune than simple PID controllers.

### Example: 4-Wheel Swerve Drive Holonomic Path Planning Controller

A holonomic path planning controller for a 4-wheel swerve drive is a good example of a higher-order controller. This type of controller is responsible for calculating the desired state of each of the four swerve modules (i.e., the angle and speed of each wheel) in order to follow a given trajectory.

Here is an example of a holonomic path planning controller for a 4-wheel swerve drive:

```python
import wpilib
import wpilib.controller
import wpilib.kinematics

class SwerveController:
    def __init__(self, kinematics, x_controller, y_controller, angle_controller):
        self.kinematics = kinematics
        self.x_controller = x_controller
        self.y_controller = y_controller
        self.angle_controller = angle_controller

    def calculate(self, current_pose, desired_state):
        # Calculate the feedforward from the desired state
        ff = self.kinematics.toSwerveModuleStates(desired_state)

        # Calculate the feedback from the PID controllers
        x_feedback = self.x_controller.calculate(current_pose.X(), desired_state.pose.X())
        y_feedback = self.y_controller.calculate(current_pose.Y(), desired_state.pose.Y())
        angle_feedback = self.angle_controller.calculate(current_pose.rotation().radians(), desired_state.pose.rotation().radians())

        # Combine the feedforward and feedback
        chassis_speeds = wpilib.kinematics.ChassisSpeeds(x_feedback, y_feedback, angle_feedback)

        # Convert the chassis speeds to swerve module states
        swerve_module_states = self.kinematics.toSwerveModuleStates(chassis_speeds)

        return swerve_module_states
```

For a complete example of a 4-wheel swerve drive holonomic path planning controller, see the `swerve-bot` example in the `robotpy-examples` repository on GitHub: [https://github.com/robotpy/robotpy-examples/tree/main/swerve-bot](https://github.com/robotpy/robotpy-examples/tree/main/swerve-bot)