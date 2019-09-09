# URDF Juggle package [![License: MIT](https://img.shields.io/badge/license-MIT-red.svg)](https://spdx.org/licenses/MIT.html)

This package contains helpfull Xacro macroses for URDF.
Look in `example` folder for usage examples.

## Colored link
Macros `colored_link` allows to make link with identical visual settings both in rviz and gazebo.
Specify attributes `color` and `transparency` and put tag `visual` inside macros but without tag `material`. Other tags you can put in tag `other`.
```xml
<xacro:colored_link name="box" color="0 0.6 0" transparency="0">
    <visual>
        <geometry>
            <box size="1 1 1" />
        </geometry>
        <origin xyz="0 0 0" rpy="0 0 0" />
    </visual>
    <other>
        <collision>
            ...
        </collision>
        <inertial>
            ...
        </inertial>
        ...
    </other>
</xacro:colored_link>
```
![](colored_link.png)

## Inertia
Macroses `box_inertia`, `cylinder_inertia` and `sphere_inertia` contains tag `mass` and appropriate inertia matrix based on mass and geometry.
```xml
<link name="box">
    ...
    <inertial>
        <origin xyz="0 0 0" rpy="0 0 0" />
        <xacro:box_inertia mass="1000" size="0.8 0.8 0.8" />
    </inertial>
    ...
</link>
```
![](inertia.png)

## Simple link
Macroses `simple_box`, `simple_cylinder` and `simple_sphere` helps to shorten the code of links having similar geometry for visual, collision and inertia tags.
#### Usual link
```xml
<link name="box">
	<visual>
		<geometry>
			<box size="1 1 1"/>
		</geometry>
		<origin rpy="0 0 0" xyz="0 0 0"/>
		<material name="box_material">
			<color rgba="0 0.8 0 0.7"/>
		</material>
	</visual>
	<collision>
		<geometry>
			<box size="1 1 1"/>
		</geometry>
		<origin rpy="0 0 0" xyz="0 0 0"/>
	</collision>
	<inertial>
		<origin rpy="0 0 0" xyz="0 0 0"/>
		<mass value="1000"/>
		<inertia ixx="166.666666667" ixy="0" ixz="0" iyy="166.666666667" iyz="0" izz="166.666666667"/>
	</inertial>
</link>
<gazebo reference="box">
	<visual>
		<material>
			<ambient>0 0.8 0 1</ambient>
			<diffuse>0 0.8 0 1</diffuse>
			<specular>1 1 1 1</specular>
			<emissive>0 0 0 1</emissive>
		</material>
		<transparency>0.3</transparency>
	</visual>
</gazebo>
```
---
#### Simple link
```xml
<xacro:include filename="$(find urdf_juggle)/simple_link.urdf.xacro" />
<xacro:simple_box
		name="box"
		color="0 0.8 0"
		transparency="0.3"
		size="1 1 1"
		mass="1000"
>
	<origin xyz="0 0 0" rpy="0 0 0" />
	<other />
</xacro:simple_box>
```