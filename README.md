# Omron-Project
Collaborative and Mobile Robotics Integration

TM5M - 700 Robotic Manipulator Integration

1.4 Desarrollo de Algoritmos para Control y Navegación [Comunicación y base de datos]

1.7 Optimización de Trayectorias en el Robot Omron LD

1.5 Sistemas de Visión para Reconocimiento y Percepción

1.6 Automatización del Proceso de Pick (Recogida)

1.8 Automatización del Proceso de Place (Colocación)

1.9 Gestión del Proceso de Carga y Manipulación

## Table of Contents

- [About](#about)
- [Software](#software)
- [ARCL](#arcl)
- [Vision System](#vision-system)
- [Resources](#resources)


## About

This project was developed as part of our concentration in Cyber-Physical Systems Tecnológico de Monterrey (Monterrey Campus), integrating collaborative robotics tools and equipment such as a TM5M-700 manipulator and an LD60 Autonomous Mobile Robot, equipment from Omron Automation available at Smart Factory MTY, an intelligent laboratory intended for improving, automating and enhancing manufacturing processes.

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


## ARCL
Advanced Robotics Command Language (ARCL) is a simple command-and-response operating language developed by Omron Robotics and Safety Technologies, Inc. used for their Autonomous Mobile Robots (AMR) to communicate with other external automation systems.

This language allows users to operate and monitor the AMR's operations using command prompts via PuTTY or Telnet, providing a more efficient interface to perform debugging, assessment and evaluating processes.

Before performing any operation using ARCL, an initial setup was done, where the ARCL server address were defined, plus the set up of an access port and a password to connect with the mobile robot.

For a collaborative access and ease of use, the access port and password were left as default parameters as seen in the _Figure 2-1. ARCL Server Setup Parameters_ shown below (from the ARCL Reference Guide).

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

Using getinfolist early in the program development allowed for easier debugging tasks and saving time when verifying the succesfull creation of information packages. 


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
* Imagen de los ejes

![Captura de pantalla 2024-10-21 143641](https://github.com/user-attachments/assets/c3c72cf0-aabb-49dc-95ed-42b6c241ec7e)




__QR Scanning__: Containing information regarding the batch and part ID of the product being manipulated, useful for traceability purposes to track any quality issues in the process.

![Captura de pantalla 2024-10-21 143837](https://github.com/user-attachments/assets/de8622a1-9a71-44d4-bb65-d12d04cfdbb9)



__Color Detection__: In this case, the robot was set different criterias for evaluation to label the color of the part, being blue, white or default the main labels indicated. Here blue represented a faulty or deffective part, white a standard quality, and default indicated that there was not enough information to label the part's color, like an empty tray.

![Captura de pantalla 2024-10-21 144100](https://github.com/user-attachments/assets/b55f9e43-cfd2-44f0-8597-a6e41326c0c0) 

* Imagen del diagrama

## Process

The whole program started with the TM5M-700 connecting to the LD60 mobile robot as a network device, using its IP address aswell as the specified port for communication, and prompting the set password. 

Subsequently, information packages such as the indication variable, the part's ID, and current working station were created (Note that this is only required to be done once.)

![createinfo_img](https://github.com/user-attachments/assets/d1ed0342-e6f3-4ad5-a778-e8fda522715c)



![updateinfo_img](https://github.com/user-attachments/assets/dc166578-878e-4b76-a756-1c3cde645170)

## Resources

- [Hardware Installation Guide](https://assets.omron.eu/downloads/manual/en/v2/i623_collaborative_robots_hardware_installation_manual_en.pdf) 

- [ARCL Reference Manual](https://assets.omron.eu/downloads/latest/manual/en/i617_advanced_robotics_command_language_(arcl)_reference_manual_en.pdf?v=14) 

- [LD60 Series datasheet](https://assets.omron.eu/downloads/latest/datasheet/en/i828_ld-series_mobile_robot_datasheet_en.pdf?v=27)

- [TM5M-700 Datasheet](https://assets.omron.com/m/51e5aefd34c8f75e/original/TM-Series-Collaborative-Robot-Datasheet.pdf)