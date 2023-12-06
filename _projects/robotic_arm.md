---
layout: page
title: Robotic Arm w/ Teleoperation and Haptic Feedback
description: 
img: assets/img/robotic_arm/LabVolt-M80.jpeg
importance: 4
category: work
---

This year-long electrical and computer engineering capstone project involved the development of a system for the teleoperation of a robotic arm with haptic feedback. The project team consisted of two electrical engineers, tasked with the development and calibration of the sensor systems for the user and the robotic arm, and two computer engineers, tasked with the development of the control system for the robotic arm, the sensor data analysis and the communications between the sensor computer and the robot control computer.

The code was written primarily in C++, which was used to implement the network programming, sensor data reading and fusion, control input calculation, and control input sending through the Labvolt SDK.

Below is a list of the components and tasks that I personally completed:
    - High level system design
    - Initial project ideation
    - Selection and ordering of flex sensors, IMU, haptic motors
    - Selection of sensor glove components
    - Implementation of serial reading from Arduino
    - Implementation of wireless communication through sockets
    - Component testing (ranges of values from IMU, flex sensors, touch sensors)
    - Implementation of haptic responses through haptic motors
    - Implementation of transforming sensor data into control inputs
    - Implementation of using the robotic arm SDK to utilize the control inputs

The parts list for the sensor array can be seen below:
<table>
<thead>
  <tr>
    <th>Component</th>
    <th>Quantity<br></th>
    <th>Description/Use<br></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Arduino Mega</td>
    <td>1</td>
    <td>Interface for control glove sensors and haptic devices</td>
  </tr>
  <tr>
    <td>Flex Sensors</td>
    <td>2</td>
    <td>Measure bend at fingers, wrist, elbow</td>
  </tr>
  <tr>
    <td>IMU (Inertial Momentum Unit)</td>
    <td>1</td>
    <td>Measure rotation of arm, movement of arm in x-y plane</td>
  </tr>
  <tr>
    <td>Vibro-motors</td>
    <td>4</td>
    <td>Provide tactile feedback to user based on amount of pressure applied</td>
  </tr>
  <tr>
    <td>Linear Actuator</td>
    <td>1</td>
    <td>Provide physical pull-back to indicate maximum pressure threshold on object</td>
  </tr>
  <tr>
    <td>Arduino Uno</td>
    <td>1</td>
    <td>Interface for reading pressure data from sensors attached to LabVolt 5150</td>
  </tr>
  <tr>
    <td>Pressure sensors</td>
    <td>4</td>
    <td>Sense object interaction on Labvolt robot</td>
  </tr>
  <tr>
    <td>Arm-Length Glove</td>
    <td>1</td>
    <td>Mount sensors and haptic feedback components</td>
  </tr>
  <tr>
    <td>Nylon Cabling</td>
    <td>2</td>
    <td>Attached to linear actuator to apply pressure to user’s fingertips</td>
  </tr>
  <tr>
    <td>3D printed glove components</td>
    <td>1</td>
    <td>Bind fingers together, provide anchor points for cabling and vibro-motors</td>
  </tr>
</tbody>
</table>

Below, some images of the assembled sensor array for the robot can be seen.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/robotic_arm/WiringSetup.jpg" title="Wiring w/ Arduino" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/robotic_arm/SensorArray.jpg" title="User Sensor Array" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Images of the wiring of the sensor array. On the left, we can see the Arduino with the wiring on a breadboard that attaches to various sensors. On the right, we can see the sensor array attached to the user control glove.
</div>

Below, a video of the demonstration of the project is available, showcasing the functionality of the robotic arm teleoperation system.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.html path="https://youtube.com/embed/32ntHmpMPzw" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Unfortunately, several axes of rotation for the robot, as well as some planned haptic responses were left uncompleted due to the onset of COVID-19 and the subsequent graduations of the team members.

