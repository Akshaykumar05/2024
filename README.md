# Work-2024-25

Yeahh!! So finally we are here in 2024....
Let's documents our learnings on the go..

## Index
1. Keycloak and HAProxy
2. IP Address
3. VPN 
4. Server Reboot
5. Inventory files updation
6. Keys Generation (Public/Private)
7. Architectural Diagrams
8. Centralised Log Server (Rsyslog)
9. Tomcat Installation
10. VNC configuration.
11. Netbox
12. VPN configuration on VM.
13. Podman Unshare
14. Docker Private Registry
15. Podman container with Php 8.2 version
16. On-prem Infrastructure migration on Cloud
17. Rsyslog configuration
18. Gitlab Upgradation
19. Nexus repo creation
20. Manual Deployment : eDetection (10.142.36.130)
21. Graylog Configuration
22. CICD Pipeline Creation (eDetection Server 10.142.36.130)
23. Port issue (Port down on any Server)
24. Space utilization issue (Disk space low < 85 %)
25. Load issue on a Server (Load average high)
26. Tomcat installation and Configuration
27. Php Application (RHEL, httpd, MySql)
28. Build CI/CD Pipeline
29. Apache Kafka
30. Swap memory (isue resolve)
31. ELK
32. K8s Deployment (Pariwanseva)
33. Docker build (Pariwanseva)
34. Logs check for k8s nodes (paidnr-app)
35. Container images migration
-----------------------------------------------

### Case Studies
## 1. Keycloak and Haproxy local installation and update the version of Haproxy (from 1.8.31 to 2.0) without deleting the data.
   * Make a container on docker and run HAproxy on it, Same for the Keycloak.
   #### Keycloak
   * is an open source software product to allow single sign-on with identity and access management aimed at modern applications and services.
   * Keycloak is the standalone tool for identity and access management, which allows us to create a user database with custom roles and groups.
   #### HAproxy
   * HAProxy is a free and open source software that provides a high availability load balancer and Proxy for TCP and HTTP-based applications that spreads requests across multiple servers.
     
## 2. IP address detail list of Staging servers with the information.

------------
  ## 3. VPN 
  * [Documentaion of VPN configuration on Uuntu](https://vpn.nic.in/resources/manuals/Manual_for_configuring_VPN_in_Ubuntu_and_RedHat.pdf)

   
## 4. Reboot a Server (Staging: 151)
   * Here we need to reboot a server of Staging environmeet with the specified IP addrees.
   ### Steps:
   * Stop haproxy (systemctl stop haproxy)
   * Stop docker
     ``docker ps -a
     ``
     ``docker stop cont_name
     ``
   * Stop Tomcat
     ``kill all -a
     ``
   * Reboot: ``init -6``
     
   ### After doing this all:
   * Do up all the services: dcoker container, Tomcat and haproxy.

-------------------

  ## 5. Updation of Inventry Files

  ## 6. Creation of Public and Private Keys
   * Make user as a root user using ``sudo -i`` command and run the command ``ssh-keygen``.
   * This will generate Public/Private rsa key pair.
   ![image](https://github.com/user-attachments/assets/f32a3d6b-c66e-4d11-aa86-c7d29dd8fdce)


## 7. Centralised Log Server
 ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/a4b724ce-dd56-47cb-afee-49cf9b9f6cff)
 
 * [Detailed Repository](https://github.com/Akshaykumar05/Centralized-Log-Server)
--------------   
## 8. Tomcat installation
 1. Download tomcat file 
 2. Un-tar file
 3. Move file to usr/local/
    * ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/5f61cba2-3830-498f-a915-825b3e5e3a11)
 4. Set up two Tomcat servers and haproxy on VM1.
 5. Restart and check the running status Tomcat1 on port 8081.
 6. Restart and check the running status Tomcat2 on port 8082.
    *  ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/623af010-748b-4641-997a-048147c18820)
   
 7. Check if the Tomcat servers are generating logs.
    1. First go inside the tomcat2 and check the log files.
       * ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/af0fd3c2-ae67-48b2-9b96-eeb5d65b8c75)
       * ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/ef4e13e7-0750-4da0-ab24-21a5cf226770)
