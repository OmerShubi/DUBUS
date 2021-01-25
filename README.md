# DUBUS - Dublin Bus Trips :bus::bus::bus:



## :loudspeaker::loudspeaker::loudspeaker: IMPORTANT NOTE :loudspeaker::loudspeaker::loudspeaker:

**The below provides a short overview of the project + an installation guide. 
For the full descriptions, explanations and such please see the [Main notebook](https://scaperex.github.io/DUBUS/) 
or download it from [Lab4_Main](Lab4_Main.html)!** :lotus_position:





Table of contents
=================

<!--ts-->
  * [Project Overview](#project-overview)
  * [Usage](#usage)
  * [Installation](#installation)
  
<!--te-->


Project Overview
================


The first part of the application includes an interactive map that displays the journeys with congestion, from uploaded stream or batch bus data.

<img src='assets/App1.jpeg' width=600/>
 

The second part of the application includes modern-day data exploration tools, bundled in a convenient interface.

Part of the app:

<img src='assets/App2.png' width=600/>


Usage 
=====

The project consists of multiple notebooks that work and interact together. For the full descriptions, explanations and such please see [Main notebook](https://scaperex.github.io/DUBUS/).

- *[Lab4_Main.ipynb](code/Lab4_Main.ipynb)* includes explanations and descriptions about Part 1 (Preprocessing & App) and Part 2 (EDA, Article and App).

- *[Lab4_Preparations.ipynb](code/Lab4_preparations.ipynb)*, *[Lab4_UI_part1.ipynb](code/Lab4_UI_part1.ipynb)*, *[Lab4_UI_part2.ipynb](code/Lab4_UI_part2.ipynb)* and *[Lab4_functions.ipynb](code/Lab4_functions.ipynb)* hold the code used in the project. 

- *[Lab1.ipynb](code/Lab1.ipynb)*, *[Lab2.ipynb](code/Lab2.ipynb)*, *[Lab3.ipynb](code/Lab3.ipynb)* - all the notebooks from the previous tasks. Used to reproduce helper indices. 


After performing the [installation steps](#installation), here is how to use the app in real time.

Prerequisites:
1. Databricks Cluster: should be turned on
2. VM:
   - Should be turned on
   - Then, 
   ```bash
   cd dubus_app
   sudo docker-compose up &
   ```
   
If this is your first time running the app, please refer to **first time setup** part in the [installation guide](./INSTALLATION.md#first-time-setup).
It also includes 
Once the app is up and running you can use it easily, just follow the in-app instructions. 

Notes,

1. As we are displaying our app inside the Databricks, you must have a valid Databricks account inorder to interact with the app. 
2. The VM server must be on for the app to work.
3. There are security limitations. Please see the **notes section** in the [installation guide](./INSTALLATION.md#notes) on how to deal with them.

Installation
============
We provide full explanations on how to set up and get the app up and running on **your** system as well.

For the full installation guide please see the [installation guide](./INSTALLATION.md)

However, **be aware!** There are a lot of steps that need to be taken in order to allow everything (DataBricks, Kibana, ElasticSearch) to work and communicate with each other.
