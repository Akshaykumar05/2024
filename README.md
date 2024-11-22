# Work-2024

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
## 16. Rsyslog configuration
* Configuration: the rsyslog server (10.242.36.24) and sync the log (application, access log and catalina.out) of eDetection Server (10.242.36.130).
* Create a log rotation script and configure it for log rotation on Staging environmenet.


-----------------------------------
## 17. Gitlab Upgradation
* Version (16.11.10--->17.3.4--------->17.4.1) on RHEL 9.4



