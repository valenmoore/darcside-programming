# Control Systems (PID)
A lot of the time, we have to control motors with more control than just voltage. We might have to speed up a flywheel to a very specific RPM, or rotate a motor to a certain angle. For this, we use a variety of control systems. The two most common types are feedforward control and PID control.

I'll do my best to explain stuff but honestly the best way to understand all this is [this website](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-flywheel.html#pure-feedforward-control); just mess around with the feedforward, then go to pure feedback, then do the combination.

## Feedforward
Feedforward control is a basic way of precisely controlling a system/motor. It applies voltage based on a mathematical model of the motor. 

For example, if you want to get a motor up to a certain velocity (RPM), you can set a parameter, $K_v$; the feedforward controller will apply $K_v \times \text{target velocity}$ volts. Basically, this means that it takes $K_v$ volts to get one unit of velocity. Maybe it generally takes about 0.5V to speed the motor up by 100 RPM, so $K_v$ would be volts per RPM, or 0.5/100.

There are other parameters too. You can set the $K_s$ to determine the voltage needed to overcome friction; a small amount of voltage is required to spin a motor at all, so when $K_s$ is set, the feedforward controllers adds $K_s$ into its voltage calculation. You can set a $K_g$ to compensate for gravity, a paramater for acceleration ($K_a$) similar to the one for velocity, and more; you can read about types of feedforward systems and parameters [here](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/controllers/feedforward.html). The type of feedforward you use depends on the system: for example, an elevator needs to compensate for gravity, but a flywheel just spins, so gravity has no effect on it.

You usually find these values by trial and error, but you can also use [SysID](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/system-identification/introduction.html) to do it automatically.

Feedforward might seem complicated, but to make it simpler, I highly recommend messing around with [this website](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-flywheel.html). Scroll down to the part that says "Pure Feedforward Control" and change the parameters to "tune" the simulated flywheel. This gives a good baseline to what feedforward actually is, and also its limitations.

## Feedback (PID)
Feedback works by looking at the error in the system. The error is the target - actual (so for example, if the setpoint is 1000 RPM and the motor is at 400 RPM, then error is 600 RPM). There are three parameters, $K_p$, $K_i$, and $K_d$. We don't ever use $K_i$ so don't worry about it. So for us, the voltage is:

$\text{voltage} = K_p \times \text{error} + K_d \times \frac{d}{dt} (error)$

Basically, the further off from the target, the more voltage it applies; as it gets closer to the target, it applies less voltage. Feedback is necessary for precise control and handling unexpected errors/friction etc.

## Analogy?
The best analogy I can come up with is driving a car: if you see a curve coming up, you know that you need to turn the wheel to follow the curve. Based on driving in the past, you can look at how much you need to turn the wheel to follow the curve; that's basically feedforward. But if you hit a pothole or for some reason, you aren't turning as much as you need to, you can observe that you are not following the correct path (that there is some error) and turn the wheel back to compensate for the error. The more error there is, the more you have to turn the wheel to compensate.