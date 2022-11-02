# Makitronics EIC2 Series
Makitronics (MKTR) Electromagnetic Interchangeable Coupler version 2 series

## Overview
The Makitronics EIC2 series is a set of electromechanical parts that enables industrial robots such as Universal Robots UR5 and Elephant MyCobot 320 Pro to have more versatility in the workplace. Designed by Dominick Lee, this open-source repository provides affordable options to robot owners who may want to create their own custom grippers or holders for robots.

## Background
Robotic arms have conventionally been a staple of innovative manufacturing. However, robot users are limited to very few commercially available options when it comes to end-effectors. Most grippers or attachments for robot arms may cost from $4k-$15k per piece depending on the precision, versatility, and interoperability of the end-effector. What this means is that small or mid-sized businesses involved in fulfillment or drop-shipping are more often performing tasks by hand rather than utilizing industrial automation technique such as cobots and production lines, especially because of the hassle and high cost of setting up one or more robots. Hypothetically, companies that may have spent $25,000+ on a robot may still find themselves in need of a robot gripper, or perhaps having a gripper that does not get the job done. Historically, companies shelled out tens of thousands of dollars buying a robot but only received an engineering burden instead of a luxury.

### What is MKTR EIC2?
Makitronics EIC2 is a high-performance low-cost solution that lowers the barriers for startups and small businesses to adopt cobots into their existing operations. By providing custom grippers, attachments, sensor mounts, and IoT based control, users can do more with their robot and enhance their existing use-cases. The vision of Makitronics is to provide smart, scalable, and affordable options for robotic and IoT automation. One of the many benefits of using the MKTR EIC2 series is that many end-effectors designed for UR5 or MyCobot 320 Pro can be used interchangeably. In addition to cost savings, there are also innovative advantages in reducing the computational load of machines and reducing the time-to-market when it comes to building a new robotic workflow since EIC2 enables additional sensors and edge-based processing to take place on the end-effector itself. As this is an ongoing project, we anticipate exciting developments.

### Advantages of MKTR EIC2
- Broader impact: Open-source parts that can be adapted to everyday use-cases<br>
- Innovation: Custom built end-effectors that are not on the market yet<br>
- Interchangeability: Being able to use a MyCobot 320 attachment on a UR5 (and vice versa)<br>
- Versatility: Electromagnetic and manual tool switching within seconds<br>
- Affordability: Lowering the barriers for small businesses to adopt robots<br>
- Efficiency: Lowering the computational load and computer vision complexities by using edge-based sensors<br>
- Scientific experimentation: Custom mounts and holders for measuring instruments and assembly<br>
- Repeatability: Parts that can be made on a 3D printer or CNC, and can be assembled by others from almost anywhere in the world<br>
- Compatibility: MKTR EIC2 series can be used for ROS/ROS2 projects and also works with GyroPalm's gesture control. It also bridges the world of microcontrollers with the world of industrial robotics.<br>

### Disclaimer
The parts involved in this project may involve making modifications to your existing robot. This will require that you have basic knowledge working with electronics and robotics. These parts may be experimental and subject to change without notice. The author is not responsible and shall not be held liable for any damages or injuries as a result of attempting any part of this project. By downloading or using these resources, you agree to perform this project at your own risk.

## Designs

Designs of the MKTR EIC2 and EIC1 series are described. In both version, the author will refer to two pieces that fundamentally make up the term "end-effector". The **first piece** is the plate that mounts on top of the selected robot, which is called the "base mount" or "plate mount". The **second piece** is the gripper or holder that the robot uses to pick up an object, which is called the "gripper" or "attachment". The end-effector is functional when it involves both the first and second pieces are mechanically coupled together and the operator is able to electrically control the attachment. 

### Gripper Logic
Industrial robots often provide a voltage (and logic) supply of 12V or 24V. Some gripper designs that use one or more servo motors or sensors may require a couple "middle pieces" to accommodate this as such technology operates on 5V. The first piece would be a [buck converter or step-down regulator](https://www.amazon.com/gp/product/B076P4C42B/) that can take in 24V DC and output 5V. The second piece would be a 5V microcontroller that is capable of providing a PWM signal to one or more servo motors. Additionally, this microcontroller may be tasked with fetching data from one or more I2C sensors. For the purpose of MKTR EIC2, we chose the [M5StickC Plus](https://www.amazon.com/M5StickC-Plus-ESP32-PICO-Mini-Development/dp/B08VGST8LJ/) which features an ESP32 onboard. This selection was made also because the M5StickC enables to users to move the gripper using wireless control options such as GyroPalm. The GyroPalm team provides additional libraries for solutions that are tested to work with the wearable technology.

### Manual Tool Switching (v1)
![EIC1](https://raw.githubusercontent.com/dominicklee/MKTR-EIC2-Series/master/images/EIC1.jpg)

The MKTR EIC1 is the predecessor of the EIC2. The EIC1 has a quick-change mount design that involves interchangeable attachments that can be detached by removing an M3 screw of 16mm length or more. This version does not require electrical attachments between the robot and base mount. A robot attachment can be slotted into the base mount and mechanically secured by inserting an M3 set screw.

### Electromagnetic Tool Switching (v2)
![EIC2](https://raw.githubusercontent.com/dominicklee/MKTR-EIC2-Series/master/images/EIC2.jpg)

The MKTR EIC2 is the next-generation solution for affordable automatic tool-switching. The EIC2 starts with a base mount that contains an electromagnet secured flush within the mount. This electromagnet is attached to a 5V regulator that can take in voltages between 5-24V from the robot arm that it is attached to. When the robot platform provides a "high level" voltage, the electromagnet turns on and will be mechanically coupled to the gripper. Turning the pin off will released the gripper.

Both the UR series and the Elephant MyCobot Pro series use M8 aviation connectors to provide auxiliary power and logic in their robot arms. However, take note that the pin mappings in each robot's respective datasheet since they are both different. This is especially important because the pin mappings are proprietary and have different logic levels. The UR series requires an M8 female connector while the Elephant MyCobot Pro series requires an M8 male connector.

In order for the robot arm to reliably pick up and "mount" to various attachments using waypoints or fixed poses, the attachments must be properly placed on a rig or rack in a fixed position. MKTR EIC2 has some rack designs that can be used.