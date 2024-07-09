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
 ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/a4b724ce-dd56-47cb-afee-49cf9b9f6cff)

* In this task, I have to transfer logs of Tomcat Servers and HAProxy to a Centralised Log Server using **rsyslog** tool. So that Developer can have all the logs together to moniter.
  ### Steps
  * Create 2 VMs, one for Tomcat services and HAProxy and other for Centalised log server.
  * VM1- Client Server: Set-up two Tomcat services named Tomcat1, Tomcat2 and HAProxy.
  * VM2- Centralised Log Server: rsyslog
  * Configure rsyslog on Tomcat and haproxy to forward logs from VM1 to VM2.

 ### Centralised Log Server set up
1. Create a VM2 with atleast 2 GB RAM and 30 GB Hard disc space.
2. Install Ubuntu on it.
3. Install **rsyslog package**
   
   ```
   sudo apt update -y
   ```
   ```
   sudo apt install rsyslog -y
   ```
   ![rsyslog install](https://github.com/Akshaykumar05/NIC/assets/114390890/78f06ca3-7859-4e11-8ec9-a3b2783dc3ce)

4. Note: If you are using CentOS 8 / RHEL 9. then by default, Rsyslog  comes installed on it. To verify the status of Rsyslog, use the command:
   ```
   systemctl status rsyslog
   ```
   ![image](https://github.com/Akshaykumar05/NIC/assets/114390890/48cfdb3e-31f1-4881-92cb-6da939834106)

   
5. Next, we need to modify a few settings in Rsyslog configuration file. Edit the rsyslog configuration file:
   ```
   sudo vim /etc/rsyslog.conf
   ```
6. Sroll the file and uncomment the following lins to allow reception of logs via UDP and TCP protocol.
     
   ```
   module(load="imudp")
   input(type="imudp" port="514")

   module(load="imtcp")
   input(type="imtcp" port="514")
   ```
   ![rsyslog conf](https://github.com/Akshaykumar05/NIC/assets/114390890/4c1d71fc-5ebd-45f3-bbd5-56dd47c698c5)

   * Save and exit the configuration file.
  
7. To recieve the logs from the client server, we need to open Rsyslog default port 514 on the firewall. Run the following commands to achieve this:
   ```
   firewall-cmd  --permanent -add-port=514/tcp
   ```
   ```
   firewall-cmd  --permanent -add-port=514/udp
   ```
   * Next, reload the firewall to save the changes.

   ```
   sudo firewall-cmd --reload
   ```

   * Sample output
     
   ![firewall tcp,udp](https://github.com/Akshaykumar05/NIC/assets/114390890/922eb207-338e-4d72-9ee0-b92ebeda301c)


8. Set up a log file to store incoming logs:
   * Add the following line to the end of the file:
     
   ```
   *.* /var/log/remote.log
   ```
9. Restart the rsyslog service:
   ```
   sudo systemctl restart rsyslog
   ```
10. To enable Rsyslog on boot, run the following command:

    ```
    sudo systemctl enable rsyslog
    ```
11. Now, we need to confirm that the Rsyslog service is listening on port 514, use the **netstat** commands as follow:
    
    ```
    sudo netstat telnp
    ```
    * Sample output
      



   
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



