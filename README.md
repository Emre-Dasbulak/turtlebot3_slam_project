# TurtleBot3 SLAM Projekt

## Beschreibung
Dieses Projekt demonstriert die Verwendung von ROS2 Humble mit TurtleBot3 im Gazebo-Simulator.  
Der Roboter erstellt eine Karte seiner Umgebung mithilfe von SLAM und kann autonom zu definierten Zielen navigieren.

## Funktionen
- TurtleBot3 Simulation in Gazebo
- Echtzeit-SLAM mit `slam_toolbox`
- Otonome Navigation zu festgelegten Zielen
- Teleoperation via Tastatur

## Installation
1. ROS2 Humble installieren
2. TurtleBot3 und slam_toolbox Pakete installieren
3. Terminal 1: Gazebo starten
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
