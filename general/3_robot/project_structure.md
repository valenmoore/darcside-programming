# Project Structure

An FRC project is set up differently than a normal Java project.

We have a folder for each subsystem.

This is an example of the different files in our intake subsystem

![intake_folder.png](../../images/intake_folder.png)

First, we have IntakeIO. This is an interface. We need an interface so we can switch between our simulation and real world code.

![intakeio_spark_implement.png](../../images/intakeio_spark_implement.png)
![intakeio_sim_implement.png](../../images/intakeio_sim_implement.png)

IntakeIOSpark and IntakeIOSim both implement IntakeIO's interface.

IntakeIOSpark is the link between hardware and software. We define motor related things here (like encoders) and create methods to track a motor's position, temperature, and voltage. 
