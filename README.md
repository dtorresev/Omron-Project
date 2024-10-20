# Omron-Project
Collaborative and Mobile Robotics Integration

TM5M - 700 Robotic Manipulator Integration

1.1 Automatización con Tecnologías Omron

- Marco teórico de Omron al dia de hoy

- Ventajas de LD Y TM

1.2 Robot Móvil Autónomo Omron LD

1.3 Robot Colaborativo Omron TM

1.4 Desarrollo de Algoritmos para Control y Navegación [Comunicación y base de datos]

1.7 Optimización de Trayectorias en el Robot Omron LD

1.5 Sistemas de Visión para Reconocimiento y Percepción

1.6 Automatización del Proceso de Pick (Recogida)

1.8 Automatización del Proceso de Place (Colocación)

1.9 Gestión del Proceso de Carga y Manipulación

## Index

- [About](#about)
- [Software](#software)
- [ARCL](#arcl)
- [Vision System](#vision-system)
- [Resources](#resources)

![Captura de pantalla 2024-10-16 200906](https://github.com/user-attachments/assets/b8aaa957-90a5-49b1-b034-57702a71b39a)  

## About

This project was developed as part of our concentration in Cyber-Physical Systems Tecnológico de Monterrey (Monterrey Campus), integrating collaborative robotics tools and equipment such as a TM5M-700 manipulator and an LD60 Autonomous Mobile Robot, equipment from Omron Automation available at Smart Factory MTY, an intelligent laboratory intended for improving, automating and enhancing manufacturing processes.

A brief description of the robots' capabilities:
* [TM5M-700]()
* [LD-60](https://industrial.omron.es/es/products/ld-series)
  * Maximum load capacity: 60 kg.
  * Automatic efficient route planning and collision prevention.
  * Indoor usage.
  * Integrates safety laser scanners on bot front and back panels.


## Software

- [TMFlow 1.86.1900](https://automation.omron.com/en/us/products/family/Omron%20TM%20Software)
- [Mobile Planner 5.4](https://automation.omron.com/en/ca/products/family/Mobile%20Planner)

![MobilePlanner_img](https://github.com/user-attachments/assets/40a63cbc-15f4-4678-a65e-ab009980cb5f)


## ARCL
Advanced Robotics Command Language (ARCL) is a simple command-and-response operating language developed by Omron Robotics and Safety Technologies, Inc. used for their Autonomous Mobile Robots (AMR) to communicate with other external automation systems.

This language allows users to operate and monitor the AMR's operations using command prompts via PuTTY or Telnet, providing a more efficient interface to perform debugging, assessment and evaluating processes.

Before performing any operation using ARCL, an initial setup was done, where the ARCL server address were defined, plus the set up of an access port and a password to connect with the mobile robot.

For a collaborative access and ease of use, the access port and password were left as default parameters as seen in the _Figure 2-1. ARCL Server Setup Parameters_ shown below (from the ARCL Reference Guide).

![ARCL Server Parameters](https://github.com/user-attachments/assets/2102fe4d-86fd-4c56-a6a3-daaf175fcd23)

### Commands

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


## Resources

- [Hardware Installation Guide](https://assets.omron.eu/downloads/manual/en/v2/i623_collaborative_robots_hardware_installation_manual_en.pdf) 

- [ARCL Reference Manual](https://assets.omron.eu/downloads/latest/manual/en/i617_advanced_robotics_command_language_(arcl)_reference_manual_en.pdf?v=14) 

- [LD60 Series datasheet](https://assets.omron.eu/downloads/latest/datasheet/en/i828_ld-series_mobile_robot_datasheet_en.pdf?v=27)