# PID Control

A PID (Proportional-Integral-Derivative) controller is a closed-loop control algorithm that computes a control signal from the error between a desired setpoint and the measured process variable. It's widely used in FRC for positioning mechanisms, regulating flywheel speed, and heading control.

## How PID Works

```mermaid
flowchart TD
    subgraph "PID Controller"
        A[Setpoint r] --> E[Error Calculator]
        Y[Measured Output y] --> E
        E --> |e = r - y| G[Error Signal]
        
        G --> P["Proportional\nKp × e"]
        G --> I["Integral\nKi × ∫e dt"]
        G --> D["Derivative\nKd × de/dt"]
        
        P --> S["Σ"]
        I --> S
        D --> S
    end
    
    S --> |Control Signal u| M[Motor/Actuator]
    M --> Plant[Physical System]
    Plant --> |Feedback| Y
    
    style A fill:#e1f5fe
    style Y fill:#f3e5f5
    style P fill:#e8f5e8
    style I fill:#fff3e0
    style D fill:#fce4ec
    style S fill:#f1f8e9
```

### PID Response Characteristics

```mermaid
xychart-beta
    title "PID Component Contributions Over Time"
    x-axis "Time" [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    y-axis "Output" -0.5 --> 1.5
    line "Setpoint" [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
    line "P Term" [0, 0.8, 0.3, 0.1, 0.05, 0.02, 0.01, 0.005, 0, 0, 0]
    line "I Term" [0, 0.1, 0.25, 0.4, 0.5, 0.6, 0.65, 0.7, 0.72, 0.73, 0.74]
    line "D Term" [0, 0.2, -0.1, -0.05, -0.02, -0.01, 0, 0, 0, 0, 0]
    line "Total Output" [0, 1.1, 0.45, 0.45, 0.53, 0.61, 0.66, 0.705, 0.72, 0.73, 0.74]
```

- **Proportional (Kp·e)**: Reacts to present error. Too high → oscillation; too low → sluggish.
- **Integral (Ki·∫e)**: Eliminates steady-state error by accumulating past errors. Too high → windup and overshoot.
- **Derivative (Kd·de/dt)**: Predicts future error to damp oscillations. Too high → noise amplification.

## Tuning Strategy (Practical FRC Approach)

1. Start with Kp only; increase until oscillations begin, then back off 30–50%.
2. Add Kd to reduce overshoot and dampen oscillations.
3. Add Ki slowly to remove steady-state error (watch for windup).
4. Set output limits and integral range to prevent windup.

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Robot as Robot
    Dev->>Robot: Set Kp = K, Ki = 0, Kd = 0
    Robot-->>Dev: Observe Overshoot/Oscillation
    Dev->>Robot: Reduce Kp, Add Kd
    Robot-->>Dev: Observe Settling
    Dev->>Robot: Add small Ki
    Robot-->>Dev: Steady-State Error eliminated
```

## Anti-Windup and Practical Considerations

- Set `integrator range` to accumulate I only near the setpoint.
- Clamp controller output to motor limits (e.g., -1 to 1).
- Filter measurement if sensor is noisy (moving average, low-pass).
- Use `atSetpoint()` tolerance instead of exact equality.

## RobotPy Example (Position Control)

```python
import wpilib
import commands2

class Elevator(commands2.SubsystemBase):
    def __init__(self):
        super().__init__()
        self.motor = wpilib.PWMSparkMax(0)
        self.encoder = wpilib.Encoder(0, 1)
        
        self.pid = wpilib.PIDController(kP=0.15, kI=0.0, kD=0.01)
        self.pid.setTolerance(0.02)  # 2 cm tolerance
        self.pid.setIntegratorRange(-0.2, 0.2)  # anti-windup
        
        self.setpoint = 0.0
    
    def periodic(self):
        output = self.pid.calculate(self.encoder.getDistance(), self.setpoint)
        # Clamp output to motor safe range
        output = max(-0.8, min(0.8, output))
        self.motor.set(output)
    
    def goTo(self, height_m):
        self.setpoint = height_m
    
    def atGoal(self):
        return self.pid.atSetpoint()
```

## Common Symptoms and Fixes

| Symptom | Likely Cause | Fix |
|--------|--------------|-----|
| Oscillation | Kp too high, Kd too low | Reduce Kp, increase Kd |
| Slow response | Kp too low | Increase Kp |
| Steady-state error | Ki too low or zero | Add/increase Ki |
| Sudden jumps | Noisy sensor, Kd too high | Filter sensor, reduce Kd |

For more information, see the RobotPy PID controller documentation: [PIDController](https://robotpy.readthedocs.io/en/stable/wpilib/wpilib.controller.PIDController.html)
