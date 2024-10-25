# Omron-Project

 &emsp;&emsp;&emsp; &emsp;&emsp;&emsp;<img src="https://github.com/user-attachments/assets/59931057-4709-4bf5-9fed-4772df0355c9" alt="tec_logo" width="500" height="110"> &emsp;<img src="https://github.com/user-attachments/assets/1348ceb1-a232-4301-8459-e93a3aed01b6" alt="smart_logo" width="110" height="110" >

## Table of Contents

- [About](#about)

- [Software](#software)

- [Mapping](#mapping)

- [ARCL](#arcl)

- [Vision System](#vision-system)

- [PI System](#pi-system)

- [Results](#results)

- [Resources](#resources)


## About

This project was developed as part of our concentration in Cyber-Physical Systems at Tecnológico de Monterrey (Monterrey Campus), integrating collaborative robotics tools and equipment such as a TM5M-700 manipulator and an LD60 Autonomous Mobile Robot, equipment from Omron Automation available at Smart Factory MTY, an intelligent laboratory intended for improving, automating and enhancing manufacturing processes.

&emsp;&emsp;&emsp; &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; &emsp;&emsp;&emsp;<img src="https://github.com/user-attachments/assets/5f6d4754-e80f-4c66-a3d7-9656813c37b6" alt="omron_lab" width="400" height="533" >


A brief description of the robots' capabilities and features:
* [TM5M-700](https://assets.omron.com/m/51e5aefd34c8f75e/original/TM-Series-Collaborative-Robot-Datasheet.pdf)
  * Payload: 6kg
  * Reach: 700mm
  * Tool:
      - Inputs-> Digital: 4, Analog: 1
      - Outputs -> Digital: 4
  * Control Box:
      - Inputs -> Digital: 16, Analog: 2
      - Outputs -> Digital: 16, Analog: 1
  * Communication:
     - RS232
     - Ethernet 
     - Modbus TCP/RTU
  * Integrated 5-megapixel color camera.

* [LD-60](https://industrial.omron.es/es/products/ld-series)
  * Maximum load capacity: 60 kg.
  * Automatic efficient route planning and collision prevention.
  * Indoor usage.
  * Integrates safety laser scanners on both front and back panels.


## Software

- [TMFlow 1.86.1900](https://automation.omron.com/en/us/products/family/Omron%20TM%20Software)

![TMFlow_img](https://github.com/user-attachments/assets/1dcdadf3-dc59-4368-a38d-a01f8f302d30)


- [Mobile Planner 5.4](https://automation.omron.com/en/ca/products/family/Mobile%20Planner)

![MobilePlanner_img](https://github.com/user-attachments/assets/40a63cbc-15f4-4678-a65e-ab009980cb5f)

## Mapping

Using MobilePlanner, an initial connection with the mobile robot was done, using its IP address and an admin account, this software is used only for the mobile robot's mapping and trajectory, thus only the LD60 was connected. The robot did an area scan to do an initial mapping of the laboratory, using relevant features for mobile robotics like LiDARS, obstacle detection and path planning. The "working space" for the robot was left after defining the areas to be excluded for the robot trajectories which would include walls, tables, chairs, and other laboratory equipment that is intended to be avoided by the robot.

![Captura de pantalla 2024-10-17 172128](https://github.com/user-attachments/assets/3d443fe0-e0cc-4641-b350-56d3616c15aa)

Then, goals were set, where locations are established for the robot to head to when instructed to move, for the main process, four locations were set, 3 main goals and one home location.

The last thing performed using MobilePlanner was the delimitation of preferred trajectories to be followed by the robot, imitating an industrial environment where the robot's working area and walkways must be indicated and signposted.


## ARCL
Advanced Robotics Command Language (ARCL) is a simple command-and-response operating language developed by Omron Robotics and Safety Technologies, Inc. used for their Autonomous Mobile Robots (AMR) to communicate with other external automation systems.

This language allows users to operate and monitor the AMR's operations using command prompts via PuTTY or Telnet, providing a more efficient interface to perform debugging, assessment and evaluating processes.

Before performing any operation using ARCL, an initial setup was done, where the ARCL server address were defined, plus the set up of an access port and a password to connect with the mobile robot.

Access port and password can be left as default parameters as seen in the _Figure 2-1. ARCL Server Setup Parameters_ shown below (from the ARCL Reference Guide).

![ARCL Server Parameters](https://github.com/user-attachments/assets/2102fe4d-86fd-4c56-a6a3-daaf175fcd23)

### Commands
One key aspect to address when using commands to connect with the mobile robot via a command prompt terminal comes with te use of __spaces__ and __indentations__, the terminal will recognize spaces as delimiters for new parameters to be added. This issue was a recurring obstacle for our progress.

Whenever new information was updated with a string containing spaces said string would appear as a trimmed version of the original data. For example, sending the following prompt:

```
"updateinfo " + "id_pieza " + "LOTE 1 PIEZA 1 BLANCO" + newline
```

Would only display:
> Info: id_pieza BLANCO

This issue was solved by using a colon [ : 
] to indicate the division of the part's information.

Introducing data like the the part's batch and ID number, as well as the color of the part being used in the process.

```
var_identero = "LOTE1:PIEZA1:" + "BLANCO"

"updateinfo " + "id_pieza " + var_identero + newline
```
An explanation of the main commands used for this project is displayed below:

```
createinfo infoName maxLen infoValue
```
"createinfo " + "indication "+  "2 " + "0" + newline

The command returns (seen via command prompt terminal):
> Created info for indication

```
updateinfo infoName infoUpdate
```
"updateinfo " + "id_pieza " + var_identero + newline

The command returns:
> Updated info for id_pieza

```
getinfolist
```
"getinfolist " + newline

An example of how the _getinfolist_ command is displayed in the terminal can be shown below:

<img src="https://github.com/user-attachments/assets/89db6b9f-9b85-445f-ad7d-cc8cffb41733" alt="Alt Text" width="200" height="200">

Using getinfolist early in the program development allowed for easier debugging tasks and saving time when verifying the succesful creation of information packages. 


```
getinfo infoName
```
"getinfo " + "indication " + newline

The command returns:
> Info: indication 0
     
```
status
```
"status " + newline

```
stop 
```
"stop " + newline

The command returns:
> Stopping

Stopping the mobile robot. 

```
goto targetLocation
```
"goto " + var_Goal + newline

The command returns:
> Going to Goal

Sending the robot to the selected target location.

## Vision System

The TM5M-700 manipulator has a 5M-pixel camera attached to the wrist joint of the robot. Including a lightning ring to improve image quality captured to perform Automated Optical Inspections (AOI).

For this project, the vision system was used extensively to improve the program.  Some of the features where the vision system was used for the project include:

- Robot Servoing
- QR Scanning
- Color Detection

__Robot Servoing__: Used to automatically re-orient the robot into a correct picking position whenever the part was left on the picking table with a certain tilt or different position than the one originally established (within range). 

The first step to utilizing Robot Servoing features in TMFlow begins with the identification of a visual pattern to be identified, although Smart Pattern Learner is available, we manually edited the selected pattern to recognize the 3 main square blocks that comprise the QR codes used, as well as a small one on the top right corner, it is crucial to highlight the use of the right lightning and distance to perform quality visual inspections.

![Captura de pantalla 2024-10-21 143528](https://github.com/user-attachments/assets/50da10c4-5e92-41d3-ad10-4fe7b7955a7b)

Once the pattern is set, the Servoing Target shall be set as well, in this case, it was intended for the robot to align its Tool Center Point with the corresponding orientation of the QR code, so we selected the _Use Current Position_ feature.

![Captura de pantalla 2024-10-21 143554](https://github.com/user-attachments/assets/69b6bbc2-02e8-4126-b4bf-756a003d8fcd)

![Captura de pantalla 2024-10-21 143641](https://github.com/user-attachments/assets/c3c72cf0-aabb-49dc-95ed-42b6c241ec7e)

Once this three-step process is concluded, the robot servoing is ready to go. 


__QR Scanning__: Containing information regarding the batch and part ID of the product being manipulated, useful for traceability purposes to track any quality issues in the process.

![img](https://github.com/user-attachments/assets/de8622a1-9a71-44d4-bb65-d12d04cfdbb9)


__Color Detection__: In this case, the robot was set different criteria for evaluation to label the color of the part, being blue, white or default the main labels indicated. Here blue represented a faulty or defective part, white a standard quality, and default indicated that there was not enough information to label the part's color, like an empty tray.

![img](https://github.com/user-attachments/assets/b55f9e43-cfd2-44f0-8597-a6e41326c0c0) 

The vision subprocess is composed of the 3 previous features, where the manipulator's camera is located in a reading position perpendicular to the part, runs the vision tasks then using multiple displays for debugging purposes, and creating a variable with the batch, ID and color of the part.

<img src="https://github.com/user-attachments/assets/7b2131af-5f3d-4bc2-a36d-0542814a072a" alt="VisionProcess" width="400" height="450">


## Process

The whole program started with the TM5M-700 connecting to the LD60 mobile robot as a network device, using its IP address as well as the specified port for communication, and prompting the set password. 

Subsequently, information packages such as the indication variable, the part's ID, and current working station were created (Note that this is only required to be done once.)

![createinfo_img](https://github.com/user-attachments/assets/d1ed0342-e6f3-4ad5-a778-e8fda522715c)

The variables are initialized with default values, but they are reinitialized once the process has concluded.

![updateinfo_img](https://github.com/user-attachments/assets/dc166578-878e-4b76-a756-1c3cde645170)

Then, the indication value is read indefinitely, where the manipulator loudly states "Waiting for Indication" in a loop until the indication value is updated by the host via Telnet.

<img src="https://github.com/user-attachments/assets/280eacf4-9baf-471a-b1bc-84e0aacf1605" alt="VisionProcess" width="550" height="300"> 

Once the robot has read the indication value set to 1, the robot will move to the Goal3, where the part to inspect has been dropped, proceeds with the visual inspection, picks up the part, and travels to the indicated Goal depending on the color identified. When the part is left in position, the robot travels to the Home station and updates the indication value to a 0, restarting the process and waiting for another indication to be sent. 
   
![img](https://github.com/user-attachments/assets/5b868b6a-3e25-4204-86cb-e72ad1ed1948)

## PI System

> PI Vision was not included in the initial delivery of this project.

Implementing Modbus TCP/IP communication was established with the TM5M-700 manipulator. 

Using AVEVA PI System, and joining a local server created for Tecnológico de Monterrey, we were able to create a personal database to gather information from the robot, monitoring its state during operation.

A service was created using PI Interface Configuration Utility to provide a bridge between the robot and the server using Modbus TCP/IP. Then, by creating PI Points associated with a particular register address each attribute of interest was monitored in real-time. The last step was including said PI Points as elements of a database, and using AVEVA PI Vision, a user-interface was developed to provide a visual representation of the robot's performance in real-time.

[![Pivision](https://img.youtube.com/vi/LyFWUElHVyo/0.jpg)](https://www.youtube.com/watch?v=LyFWUElHVyo)

## Results

The performance of the program worked as expected, picking up the parts from the indicated places as established and delivering them to the corresponding station, uploading the part's information to a dashboard updated via Telnet using ARCL.

__Improvements__ -
Some huge areas of opportunity can be identified for this particular project, from the trajectory creation by adding mid points to prevent failures when reaching or approaching goal locations, adding landmarks to perform robot servoing aside from the QR inspection, providing a more efficient approach in the pick process, including more process variables to update the robot's state during operation, and increasing the manipulator's velocity during the picking and placing process to decrease times. 

## Resources

- [Hardware Installation Guide](https://assets.omron.eu/downloads/manual/en/v2/i623_collaborative_robots_hardware_installation_manual_en.pdf) 

- [ARCL Reference Manual](https://assets.omron.eu/downloads/latest/manual/en/i617_advanced_robotics_command_language_(arcl)_reference_manual_en.pdf?v=14) 

- [LD60 Series datasheet](https://assets.omron.eu/downloads/latest/datasheet/en/i828_ld-series_mobile_robot_datasheet_en.pdf?v=27)

- [TM5M-700 Datasheet](https://assets.omron.com/m/51e5aefd34c8f75e/original/TM-Series-Collaborative-Robot-Datasheet.pdf)