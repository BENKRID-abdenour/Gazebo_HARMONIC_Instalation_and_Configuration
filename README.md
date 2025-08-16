# Gazebo Harmonic Installation Guide for ROS 2 Jazzy on Ubuntu 24.04 LTS

This guide explains how to **install Gazebo Harmonic** for use with an existing ROS 2 Jazzy installation on Ubuntu 24.04.

---

## Table of Contents
- [Overview](#overview)
- [System Requirements](#system-requirements)
- [Install Gazebo Harmonic](#install-gazebo-harmonic)
- [Additional Packages](#additional-packages)
- [Verify Installation](#verify-installation)
- [Uninstall](#uninstall)

---

## Overview
Gazebo Harmonic is the latest supported Gazebo release compatible with **ROS 2 Jazzy**.  
This guide provides step-by-step instructions to install it using Ubuntu `.deb` packages.

![Gazebo_HARMONIC](Images/Gazebo_HARMONIC.jpeg)

---

## System Requirements
- Ubuntu 24.04 (Noble) 64-bit  
- ROS 2 Jazzy already installed  
- Minimum 8 GB RAM recommended  
- Internet connection  
- `sudo` privileges  

---

## Enable Gazebo Repositories
First, ensure that your system can access the Gazebo package repositories:

```bash
sudo apt update && sudo apt install software-properties-common
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" > /etc/apt/sources.list.d/gazebo-stable.list'
wget https://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
sudo apt update
```

## Install Gazebo Harmonic

ROS 2 Jazzy introduces vendor packages in the ROS repository, which provide all the necessary libraries for Gazebo Harmonic. To install the latest version of Gazebo and integrate it with ROS 2 Jazzy, simply execute the following command after sourcing your ROS environment:

```bash
sudo apt-get install ros-jazzy-ros-gz
```
Note: On certain systems or configurations, this command may fail with a message such as "Unable to locate package ros-jazzy-ros-gz" if the ROS repository has not been properly added or updated.

---

## Additional Packages

In certain situations, users have reported that although ROS 2 Jazzy and Gazebo Harmonic are installed, they cannot find a working tutorial to successfully integrate their ROS-based robot into Gazebo. Therefore, it is imperative to manually install some additional packages to resolve this issue.


```bash
sudo apt-get install ros-jazzy-gz-ros-pkgs
sudo apt-get install ros-jazzy-gz-ros2-control
```
These represent the current adaptations of the ROS Gazebo packages, where the older gazebo-ros-pkgs have been replaced by the new gz-ros-pkgs.

## Verify Installation

Test if the simulator is working by running:

```bash
source /opt/ros/jazzy/setup.bash
gz sim --help
```

To verify if Gazebo is already integrated with ROS 2 Jazzy, execute the following commands in your terminal:

```bash
source /opt/ros/jazzy/setup.bash
ros2 pkg list | grep ros_gz
```

If the returned result looks like this:

```bash
ros_gz 
ros_gz_bridge 
ros_gz_image 
ros_gz_interfaces 
ros_gz_sim 
ros_gz_sim_demos
```
This means that ROS and Gazebo are successfully connected.

---

## Uninstall

Remove Gazebo and ROS 2 Gazebo packages:

```bash
sudo apt remove gazebo11 libgazebo11-dev ros-jazzy-gazebo-* && sudo apt autoremove
```

Remove Gazebo repository (optional):

```bash
sudo rm /etc/apt/sources.list.d/gazebo-stable.list
sudo apt update
```
