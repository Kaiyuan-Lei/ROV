**==Mission-Specific Design==**



## **i. The design and features of the  electric manipulator arm **

## ![image-20220815122249233](K:\Git\pics\image-20220815122249233.png)

The electric manipulator is used to automate the object grasping, in tasks one and two, required to place, repair, and remove the operation of pipes, fishing nets, and some underwater debris as required. The design needs to be as compact as possible in order to adapt to the most varied working conditions.


Our team developed a single-degree-of-freedom manipulator, driven by a high-power output waterproof servo motor, mounted vertically on the ROV body. We then realized that this approach might not be efficient during ROV deployment and retrieval. Therefore, we added an additional degree of freedom to the manipulator

It can be easily moved from the vertical to the horizontal position. In addition, the torque of the servo motor may not be enough and the locking current is too high. Therefore, the DC motor used is used for the large torque requirement task.

As one *of* the core components of the ROV, the electric robotic arm must meet the ability to achieve free operation in a variety of environmental conditions. That is why the structural design of the robotic arm is particularly important. Since its jaws need to grasp and pick up objects (such as cannons) quickly, it is designed in an arc shape with a circular diameter of about 100 mm. Meanwhile, the manipulator has two degrees of freedom. It can be switched between vertical and horizontal mounting modes.



​    

## **ii. Object detection system for motor control**

***![Picameras2_1500](K:\Git\pics\Picameras2_1500.jpg)***

In an effort to inspect the underwater in real time, the team has installed a V2.1 Raspberry Pi camera 2.1 module on the ROV. This camera module is aimed to monitor and control the motion of the servo motor.   Meanwhile, the communication process / data transmission is achieved through a building control under QGC (QGroundControl), which provides an interface for the team to monitor the motion of the motor in real time.  Through this digital connection, the camera is enabled to conduct tasks that also seek photographs as visual evidence for further investigation. 



## ***iii.  Raspberry pi Control logic for servo motor **

With visual aid, the operation status of the servo motor could be adjusted. By the fundamental working principle of a servo motor, a PWM control signal must be sent to the pilot circuit so that a angle-modulated  signal could be produced and to power the motor, as if exemplified in this flowchart.

![image-20220817013727387](../pics/image-20220817013727387.png)

​                           *fig - Basic working principle of servo motor*

The servo motor has three connection lines: ground, power and control (signal) lines, with the middle line usually being the power line. By sending a pulse width modulation (PWM) signal through the control line, the servo motor can be controlled to rotate to an angle. To extend this principle to key of a control logic, we must ensure This PWM signal must be sent periodically, otherwise the servo motor will turn to an arbitrary angle. Normally, the PWM signal period for controlling the servo motor is 20ms (50HZ) and the width is between 0.5ms-2.5ms (corresponding to the minimum and maximum angles).

　However, the RPi. GPIO library only provides the function to control the duty cycle of PWM signal, and some conversion is needed to control the angle of servo motor. For other rotation angle of servo motor angle-duty cycle conversion can be followed in the same order. In essence, the Raspberry Pi control Raspberry Pi is actually the control of the duty cycle of the PWM signal.



## iv.  *Computer vision system for image processing* 

Another camera we installed on the front side of the ROV is used for digital image processing. We installed OpenCV-contrib-python to fulfill tasks where the CV system is required to distinguish a cluster of  objects with distinct features. 

![8ba30222285289970b83fc41cc1cf9f](../pics/8ba30222285289970b83fc41cc1cf9f.jpg)



  In order to display the image captured from the camera module, we need to use four of the functions to process a am image properly:



| *cv2.imshow()*               | -display an image                                       |
| ---------------------------- | :------------------------------------------------------ |
| ***cv2.waitKey()***          | -**control the timing of the image display**            |
| ***cv.destoryAllWindows()*** | **-close all windows displayed by the current program** |
| ***cv2.imwrite()***          | **-store an image**                                     |

To compare the characteristics of an array of images, we could directly check the properties of the pixel array. Two of the methods that we attempted are to compare by either shape or size of the images. 

1). By shape - The array of color images is a three-dimensional array that can be represented as (a,b,3). a indicates the number of pixel channels in the vertical direction (vertical pixels), b indicates the number of pixel channels in the horizontal direction (horizontal pixels), and 3 indicates that each pixel has three color channels. 

2). By size - Indicates the number of color channels the image has. For color images, the number of pixels is a × b, and the number of color channels is a × b × 3.



## iv. *Fry release system*

![image-20220817001812480](../pics/image-20220817001812480.png)

​       To approximate the size of a fish cohort in task 2.3, a fry release system is needed when freeing large amount fry. This system is constituted of three major components including a motor, a disk and a PMMA tube. In order to prevent water influx, one side of the tube is sealed and the disc is connected to the motor which is used to open or close the other side of the tube. Before its departure, the device should be turned upside down with fish in the device. Next,  we place fish into the dive and use the motor to rotate the disk to close the tube. Once the device reaches designated spot, the motor drives the disk to rotate. The tube will be open thereafter, and fish will be released into the area below the tube. 



## ***v.  Smart float***

​       *To design a profiliing float is not as smooth as expected for the team...





## *vi. Micro-ROV* 

By using Engineering Club's self-driven micro-rov, we were able to detect in real time the flow of turbid water in a potentially damaged drainage pipe. Due to its capsule-shaped design structure, the rounded edges on the front and back of this ROV allow it to move smoothly along the drain without damaging it or jamming it.

We installed a single channel optical video signal transmitter with RS485 data receiving port inside the mini-ROV for video and control signal transmission between the mini-ROV and the ROV. The signal is then received by installing an Arduino Nano to output PWM control ESC.

We used 8 AA alkaline batteries in series as the on-board power supply, outputting 12 V. Meanwhile, the 2-layer battery holder was mounted in a 4 cm diameter syringe with a removable piston at the rear of the syringe, which prevents high pressure hydrogen from being generated inside the battery and acts as a pressure release. Since most on-board devices have a 5V input voltage, a DC-DC 5V buck converter is connected in parallel with the battery and ESC.

 

