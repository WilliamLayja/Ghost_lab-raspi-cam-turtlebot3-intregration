# Ghost_lab-raspi-cam-turtlebot3-intregration
//In the starting process for this project we had lots of issues. One thing to understand is that we found to main ways to go about this integration. First thing you need to take note of is the physical parts that you have. In our case, we had a Turtlebot 3 that was using a Rasberru Pi 3B+ that was attached to a Lidar sensor, and an OpenCR that helps in wheel movement.

//The next thing you need to do is understand a basics of Ros 1 & 2 as well as understand the general basics of how to use the terminal on a computer. The terminals in Windows 10 & 11 will unfortuently not be very helpful when starting this inigration unfortunetly due to Windows having very little to no support for ROS. This is why we reccomned using a virtual machine (VM) of Linux the best way to go about it. If you don't know how to install a virtual machine into your computer I would recommend looking on the internet for any Virtualbox (VB) tutorial. 

//Heres a link to a video incase you can't find one that is helpful. https://youtu.be/b866-7Y_0KQ?si=Ga1pSnI6eOk2_-t0. 
//after you have install VB, you have to find an operating system (OS) that fits your needs. In our case, we use Ubunut which is a linux based OS. However, one big caviate that we found is that the version of Ubuntu matters very much to the cameras inegration. You see, the swarm tower that we have in the Ghost Lab runs on Ubuntu version 18.04. This is relatively older verson of Ubuntu that doesn't support ROS 2. Which means all of the turtlebots that we have in the lab are all running on ROS 1 Noetic/ Melodic. We eventually found a way to make the camera inigration work while on ROS 1, but we found it to be weird, and so I took the liberty of making as leat one of the turtlebots in ROS 2. This does mean that if we ever wanted to control this specific turtlebot with the swarm tower we would have to upgrade the OS from 18.04 to something that supports ROS 2, in the case of the turtlebot documentation, Ubuntu 22.04.

#Intigration via ROS 1
//For ROS 1 integration which is what the already installed on the robots, your need to intsall a ubuntu 18.04 VM onto your computer. Fortunutly, the turtlebot3 documentation basicaly just gives you a step by step process on what you need to do for this.
//Here is the link to the documentation. https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup.
//Make sure that when you are ready to instal the ROS packages, that you are in the Noetic tab of the documenation to make sure that you download the right verson of ubuntu as well as not having any issues when downloading all the neccessary packages. For the setup of your VM, start under the Quick Sart Guide- 3.1 PC Setup page. The rest of the setup documentation is for the robot it'self and the turtlebots in the Ghost Lab already have eveyrthing installed. 

//Now that you have all of your PC packages installed, the only other thing you can do before moving onto the the Ghost Labs Quick Start Guide/demo is to make sure that the robot knows that your computer is the "master" by telling it that it should be conecting to your IP.
//to know what your IP is, in the termial type "ip a"
//After finding out what your IP is, follow steps 1-5 on Ghost Labs Quick Start Guide/demo.
//To deviate from the demo, type "ls"
//Type nano ./. bashrc
//Use the arrow keys to navigate to where it says export ROS_MASTER_URI=http://x, 
//Control S (to save) and Control X (to exit the nano)
//continue through the Quick Start Guide/demo instuctions.

//Finally getting to the camera:
//I found that the only was to see anything from the camera in ROS 1 is to look at a photo, I could not find a live feed unfortunetly
//Make sure the robot is powered off for this part.
//Interms of the physical parts, we used a rasberry pi V2 camera. To connect this camera physically all that needed to be done as lift a little bracket on the raspberry pi and make sure that the pins on the camera aline with the ones on the raspi. Don;t forget to lock the bracket back into place to secure the camera.
//Unfortunetly, the is no indicator that the camera is connected to the raspi sucessfully, but if you do these next commands, it should be working.
//type ls and look for the take_picture.py library.
//type python3 take_picture.py
//When thats done it has offically taken a photo, but you need to set a place to save it on the device. In order to do tha you need to find a folder to place the photo in on your computer and type that directory into the next line of code. 
scp ubuntu@192.168.0.11[1-4]:home/ubuntu/captured_image.png (your directory name)
When you have done this, the photo will save to your computer and you can use it like it were a regular PNG file!
Integration Via ROS 2
Using ROS 2 gives you more ways of learning to integrate the camera. Instead of installing Ubuntu 18.04, you will install 22.04 on your VM. The documentation for the Turtlebot3 also has this process step by step.

Make sure you follow the steps in the Humble tab for this one.
Don't forget that the turtlebots are on ROS 1 at the moment, so you will also need to go through the 3.2 & 3.3 pages of the documentation for setting up the Raspberry Pi and the OpenRC for the new version of ROS. It is best to do this process on a new micro SD card with a minimum of 16 GB to make sure that we don't look the ROS 1 code and so we have enough space for the new packages that help ROS 2 run. 
Unlike the documentation for ROS Noetic, ROS Humble integrates the Raspberry Pi camera from the very start, so in the documentation, they have the packages ready for you to copy and paste into your terminal. It is located in a drop-down menu under
Using the v4l2-camera package to use the Pi Camera
I have tried using the
Using the camera-ros package to use the Pi Camera
But that one failed to work well.
After you have gone through all the package installations, make sure that the motors turn.
If the motors turn, you are ready to start the interface for the camera. Which can be brought up via the code in the documentation on page 3.5.
