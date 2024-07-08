# Work-2024

Yeahh!! So finally we are here....
Let's documents our learnings on the go..

### Case Studies
## 1. Keycloak and Haproxy local installation and update the version of Haproxy (from 1.8.31 to 2.0) without deleting the data.
   * Make a container on docker and run HAproxy on it, Same for the Keycloak.
   #### Keycloak
   * is an open source software product to allow single sign-on with identity and access management aimed at modern applications and services.
   * Keycloak is the standalone tool for identity and access management, which allows us to create a user database with custom roles and groups.
   #### HAproxy
   * HAProxy is a free and open source software that provides a high availability load balancer and Proxy for TCP and HTTP-based applications that spreads requests across multiple servers.
     
## 2. IP address detail list of Staging servers with the information.
   
## 3. Reboot a Server (Staging: 151)
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

  ## 4. Updation of Inventry Files

  ## 5. Creation of Public and Private Keys
   * Make user as a root user using ``sudo -i`` command and run the command ``ssh-keygen``.
   * This will generate Public/Private rsa key pair.

## 6. Centralised Log Server
* In this task, I have to transfer logs of Tomcat Servers and HAProxy to a Centalised Log Server using **rsyslog** tool. So that Developer can have all the logs together to moniter.
  ### Steps
  * Create 2 VMs, one for Tomcat services and HAProxy and other for Centalised log server.
  * VM1- Client Server: Set-up two Tomcat services named Tomcat1, Tomcat2 and HAProxy.
  * VM2- Centralised Log Server: rsyslog
  * Configure rsyslog on Tomcat and haproxy to forward logs from VM1 to VM2.

 ### Tomcat installation
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



