# DUBUS - Dublin Bus Trips :bus::bus::bus:



# :loudspeaker::loudspeaker::loudspeaker: IMPORTANT NOTE :loudspeaker::loudspeaker::loudspeaker:

**The below provides a short overview of the project + an installation guide. 
For the full descriptions, explanations and such please see [Lab4_Main](./Lab4_Main.html)**





Table of contents
=================

<!--ts-->
  * [Project Overview](#project-overview)
  * [Usage](#usage)
  * [Installation](#installation)
  
<!--te-->


Project Overview
================

In this project we presnt our application.

The first part of the application includes an interactive map that displays the journeys with congestion, from uploaded stream or batch bus data.

![App Preview1](https://drive.google.com/uc?id=14B5RuYNOmYzgGg-8bkhVkZMxHaiNLVV4)

### Link to our application: [DUBUS - Dublin Bus Trips - congesntion](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/1325942436209506/dashboard/1325942436209514/present)

The second part of the application includes modern-day data exploration tools, bundled in a convinient interface.

Part of the app:
![App Preview2](https://drive.google.com/uc?id=12eZIJ2J3cffro4nQCXi-IHiD2eXfxUjx)


### Link to our application: [DUBUS - Dublin Bus Trips - Analytics](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/2483473424244723/dashboard/1109751670127317/present)

## Notes:
We provide full explanations on how to set up and get the app up and running on **your** system as well.

However, **be aware!** There are a lot of steps that need to be taken in order to allow everything (DataBricks, Kibana, ElasticSearch) to work and communicate with each other.

For example, 
- we tested the system on specific versions of Spark, DBR, Elastic, Kibana, VM OS and such, and cannot provide guarentees for other software versions.
- DataBricks requires embedded webpages to support the HTTPS standard for secure connections. Therefore, you must set up a SSL Certificate on your VM for it to work.

Additionally, for both usage on your system or on ours:

1. As we are displaying our app inside the Databricks, you must have a valid Databricks account inorder to interact with the app. 
2. The server must be on for the app to work.
3. Due to security limitations, first-time visitors must first open [this link](https://da2020w-0001.eastus.cloudapp.azure.com:5601) in their browser, allow the necessary permissions, and only then the app will be displayed correctly.
4. To avoid reruning the whole process on changes in filters, open the [databricks notebook Part1](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/1325942436209506/command/2483473424243540) and [databricks notebook Part2](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/2483473424244723/command/1109751670127311)  make sure that the databricks widgets option in the notebook is set to `on_widget_change: do nothing`


Usage 
=====

The project consists of multiple notebooks that work and interact together.

- *[Lab4_Main](./Lab4_Main.ipynb)*  includes explanations and descriptions about Part 1 (Preprocessing & App) and Part 2 (EDA, Article and App).

- *[Lab4_Preparations](./Lab4_Preparations.ipynb)* consists of the preprocessing part, in which we also train and save the ML model, and the relevant helper models (indexer and encoder, for categorical variables).

- *[Lab4_UI_part1](./Lab4_UI_part1.ipynb)* - The front-end of the first part of our App.

- *[Lab4_UI_part2](./Lab4_UI_part2.ipynb)* - The front-end of the second part of our App.

- *[Lab4_functions](./Lab4_functions.ipynb)* includes all the functions we used through out the project. Includes back-end connection functions (such as connecting to Elastic) as well. 

- *[Lab1](./Lab1.ipynb)*, *[Lab2](./Lab2.ipynb)*, *[Lab3](./Lab3.ipynb)* - all the notebookes from the previous tasks. In these notebookes you can reproduce some indices we created during the project. 


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
   
If this is your first time running the app, you will need to set up the Elastic indices. 

To do so, follow *[Lab1](./Lab1.ipynb)*, *[Lab2](./Lab2.ipynb)* and *[Lab3](./Lab3.ipynb)* to reproduce the relevant indices. 

Additionally, you might need to modify the Kibana dashboards to match the newly created indices, as these are configured per installation. 

Finally, run *Lab4_UI_part1.ipynb* and *Lab4_UI_part2.ipynb*.


Once the app is up and running you can use it easily, just follow the in app instructions.



Installation
============

The installation consists of two parts - Frontend & Backend.
We assume that databricks and the VM are configured to be able to communicate with each other securely.

### Frontend

Databricks - Tested on Databricks Runtime Version `6.4` which includes Apache Spark `2.4.5`, Scala `2.11` and python `3`. Specifically `pip 19.0.3`, `python 3.7.3` and `git 2.7.4` were used.

To install the app, on Databricks:
1. Clone the repository into your databricks workspace - `git clone https://github.com/scaperex/DUBUS.git` 
2. Assuming `pip` and `python` are installed (overwise install them), install the necessary packages by `pip install -r requirements.txt`
3. Install additional components - ElasticSearch-Spark. To install the Elastic connector (sink) follow the [DataBricks Documentation](https://docs.databricks.com/libraries/cluster-libraries.html). Specifically, our code uses `elasticsearch_spark_20_2_11_7_9_3.jar`. Download and install it from [Elastic](https://www.elastic.co/guide/en/elasticsearch/hadoop/current/install.html).



### Backend
This part is done on your VM (e.g. Azure).

1. Create an empty directory - `mkdir dubus_app`
2. cd into it - `cd dubus_app`
3. Install [docker](https://www.docker.com/) and [docker compose](https://docs.docker.com/compose/):
   ```bash
   sudo apt-get remove docker docker-engine docker.io containerd runc
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```
   This uninstalls if already installed, then downloads and installs both Docker and docker-compose.
4. Note: Databricks requires embedded webpages to support the HTTPS standard for secure connections. Therefore, you must set up a SSL Certificate. For production environments see for example [cloudflare](https://www.cloudflare.com/ssl/). For development enviroments you may create a certificate for example with [elasticsearch-certutil](https://www.elastic.co/guide/en/elasticsearch/reference/7.10/certutil.html) and save the key as `kibana-server.p12` in the same directory as the project file. 
5. The docker-compose.yml contains all the configurations needed to setup the elastic and kibana containers, network and volumes. Run it with:
   ```bash
   sudo docker-compose up &
   ```
