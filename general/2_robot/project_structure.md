# Project Structure

An FRC project is set up differently than a normal Java project.

We have a folder for each subsystem.

This is an example of the different files in our intake subsystem

![intake_folder.png](../../images/intake_folder.png)


### IntakeIO, IntakeIOSim, and IntakeIOSpark
First, we have IntakeIO. This is an interface. We need an interface so we can switch between our simulation and real world code.

![intakeio_spark_implement.png](../../images/intakeio_spark_implement.png)
![intakeio_sim_implement.png](../../images/intakeio_sim_implement.png)

### Why an interface?
IntakeIOSpark and IntakeIOSim both implement IntakeIO's interface. IntakeIO defines the basic functions, and then Spark and Sim have different definitions for those functions. That way, the Intake class can call functions from IntakeIO; whichever IO we are using (Spark or Sim) will have a definition for that function, and the appropriate code will run.

For example, say we have a function, `void deployIntake()`. When running code on the robot, we'll want to connect to the motor that moves the intake, then apply voltage to that motor. But if we try to connect to a motor while simulating, the code will crash because the motor isn't there. We have to set things up differently for the sim, connecting to simulated motors instead.

Both IntakeIOSim and IntakeIOSpark will define `deployIntake()`. One will use real motors, and one will use simulated ones. That way, the Intake class can call `deployIntake` regardless of if we are simulating or not; the appropriate code will run. This lets us keep the simulation logic exactly the same as the real robot, and also makes it really easy for us to switch between sim and real life.

### What does each one do?
IntakeIOSpark is the link between hardware and software. We define motor related things here (like encoders) and create methods to track a motor's position, temperature, and voltage. 
IntakeIOSim links the code to simulated motors, tracking theoretical position instead. 

### Intake
Next, we have Intake. This is where methods to handle logic are put such as `isDeployed()`, which checks whether the intake is deployed or not and returns true or false. 

In here, we also have methods that can set motor positions such as `setActuatorTargetPosition()`and motor voltages like `setRollerVoltage()`. These methods can be used in commands that combine multiple steps (more on this later). 

This class also contains the `periodic()` method. This method runs continuously when the robot is enabled. It calls methods like intakeIO's `updateInputs()` which need to be updated continuously. 