--------------------------
## 10. VNC Configuration
* **Virtual Network Computing** (VNC) is a free tool that allows a client to connect to a server, and interact with the desktop of the remote machine. The server-side component listens for connections on TCP port 5900 by default.
* [Blog](https://linuxize.com/post/how-to-install-and-configure-vnc-on-ubuntu-20-04/)

* Install tigerVNC
* ![image](https://github.com/user-attachments/assets/45b3449e-9ba6-4ea0-9f82-0072c599faab)

* VNC password
* ![image](https://github.com/user-attachments/assets/b28115a9-05bf-4b21-b8fb-a990fe351234)

* Now start the VNC server using the vncserver command:
```
vncserver
```


* ![image](https://github.com/user-attachments/assets/20eacdfd-9349-48ad-a45e-1d9f91a362e6)

* You can get a list of all the currently running VNC sessions by typing:
```
vncserver -list
```
![image](https://github.com/user-attachments/assets/37f83cd3-f22b-4d3b-bbe1-0a93b2726405)

* Kill
```
vncserver -kill :1
```
![image](https://github.com/user-attachments/assets/b56efad6-c06d-4f10-904a-5f5ce3323454)

### VPN configuration 
```
sudo ./vpn_install.sh 
```

## 12. Podman Unshare
* Podman unshare is useful for troubleshooting unprivileged operations and for manually clearing storage and other data related to images and containers.
* It is also useful to use the podman mount command. If an unprivileged user wants to mount and work with a container, then they need to execute podman unshare.

## 13. Docker Private Registry
* A Docker private registry is a central place where you can store and manage your Docker images, similar to Docker Hub but within your own controlled environment. Here’s why you might want to use a Docker private registry:

 1. Security and Control
* Sensitive Data: If your Docker images contain proprietary or sensitive data, using a private registry ensures that you have full control over who can access and push/pull these images.
* Internal Use: For organizations, it’s often crucial to keep certain applications or microservices private. A private registry allows you to store these images securely within your network.
  
 2. Performance and Reliability
* Local Network: Hosting a registry on your local network reduces latency, making it faster to pull images during deployment, especially in large clusters or CI/CD pipelines.
* Reduced Dependency on External Services: By using a private registry, you’re not reliant on external services like Docker Hub, which could have outages or be subject to rate limits.
  
 3. Custom Policies and Integrations
 * Access Control: You can define custom access control policies tailored to your organization’s needs, ensuring that only authorized users or systems can interact with the registry.
 * Integration with CI/CD Pipelines: Private registries are often integrated into CI/CD pipelines to automate the process of building, testing, and deploying Docker images.
 4. Cost Efficiency
 * Avoid External Costs: If you’re pushing a large number of images or have a high rate of deployments, a private registry helps avoid potential costs associated with using a third-party service like Docker Hub.
 5. Custom Image Management
 * Image Retention Policies: You can implement policies to automatically clean up old or unused images, helping to manage storage efficiently.
 * Namespace and Tagging: Control how images are named, tagged, and organized, making it easier to manage multiple versions of images across different environments (e.g., development, staging, production).
 6. Compliance and Auditing
 * Auditing: A private registry allows you to track who accessed which images and when, providing valuable auditing capabilities for compliance with industry standards.
 * Regulatory Requirements: In regulated industries, data sovereignty is important. A private registry ensures that your Docker images are stored and managed in compliance with local regulations.
 7. Offline Deployments
 * Air-Gapped Environments: In environments where internet access is restricted (e.g., military, industrial, or isolated systems), a private registry allows you to maintain and deploy Docker images without needing external connectivity.
8. Custom Feature Set
 * Custom Plugins or Middleware: A private registry can be extended with custom plugins or middleware to meet specific requirements, such as automated vulnerability scanning, custom logging, or integration with other internal tools.
Summary
In essence, a Docker private registry gives you full control over how Docker images are stored, accessed, and managed. This is particularly important for security, performance, compliance, and cost control in enterprise environments or when dealing with sensitive data.
-----------

## 14. Podman container with Php 8.2 version
* In this task we have to create a VM with Ubuntu 20.04 install on it. Then we will setup Php 8.2 version and later will integrate with DB PostgreSQL.
  

## 15. On-prem Infrastructure migration on Cloud
* Currently NIC have their on-prem infrastructure, and now the organisation migrating it's infra on Jio Cloud. So We need to migrate everything-- Applications and their servers.
  ### Things need to do for migration: 
* First of all we have to ctreate servers on Cloud and then migrate Tomcat instances of the application on Jio Cloud's servers.
* Log Configuration files transfer: We need to update logs configuraion files of the staging servers to the Cloud servers in their **rsyslog.conf file**.
* Need to creat repository on Cloud servers to save war files of staging servers.
* Create CICD Jenkins pipelines
* Zabbix setup for monitoring servers
* Database connection configuration

-------------------------------

## Server Login
1. Login to Jump server
   
3. login to particular server
   
   <img width="524" alt="image" src="https://github.com/user-attachments/assets/bbcf3be9-cc8c-4db1-8870-fbcdc41beb97">

4. See the available content
   
   <img width="925" alt="image" src="https://github.com/user-attachments/assets/90ea4ba0-0674-4eef-ae08-0b4f30c1bbc2">

6. Check the tomcat and wars.
   
   <img width="653" alt="image" src="https://github.com/user-attachments/assets/6befac22-f3dc-41b1-ab74-94f17094cf7a">

8. Check available tomcats
   
   <img width="924" alt="image" src="https://github.com/user-attachments/assets/7e963512-e6e9-449f-8874-bea4627d6b14">

10. Check logs and wars
    
   <img width="836" alt="image" src="https://github.com/user-attachments/assets/a15973aa-a750-4c59-bc65-7716cd4a89e8">

12. War details
    
   <img width="704" alt="image" src="https://github.com/user-attachments/assets/ffd413e8-9486-4b4f-800f-3f29253fa867">


----------------------------------
### SSL Lab
* We need to check the status and validity date of SSL Certificates (of websites)
* [Website to check domain status](https://www.ssllabs.com/ssltest/)


----------------------------------
## 16. Log-Archive configuration
* Configuration: the rsyslog server (10.242.36.24) and sync the log (application, access log and catalina.out) of eDetection Server (10.242.36.130).
* Create a log rotation script and configure it for log rotation on **Log Central Server** (10.242.36.24) of Production environmenet.
---------------------------
* First login on the Master server (10.242.36.24) using ssh
  ```
  ssh username@server IP
  ```
  ```
  cd /u01/
  ```
  ```
  mkdir log-archive
  ```
  ```
  cd particular ip (of client server)
  ```
* Go inside if there is any file.
  ```
  cd OR_VAHAN
  ```
  ```
  ls
  ```
  ```
  cd dash_cat
  ```
* Check the path of .log file
  ```
  ls -lrth
  ```
  
  ```
  pwd
  ```
* Note the path and update the same path in configuration file of that IP.
* Edit confif file (path: /etc/logrptate.d)
  ```
  cd /u01/etc/logrotate.d
  ```

 * Create file (named of client IPs) and edit the log-rorate configurations 
  ```
  vim 10.242.36.130
  ```
 
  Do all the log-archive entries of application, access log and catalina.out in the file with following script.
  
  ```
  /u01/log/10.242.36.130/vtc_cat/*.log {
                daily
                rotate 370
                create
                copytruncate
                create 700 root root
                dateext
                dateyesterday
                dateformat -%d-%m-%Y
                compress
                missingok
                notifempty
                olddir /u01/log-archive/10.242.36.130/vtc_cat/
        }
  ```
  * Make a directory with the same log-archive path:
    ```
    mkdir -p /u01/log-archive/10.242.36.130/vtc_cat/
    ```

  * Update the permission under path: /u01/
    ```
    chmod -R 755 log-archive
    ```
  * Run the Dry run command to check errors if any
    ```
    logrotate -d /etc/logrotate.conf
    ```
    ```
    logrotate /etc/logrotate.conf
    ```

* Restart the Rsyslog service
    ```
    systemctl restart rsyslog
    ```
    ```
    systemctl status rsyslog
    ```
* If need to update the log rotation time, cinfigure in crontab
    ```
    vim /etc/crontab
    ```
    ![image](https://github.com/user-attachments/assets/cc8738e9-3550-4e57-b051-c7ac6087e9ea)


-----------------------------------
## 17. Gitlab Upgradation
* Version (16.11.10--->17.3.4--------->17.4.1) on RHEL 9.4

-------------------------
## 19. Nexus repo creation
- Create repository in the Nexus

-----------------------------------------
## 20. Manual Deployment: eDetection
### Steps to follow:
#### Pre-requisite
* Delete the old war in the local Download (if there is any) and "tmp" folder of the server.
* Download the war from **Nexus** ```10.246.40.241/Nexus``` to the local
1. Login on the server
   ```
   ssh etrans-infra-mon10@10.242.36.130
   ```
2. Make user as root
   ```
   sudo bash
   ```
3. Go on the 'tmp' and check the war is there or not (delete the old war if there is using the commamd ```rm -rf eDetectionServer.war```)
   ```
   cd /tmp
   ```
   ```
   ls -ltr
   ```
   <img width="923" alt="Manual Deploy 3" src="https://github.com/user-attachments/assets/1f6589a0-dca7-440f-8b4c-3f90e852d5cf" />

4. Now go to the Tomcat path
   ```
   cd /u01/Vahan_Deployment/edetection_srv1/webapps/
   ```
   <img width="814" alt="Manual Deployment eDetection 1" src="https://github.com/user-attachments/assets/e0d2145f-686e-43bf-ad06-130cb7830452" />

5. Check the list using 'ls' and 'ls -ltr'. And there you'll find the old war with the same name. So first make a backup of old war with today date. Command:
   ```
   mv eDetectionServer.war eDetectionServer.war_23_12_2024
   ```
6. Copy to "tmp" folder on Remote Server from local Server (this command should be run on your local "Dowanload")
   ```
   scp -r eDetectionServer.war etrans-infra-mon10@10.242.36.130:/tmp
   ```
7. Now Copy from "tmp" folder to "webapp" folder 
   ```
   cp /tmp/eDetectionServer.war .
   ```
   <img width="925" alt="Manual Deploy 2" src="https://github.com/user-attachments/assets/8eca1179-caee-4541-a9af-ef0e930a128d" />

8. Check the war in webapps it should be today's date
   ```
   ls -ltr
   ```
9. Now go back on the 'webapps' and restart the tomcat:
    
   ```
   systemctl restart tomcat@edetection_srvr
   ```
   <img width="922" alt="image" src="https://github.com/user-attachments/assets/bde699ed-fc7d-48bd-b001-7ef30924b87d" />

10. Lists all running processes with detailed information on ``edetection_srv1``` Tomcat.
    ```
    ps -ef | grep edetection_srv1
    ```
    <img width="539" alt="image" src="https://github.com/user-attachments/assets/97774922-0080-4683-a887-880f0f842856" />

    * Terminate the process
    ```
    kill -9 PID
    ```
    * Verified it was stopped:
    ```
    ps -ef | grep edetection_srv1
    ```
    * The process was no longer running (only the grep command appeared).
    * Restarted the service:
    ```
    cd ../bin/
    sh startup.sh
    ```
    <img width="924" alt="tc" src="https://github.com/user-attachments/assets/1bd10a96-7df9-4328-8d25-d801268fb0c2" />


11. Change the location of Backup
    ```
    mv eDetectionServer.war_23_12_2024 /u01/backup_edtn/
    ```
    ```
    ls -ltrh
    ```
    <img width="924" alt="image" src="https://github.com/user-attachments/assets/f45bd7a6-3aba-460a-b10e-fc145cd0a267" />
    
### Angular build Deployment
* In this manual deployment all the process is same except restart of Tomcat.
#### Steps:
1. Download the build from Nexus (use different terminal, go in Download)
   ```
   ls -ltrh
   ```
   ```
   scp -r eDetection.zip  etrans-infra-mon10@10.242.36.130:/tmp
   ```
   <img width="925" alt="image" src="https://github.com/user-attachments/assets/08aaaed2-477e-4d55-b853-bf9f327bcdae" />

2. Check either build has been opload on remote server
   ```
   ls -ltrh
   ```
   <img width="922" alt="image" src="https://github.com/user-attachments/assets/9f33455a-fb04-498f-a9db-349b40fff7d8" />

   As we can see in the image that zip file of build has been there on Remote server. So we'll make a backup of previous buils with same name and unzip the build.

   <img width="922" alt="image" src="https://github.com/user-attachments/assets/6970c797-b98f-4ad5-9488-605c5b641162" />

   ```
   unzip eDetection.zip
   ```

3. Now send build to remote server and change the permission of eDetection (500 from 755).
   ```
   cp -r /tmp/eDetection .
   ```
   ```
   chmod -R 500 eDetection
   ```

   <img width="615" alt="image" src="https://github.com/user-attachments/assets/9f106070-b3ee-4867-b84d-3385b0dfb3ea" />

   Note: Here no need to restart the Tomcat since this is a Angular war.

4. Send the backup file to the backup path.
   ```
   mv eDetection_15_01_2025 /u01/backup_edtn/
   ```
   ![edection_backup](https://github.com/user-attachments/assets/d618400a-dfb8-4cde-b8d9-144d9dde3c4c)

   [eDetection Website](https://vahan.parivahan.gov.in/eDetection/#/login)

   -------------------------------------------------------------
   ### Troubleshoot: eDetection Url not working

   <img width="794" alt="image" src="https://github.com/user-attachments/assets/7a464cde-d719-4b20-a36c-ab176560ed4c" />

   
   
------------------------------------------------------------------------------
## 22. CICD Pipeline Creation (eDetection Server 10.142.36.130)
* Case Study: Currently we do the manual deployment of eDetection Server but now we need to automate the deployment using Jenkins.
* What to do : We need to create the epositories on Nexus, CICD pipelines on Jenkins and configure the Inventory file, yml file and create the roles for Ansible. (First we will do all on staging environment for testing purpose, later on Production.)

### Tools:
1. Nexus
2. Ansible
3. Jenkins

-------------------------------------------------------------------------------
## 26. Tomcat installation and Configuration
Documentation file of this task has been saved to the NIC folder.

----------------------------------------------------------------------------------
## 27. Php MySql Website
In this task we have to setup a phpMySql Website (using RHEL, httpd) and configure this with the Git to make commits according to the changes need.

--------------------------------------------------------------------------------
## 29. Apache Kafka
A distributed streaming platform, it allows application to send, store & process data in real time.
#### Benefits
* Scalability: Handle large amount of data
* Fault Tolerance: Replication of data
* High Throughput: Capable of processing millions of messages per seconds.
* Durability: Reliable storage of messages.

#### Kafka Broker
When you run Kafka, you start one or more "broker" processes. It is basically the server (or node) in a Kafka cluster.
 * Stores messages
 * Handle read/write requests

#### Kafka Topic
A Kafka topic is like a "channel" or "category" 

* **Producer**: An application or process that sends events to Kafka topics. Producers write data to Kafka.
* **Consumer**: An application or process that reads events from Kafka topics. Consumer subscribe the data.

#### Kafka Partition
A partition is a substitution of a Kafka topic. Topics can have multiple partitions so data can be spread out across brokers. 

Each partition maintains a sequential order of messages, allowing parallel read and write for higher performance.
-----------------------------------------------------------------------------------------------
## 30. Swap memory (isuue resolve)
Use case: If there is the issue of **Swap memory** use on a Server, then we need to troubleshoot with following command.

### Steps:
1. Check current memory and disk usage
   ```
   free -m
   ```
   Displays memory usage in megabytes.
   Look for:
   * ```total / used / free RAM```
   * ```swap usage```

   ```
   df -hT
   ```
   Shows disk usage
-------------------------------------------------------------------------------
## 31. ELK 
<img width="346" height="146" alt="image" src="https://github.com/user-attachments/assets/98df61de-3489-4810-b484-3d01b5b5080b" />

ELK = Elasticsearch + Logstash + Kibana

It's a powerful open-source log analysis and visualization system widely used in DevOps and Kubernetes environments.
### Components:
1. Elasticsearch
 - A distributed search & analytics engine.
 - Stores all logs centrally.
 - Fast search, filtering, aggregation.

2. Logstash (or Fluent Bit)
 - A data pipeline tool.
 - Collects, processes, and forwards logs.
 - Can transform logs, parse JSON, etc.

3. Kibana
 - Web UI to visualize data stored in Elasticsearch.
 - Dashboards, charts, and real-time log searches.

### Using ELK in Kubernetes (K8s)
In Kubernetes, each Pod or Container writes logs to stdout and stderr. These logs are picked up using log forwarders and sent to ELK.

### You can deploy ELK using:
* Helm charts (recommended)
* YAML manifests
* Elastic Operator (for advanced users)

### Recommended Stack for K8s:
Fluent Bit → Elasticsearch → Kibana

Why?
* Logstash is heavy.
* Fluent Bit is lightweight, designed for K8s, and more resource-efficient.

## 32. K8s Deployment (PariwanSewa)
Here are the steps to deploy files manually on the staging environment on K8s.

### Steps:
1. Login on the server
2. Go to ```tmp``` folder, and enter in the last created folder where all the deployable files are stored.
   
   ![k8s deploy1](https://github.com/user-attachments/assets/ab23e7be-5668-4f0b-a62c-1c76a23753f7)

3. As in above screenshot there is ```23_2ndparivahan``` directory

   ![k8s deploy2](https://github.com/user-attachments/assets/11afdf1c-8fd5-4035-9b04-1f4520a1cbbd)

4. Create the backup first of all  the file with current date.
--------------------------------------------------------------------------
## 33. Docker build (Pariwanseva)
  In this task, we need to create docker build and send it to the K8s server (Parivahanseva)

### Steps:
1. Get 4 files---> .tar (on local)
   --- docker load
   --- docker tag

2. Gitlab----> search "paidnr"
3. Branch Change----> production
4. Download-----> tar.gz

5. Send tar file to "tmp" and extract there
   ```
   cp vahan-paidnrsearchservice-production.tar.gz /tmp
   ```
5. Extract tar (inside tmp)
   ```
   tar -xvzf vahan-paidnrsearchservice-production.tar.gz
   ```
6. Create a directory----> paidnr
7. Edit Dockerfile -----> vim dockerfile------> From: maven:latest as build

8. Build file (VPN disconnect)
   ```
   docker build -t paidnrsearchservices_v1 -f Docker_jenkins .
   ```
   ```
   docker build -t paidnrui_v4 -f dockerfile .
   ```
9. Check build
   ```
   docker images
   ```
10. Save 
    ```
    docker save -o  paidnrsearchservices_v1.tar f2323d0687ee
    ```
    ```
    scp -rp  paidnrsearchservices_v1.tar etrans-infra-mon10@10.192.188.222:/tmp
    ```
    -------------------------------------------------------------------------------
## 34. Logs check for k8s nodes (paidnr-app)
   In this task we have to check the daily logs of K8s pod (suggested services/app) and send them to the required Developer.
   ### Steps:
   1. Login to the jump server
   2. check pods details
      ```
       kubectl get all -n paidnr-app
      ```
      ```
      kubectl get pods -n paidnr-app
      ```
   3. Check logs of the given service (paidnr-app)
      ```
      kubectl logs -f vahan-paidnrgateway-6466b6c984-676zr -n paidnr-app
      ``` 

 ## 35. Container images migration 
    We need to migrate the Podman container from one server to another. Three things need to be consider during this:
    1. Image
    2. Volume
    3. Port

    Step.1 Login on the server 
    
    ```
    ssh etrans-infra-mon11@10.192.88.232
    ```
    ```
    ssh etrans-infra-mon11@10.192.88.183
    ```
    Step.2 Check the running images
    
    ```
    podman images
    ```
    ```
    podman ps -a
    ```
    Step.3 Make/save tar files of all four running imgaes
    
    ```
    podman save -o zookeeper.tar e15fcb51736e
    ```
    Step.4 send these tar files to local from the server
    
    ```
    scp -o ProxyJump=etrans-infra-mon10@10.192.88.232 -rp  etrans-infra-mon11@10.192.88.183:/tmp/tarimages .
    ```
    Step.5 Now send them from local to req. server
    
    ```
    scp -r /home/nic/tarimages etrans-infra-mon11@10.192.188.222:/tmp
    ```
    


