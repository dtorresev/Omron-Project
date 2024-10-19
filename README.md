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

![Captura de pantalla 2024-10-16 200906](https://github.com/user-attachments/assets/b8aaa957-90a5-49b1-b034-57702a71b39a)  

## Software

- [TMFlow 1.86.1900](https://automation.omron.com/en/us/products/family/Omron%20TM%20Software)
- [Mobile Planner 5.4](https://automation.omron.com/en/ca/products/family/Mobile%20Planner)

![MobilePlanner_img](https://github.com/user-attachments/assets/40a63cbc-15f4-4678-a65e-ab009980cb5f)


## ARCL commands used
```
createinfo infoName maxLen infoValue
```
"createinfo " + "indication "+  "2 " + "0" + newline

The command returns (seen via PuTTY):
> Created info for indication

```
updateinfo infoName infoUpdate
```
"updateinfo " + "id_pieza " + var_identero

The command returns:
> Updated info for id_pieza

```
getinfo infoName
```
"getinfo " + "indication "

The command returns:
> Info: indication 0
     
```
status
```

```
stop
```

```
goto targetLocation
```
## Resources

[Hardware] (https://assets.omron.eu/downloads/manual/en/v2/i623_collaborative_robots_hardware_installation_manual_en.pdf) 
[ARCL reference manual](https://assets.omron.eu/downloads/latest/manual/en/i617_advanced_robotics_command_language_(arcl)_reference_manual_en.pdf?v=14) 