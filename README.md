# Phase 1: ROS2 Humble Installation

Systempakete aktualisieren

```bash
sudo apt update && sudo apt upgrade -y
```

Benötigte Pakete installieren

```bash
sudo apt install curl gnupg lsb-release -y
```

ROS2 Repository-Schlüssel hinzufügen

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo gpg --dearmor -o /usr/share/keyrings/ros-archive-keyring.gpg
```

ROS2 Repository hinzufügen

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

Paketliste aktualisieren

```bash
sudo apt update
```

ROS2 Humble Desktop installieren

```bash
sudo apt install ros-humble-desktop -y
```

ROS2 Umgebung konfigurieren (bei jedem Terminalstart automatisch laden)

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

Abhängigkeiten installieren (für Build-Prozesse)

```bash
sudo apt install python3-colcon-common-extensions python3-rosdep python3-argcomplete -y
sudo rosdep init
rosdep update
```

Installation testen

```bash
ros2 run demo_nodes_cpp talker
```

Wenn kontinuierlich Nachrichten ausgegeben werden, ist ROS2 korrekt installiert.

---

# Phase 2: TurtleBot3 Installation und Gazebo Simulation

In dieser Phase:

* Installation der TurtleBot3 Pakete
* Auswahl des Robotermodells
* Start der Simulation

TurtleBot3 Pakete installieren

```bash
sudo apt install ros-humble-turtlebot3* -y
```

TurtleBot3 Modell setzen

```bash
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
```

burger = klein und leicht, ideal für Simulation
Alternativen: waffle oder waffle_pi

Simulation starten

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

Wenn Gazebo startet und der Roboter sichtbar ist, ist die Installation erfolgreich.

Roboter per Tastatur steuern

Neues Terminal öffnen:

```bash
source /opt/ros/humble/setup.bash
```

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

Dieser Schritt testet die grundlegende Bewegung und Steuerung.

---

# Phase 3: SLAM (Kartenerstellung)

Ziel: Der TurtleBot3 erstellt während der Bewegung eine Karte der Umgebung.

SLAM Paket installieren

```bash
sudo apt install ros-humble-slam-toolbox -y
```

Zusätzliche benötigte Pakete installieren

```bash
sudo apt install ros-humble-slam-toolbox -y
sudo apt install ros-humble-turtlebot3 -y
```

slam_toolbox = Echtzeit-SLAM
turtlebot3 Paket = Roboterspezifische Konfiguration

TurtleBot3 Modell erneut setzen

```bash
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc
```

Gazebo Simulation starten

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

SLAM starten

Neues Terminal öffnen:

```bash
source /opt/ros/humble/setup.bash
ros2 launch slam_toolbox online_async_launch.py
```

Dieser Prozess muss parallel zur Simulation laufen.

Roboter bewegen

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

Während der Bewegung wird die Karte erstellt.

---

# RViz starten

Neues Terminal öffnen:

```bash
source /opt/ros/humble/setup.bash
```

```bash
rviz2
```

Dies öffnet die grafische Visualisierungsoberfläche.

# Autonome Navigation

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=true
```

Zielsetzung mit RViz
RViz öffnet sich und Sie können das Werkzeug „2D-Navigationsziel“ verwenden.
Der Roboter bewegt sich autonom auf das Ziel zu.

# RViz Konfiguration für SLAM

Add → By Topic → map
Zeigt die erstellte Karte

Add → RobotModel
Zeigt Position und Orientierung des Roboters

2D Pose Estimate und 2D Nav Goal
Ermöglichen das Setzen von Startposition und Ziel

---

# Überprüfung

Während:

* Gazebo läuft
* der Roboter per Tastatur bewegt wird
* RViz geöffnet ist und map + RobotModel aktiv sind

wird die Karte schrittweise aufgebaut und aktualisiert.


