# Talon FX
The Talon FX is a high-performance brushless motor controller from CTRE. It is designed to be used with the
Falcon 500 motor, and it provides a number of advanced features, including:

-   **Integrated encoder:** The Talon FX has a built-in encoder that provides high-resolution feedback on
the motor's position and velocity.
-   **On-board PID:** The Talon FX can run PID loops on-board, which can help to improve the performance and
reduce the latency of your control loops.
-   **Motion Magic:** Motion Magic is a feature that allows you to control the motor's position using a
trapezoidal motion profile. This can be used to create smooth and accurate movements.

### Example: Simple Position Control

This example shows how to configure a Talon FX and use its on-board PID controller to move to a specific position.
```python
import ctre
import wpilib

class MyRobot(wpilib.TimedRobot):
    def robotInit(self):
        self.talon = ctre.WPI_TalonFX(1)
        self.joystick = wpilib.Joystick(0)

        # --- Configure the Talon FX ---
        self.talon.configFactoryDefault() # Start with a clean slate

        # Configure the PID gains for the position loop (slot 0)
        self.talon.config_kP(0, 0.1)
        self.talon.config_kI(0, 0.0)
        self.talon.config_kD(0, 0.0)

        # Configure the sensor. The integrated sensor is the default.
        self.talon.configSelectedFeedbackSensor(ctre.FeedbackDevice.IntegratedSensor, 0, 0)

    def teleopPeriodic(self):
        # When the A button is pressed on the joystick, move to position 10000
        if self.joystick.getAButtonPressed():
            target_position = 10000 # Sensor units
            self.talon.set(ctre.TalonFXControlMode.Position, target_position)

# To simply drive the motor with a joystick:
speed = self.joystick.getY()
self.talon.set(ctre.TalonFXControlMode.PercentOutput, speed)
```
{{#authors lmaxwell24}}
