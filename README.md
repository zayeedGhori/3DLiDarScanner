# 3DLiDarScanner
Final project for COMPENG 2DX3 course at McMaster University. This device uses a VL53L1X ToF LiDar sensor to scan a 3D diagram activated by a push button. Using the Texas Instrument MSP432E401Y microcontroller, which is programmed using C, activates a stepper motor to turn it in increments of 22.5 degrees, and stops briefly to capture readings in the y-z axis using I2C to communicate distance readings from the VL53L1X ToF Sensor to the microcontroller. The analog reading from ToF sensor is converted internally using a 16-bit ADC conversion to a digital time signal, then using the speed of light converts this into a distance, which is then transmitted to the microcontroller over I2C. User movement is then required to complete multiple scans in the x direction to complete a diagram. The microcontroller sends a UART signal through USB to the operating computer. The computer Python program takes the UART distances and assumes that the first UART transmission is at 0 degrees and each successive transmission is at an additional 22.5 degree increments. Using simple trigonometry, the distance value is converted into y and z measurements.

# Schematic
![image](https://user-images.githubusercontent.com/47336360/233507171-5ac6a833-fa51-45f0-84fd-85b0d3c6f5d3.png)

# How to use
1.	Connect the MSP432E401Y microcontroller, VL531X ToF sensor, stepper motor and push button as outlined in the circuit schematic, taking special care that all the pins are secured to the correct wires.
2.	Ensure that the motor is mounted to a flat vertical wall and that the ToF sensor is securely placed in its mount and then put onto the stepper motor shaft.
3.	Connect the USB A to Micro-USB wire to the side of the microcontroller without the large ethernet (networking) connector (As shown in the device setup)
4.	Go to Device Manager (on Windows) and search for Serial Connections. Take note of the COM# of the connection that says UART, 
5.	Install Python 3.6 to 3.10.
    1.	Make sure that python is added to PATH.
7.	Open Command Prompt (Windows):
    1.	Type in “python --version” and press Enter to verify Step 4 is completed correctly.
    2.	Type “pip install pyserial”, press Enter.
    3.	Type “pip install open3d”, press Enter.
8.	Open Python IDLE
    1.	Open `deliverable2.py`
    2.	Change `COM9` in line 17 to the COM# found in step 3 and save.
    3.	Keep open for Step 8.
9.	Install Keil uVision 5 and open it.
    1.	Open `2dx_studio_8c`
    2.	Click on the options for Target 1   and ensure that the ARM compiler is set to default:![image](https://user-images.githubusercontent.com/47336360/233507455-a67d66c4-6c4b-4a56-82c2-4afe97ce4287.png)

    3.	Go to the Debug tab in the Target 1 Options and ensure that the CMSIS Debugger is used:![image](https://user-images.githubusercontent.com/47336360/233507480-f8f54308-feae-44b2-a37a-a9b861d2ea68.png)

  
    4.	Exit the Target 1 Options menu.
    5.	Click on Translate![image](https://user-images.githubusercontent.com/47336360/233507716-b74c5afc-5a1a-4ae9-8c1b-e48c44de4bd0.png)
, then Build![image](https://user-images.githubusercontent.com/47336360/233507733-dd6de473-dcc0-452e-985c-dc2a0c87c33f.png)
, then Load ![image](https://user-images.githubusercontent.com/47336360/233507751-d8314753-ac25-4e89-8d10-cc0cc276c38d.png)
 and ensure there are no Errors that prevent the microcontroller from being flashed.
10.	Run `deliverable2.py` in Python IDLE
    1.	Press Enter when prompted.
11.	Move to the location you would like to scan.
12.	Press the reset button on the microcontroller.
13.	Press the push button to start the y-z scan.
    1.	The motor will do a full 360 degree rotation, stopping ever 22.5 degrees to take measurements, ensure that the ToF wires don’t get tangled.
14.	Once the first scan is complete, take one step either forward or backward (ie. in the x-direction).
15.	Repeat steps 11-13 (continuing to move forward if done so in the previous step or backwards, not changing the direction of movement) until 3 cycles have completed.
16.	Once the process is complete, a graph of dots will appear in a new Window.
17.	Close that Window to view the 3D model.
