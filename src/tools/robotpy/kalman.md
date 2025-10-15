# Kalman filter

A Kalman filter is a powerful tool for state estimation. It is a recursive filter that is able to estimate the state of a system, even in the presence of noise and uncertainty. In FRC, Kalman filters can be used for a variety of purposes, such as:

-   Estimating the robot's position and orientation.
-   Filtering noisy sensor data.
-   Fusing data from multiple sensors.

WPILib provides a `LinearSystem` class and a `KalmanFilter` class that work together.

### Example: Estimating Velocity from Position

Let's say we have a motor with an encoder that measures position, but we also want to know its velocity. We can use a Kalman filter to estimate both position and velocity.

This is a conceptual example. In a real robot, you would use a plant model that matches your system (e.g., from SysId).

```python
import wpimath.system
import wpimath.system.plant
import wpimath.kinematics
import numpy as np

# Let's model a simple system: a motor with position and velocity states.
# x = [position, velocity]'
# We can only measure position. We want to estimate both position and velocity.

# System matrices (for a 50Hz loop, dt=0.02s)
# These describe how the state changes over time.
A = np.array([[1, 0.02], [0, 1]])  # State transition matrix
B = np.array([[0], [0.02]])      # Input matrix (how input affects state)
C = np.array([[1, 0]])           # Measurement matrix (we only measure position)
D = np.array([[0]])              # Feedthrough matrix

system = wpimath.system.LinearSystem_2_1_1(A, B, C, D)

# Kalman filter
# We need to provide standard deviations for process noise and measurement noise.
# These represent how much we trust our model and our sensor, and need to be tuned.
process_noise_std_dev = 0.1
measurement_noise_std_dev = 0.01

kalman_filter = wpimath.kinematics.KalmanFilter_2_1_1(
    system,
    [process_noise_std_dev, process_noise_std_dev],  # State standard deviations
    [measurement_noise_std_dev], # Measurement standard deviations
    0.02 # dt
)

# In the robot loop:
# Get motor voltage (u) and measured position (y)
voltage = 5.0 # example input
u = np.array([voltage])
measured_position = 1.2 # example measurement
y = np.array([measured_position])

# Predict the next state based on the model and input
kalman_filter.predict(u, 0.02)

# Correct the state estimate with the new measurement
kalman_filter.correct(u, y)

# Get the estimated state (position and velocity)
estimated_position = kalman_filter.getX(0)
estimated_velocity = kalman_filter.getX(1)
```

For more information, see the RobotPy Kalman filter documentation: [https://robotpy.readthedocs.io/en/stable/wpilib/wpilib.kinematics.KalmanFilter.html](https://robotpy.readthedocs.io/en/stable/wpilib/wpilib.kinematics.KalmanFilter.html)
