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
5. The docker-compose.yml contains all the configurations needed to setup the elastic and kibana containers, network and volumes. Under the `volumes` section, update the paths according to your host system configuration if needed. Then, run it with:
   ```bash
   sudo docker-compose up &
   ```
   
   
First Time Setup
================

If this is your first time running the app, you will need to set up the Elastic indices.

To do so, follow *[Lab1](code/Lab1.ipynb)*, *[Lab2](code/Lab2.ipynb)* and *[Lab3](code/Lab3.ipynb)* to reproduce the relevant indices. 

Additionally, you might need to modify the Kibana dashboards to match the newly created indices, as these are configured per installation. 

Additionally, you might need to modify some paths, such as the IP of the VM, in the *[Lab4_functions](code/Lab4_functions.ipynb)* `Global Parameters` section.

Finally, run *Lab4_UI_part1.ipynb* and *Lab4_UI_part2.ipynb*.



Notes
=====
- we tested the system on specific versions of Spark, DBR, Elastic, Kibana, VM OS and such, and cannot provide guarentees for other software versions.
- DataBricks requires embedded webpages to support the HTTPS standard for secure connections. Therefore, you must set up a SSL Certificate on your VM for it to work.
- As we are displaying our app inside the Databricks, you must have a valid Databricks account inorder to interact with the app.
- The server must be on for the app to work.
- Due to security limitations, first-time visitors must first open the Kibana interface (VM IP on port `5601`) in their browser, allow the necessary permissions, and only then the app will be displayed correctly.
- If you encounter a situation where changes in filters result in reruning the whole process, open the databricks notebook and make sure that the databricks widgets option in the notebook is set to `on_widget_change: do nothing`.
