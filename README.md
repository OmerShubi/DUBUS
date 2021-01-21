# DUBUS - Dublin Bus Trips :bus::bus::bus:

Table of contents
=================

<!--ts-->
  * [Project Overview](#project-overview)
  * [Usage](#usage)
  * [Installation](#installation)
  
<!--te-->


Project Overview
================

In this part we define a task over the Dublin dataset based on one of the paper *Overview of Data Exploration Techniques* by Stratos Idreos (Harvard), Olga Papaemmanouil (Brandeis) and Surajit Chaudhuri (Microsoft Research). 

We present an application that allows the user to do **modern-day data exploration**. 

More spcifically, we provide a collection of advanced visualization & data exploration tools, bundled in a convinient interface. 
In part it allows the user to: 
1. Dynamic overview of the data that they uploaded via an interactive dashboard.
2. Perform further investigation of the data in an intuitive, code-less way, using state-of-the-art tools.
3. Quick query result estimation and visualization using sampled data.


### Link to our application: [DUBUS - Dublin Bus Trips - Analytics](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/2483473424244723/dashboard/1109751670127317/present)

Notes,

1. As we are displaying our app inside the Databricks, you must have a valid Databricks account inorder to interact with the app. 
2. The server must be on for the app to work.
3. Due to security limitations, first-time visitors must first open [this link](https://da2020w-0001.eastus.cloudapp.azure.com:5601) in their browser, allow the necessary permissions, and only then the app will be displayed correctly.
4. To avoid reruning the whole process on changes in filters, open the [databricks notebook](https://eastus.azuredatabricks.net/?o=6694791539123117#notebook/2483473424244723/command/1109751670127311) make sure that the databricks widgets option in the notebook is set to `on_widget_change: do nothing`


The project consists of multiple notebooks that work and interact together.

- *[Lab4_Main](./Lab4_Main.ipynb)*  includes explanations and descriptions about Part 1 (Preprocessing & App) and Part 2 (EDA, Article and App).

- *[Lab4_Preparations](./Lab4_Preparations.ipynb)* consists of the preprocessing part, in which we also train and save the ML model, and the relevant helper models (indexer and encoder, for categorical variables).

- *[Lab4_UI_part1](./Lab4_UI_part1.ipynb)* - The front-end of the first part of our App.

- *[Lab4_UI_part2](./Lab4_UI_part2.ipynb)* - The front-end of the second part of our App.

- *[Lab4_functions](./Lab4_functions.ipynb)* includes all the functions we used through out the project. Includes back-end connection functions (such as connecting to Elastic) as well. 

Usage 
=====
Prerequisites:
1. Databricks Cluster should be turned on
2. VM should be turned on

Then,
On VM:
```bash
cd dubus_app
sudo docker-compose up &
```

TODO Add how to use

TODO More images and explanations
![App Preview](https://drive.google.com/uc?id=14B5RuYNOmYzgGg-8bkhVkZMxHaiNLVV4)


Installation
============

The installation consists of two parts - Frontend & Backend.
We assume that databricks and the VM are configured to be able to communicate with each other securely.

### Frontend
1. Clone the repository into your databricks workspace - `git clone https://github.com/scaperex/DUBUS.git` 
2. Assuming `conda` is installed, install the necessary packages by `conda create -f enviroment.yml`
3. Activate the environment with `conda activate <env_name>`
4. Install additional components - ElasticBridge TODO 

Tested on TODO

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

Note: 
Databricks requires embedded webpages to support the HTTPS standard for secure connections.
Therefore, you must set up a SSL Certificate. For production environments see for example [cloudflare](https://www.cloudflare.com/ssl/).
For development enviroments you may create a certificate for example with [elasticsearch-certutil](https://www.elastic.co/guide/en/elasticsearch/reference/7.10/certutil.html) and save the key as `kibana-server.p12` in the same directory as the docker-compose file.


TODO - 
1. Create requirement.txt / env.yml
2. How to install EVERYTHING
3. Think of params that need to be changed in CODE

