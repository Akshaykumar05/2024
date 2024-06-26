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

## 6. Logs Transfer
* In this task, I have to transfer logs of Tomcat and HAProxy of a server to a Centalised Log Server using **rsyslog** tool.
  ### Steps
  * Create 2 VMs, one for Tomcat and HAProxy and other for Centalised log server.
  * Install applications on them. On VM1: Tomcat and HAProxy, on VM2: rsyslog
  * Forward logs from VM1 to VM2

 ### Tomcat installation
 1. Download tomcat file
 2. Untar file
 3. Move file to usr/local/
    * ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/5f61cba2-3830-498f-a915-825b3e5e3a11)
 4. 
