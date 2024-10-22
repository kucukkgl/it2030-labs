## Cyberlabs Setup
Portainer Access on the Sandbox VM
https://localhost:9443/#!/auth
user/pwd: admin/infosecure123456789

![image](https://github.com/user-attachments/assets/c53b7626-d486-4412-ac20-554c8d53256c)


## Part 1: Configuring UFW Firewall on Ubuntu

### Objective
To enable and configure the Uncomplicated Firewall (UFW) on Ubuntu to control network traffic effectively.

### Instructions

1. **Check UFW Status**
   - Open your terminal.
   - Type the following command to check the current status of UFW:
     ```bash
     sudo ufw status
     ```
   - You should see a message indicating that "Status: inactive".
   - **Action**: Take a screenshot of this status and upload it here.

2. **Allow All Ports Temporarily**
   - Before enabling UFW, allow all incoming and outgoing connections to prevent accidental lockouts:
     - Type the following command to allow all incoming connections:
       ```bash
       sudo ufw default allow incoming
       ```
     - Then, allow all outgoing connections:
       ```bash
       sudo ufw default allow outgoing
       ```
   - **Discussion**: Discuss with your peers the importance of allowing all ports initially. Consider the following:
     - Why do you think firewalls come with the least privileges by default?
     - Is allowing all ports a good approach for initial configuration?
     - Evaluate the implications of this decision.

3. **Enable UFW**
   - Now, enable the UFW by typing:
     ```bash
     sudo ufw enable
     ```
   - **Action**: Check the status of UFW again to ensure it is active:
     ```bash
     sudo ufw status
     ```
   - You should see a message indicating that "Status: active".
   - **Action**: Take a screenshot of this status and upload it here.

---

## Part 2: Verifying Apache Hosting on the Ubuntu Server

### Objective
Linux Server hosts a web application. We will confirm that the Apache web server is running on the Linux server and is accessible over the network.

![image](https://github.com/user-attachments/assets/9c2f3915-b68d-4589-96bd-44b9d3a9de54)


### Instructions
1. ** Notedown Linux(Ubuntu) Server IPV4 address**
  ```bash
  ip addr show eth0 | grep inet
  ```


2. **Check Apache Service Status**
   - Open your terminal.
   - Check the status of the Apache service by running:
     ```bash
     sudo systemctl status apache2
     ```
   - You should see an output indicating that the Apache service is **active (running)**.

  - CTRL + C to exit

3. **Test Apache Accessibility**
   - To test if Apache is accessible, use the following command:
     ```bash
     curl http://localhost:80
     ```
   - You should see the default Apache welcome page or any other webpage configured as the default.

   - Open Chrome and type http://localhost:80 on the url you shoulD be seeing how chrome renders the html from apache web server.
   
   - Open Chrome and type http://ubuntu_ip_address:80 (e.g. http://192.168.124.123) on the url you should be seeing how chrome renders the html from apache web server.

Here’s the updated version of **Part 3**, with steps 8 and 9 removed. The focus is now solely on testing the SSL container and managing UFW firewall rules.

---

## Part 3: Firewall Rule Implementation

Ubuntu is hosting a web site.
### Objective

Implement and delete firewall rules.

### Instructions

1. **Test Website Access from the `SSL` Container**
   - Start `SSL` container on the portainer.
   - Ensure you are in the `SSL` container's console.
   - Use the `curl` command with your host IP address:
     ```bash
     curl http://ubuntu_ip_address:80
     (e.g. http://192.168.124.123)
     ```
   - You should see the html code the same webpage as before. Upload the screenshot of this output.

2. **Block `SSL` Container's Access to Host Machine Using UFW**
   - Go back to the host machine's terminal.
   - Block access to the host machine from the SSL container:
     ```bash
     sudo ufw deny from <ssl_container_ip>
     e.g. sudo ufw deny from 172.17.18.19
     ```
   - Replace `<ssl_container_ip>` with the actual IP address of your SSL container.

3. **Check UFW Status**
   - Verify the UFW status:
     ```bash
     sudo ufw status
     ```
   - Upload your screenshot here. You should see that traffic for the SSL server is denied.

4. **Test Connectivity from the SSL Container Again**
   - Go back to the SSL container's console and type:
     ```bash
     curl http://ubuntu_ip_address:80
     ```
   - The firewall should block this request. Upload the screenshot of this output.

5. **Re-allow SSL Container to Access Host Machine's Localhost Page**
   - On the host machine, list UFW rules with numbering:
     ```bash
     sudo ufw status numbered
     ```
   - Find the associated rule number for the SSL container's IP address and upload your screenshot here.

6. **Delete the Block Rule**
   - Remove the blocking rule by typing:
     ```bash
     sudo ufw delete <rule_number>
     ```
   - Replace `<rule_number>` with the actual number you found in the previous step. Upload your screenshot here.

7. **Test Website Access Again from the SSL Container**
   - Return to the SSL container's console and type:
     ```bash
     curl http://<host_ip_address>
     ```
   - You should now successfully access the webpage's html code. Upload your screenshot here.

---

## Part 4: Managing Network Access with UFW and CIDR Notation

### Objective
To activate the noSSL container, test connectivity, and manage network access for both SSL and noSSL containers using UFW with CIDR notation.

### Instructions

1. **Activate the `noSSL` Container Using Portainer in the Sandbox VM**
   - Open your sandbox VM where Portainer is installed.
   - Launch Portainer in your web browser.
   - Navigate to the **Containers** section.
   - Find the `noSSL` container and start it by clicking the **Start** button.

2. **Test Website Access from the `noSSL` Container**
   - Open the `noSSL` container's console in Portainer.
   - Inside the `noSSL` container's console, type:
     ```bash
     curl http://ubuntu_ip_address:80
     ```
   - You should successfully retrieve the host machine's localhost webpage. Upload your screenshot here.

3. **Block Network Access for SSL and noSSL Containers**
   - Go back to the host machine's terminal.
   - Block the entire network for both `SSL` and `noSSL` containers from accessing the host machine by using CIDR notation:
     ```bash
     sudo ufw deny from <IP_range>
     ```
   - Replace `<IP_range>` with the appropriate CIDR notation (e.g., `172.17.0.0/16`).

4. **Check UFW Status**
   - Verify the UFW status:
     ```bash
     sudo ufw status
     ```
   - Upload your screenshot here.

5. **Discuss CIDR Notation**
   - Explain what you did by using CIDR notation in the previous step.
   - Research and discuss the practicality of using CIDR notation in firewalls with your peers. Consider questions such as:
     - What are the advantages of using CIDR notation?
     - How does it improve network management and security?

6. **Test Connectivity from both the `SSL' and `noSSL` Container Again**
   - Go back to the noSSL container's console and type:
     ```bash
     curl http://ubuntu_ip_address:80
     ```
   - Discuss what happened and why you received that response.
   - Upload your screenshot here.

---

# Optional Extra Points
## Part 5: Exploring Help Options in UFW

### Objective
To familiarize yourself with the UFW (Uncomplicated Firewall) command options and see how they affect firewall rules.

### Instructions

1. **Display UFW Help Menu**
   - Open your terminal and type the following command to view all available commands and options for the UFW firewall:
     ```bash
     sudo ufw --help
     ```
   - This command will display a list of commands you can use to manage firewall rules.

2. **Choose an Option to Try**
   - Pick one of the listed options to experiment with. You can choose from options such as `allow`, `deny`, `limit`, or `delete`.
   - For example, to allow traffic on a specific port, use:
     ```bash
     sudo ufw allow <port_number>
     ```
   - Alternatively, to limit the rate of connections to a service, use:
     ```bash
     sudo ufw limit <service>
     ```

3. **Document the Results**
   - After running the chosen command, check the updated status of the UFW rules by typing:
     ```bash
     sudo ufw status
     ```
   - Take a screenshot of the updated UFW status and upload it here.
   - **Describe the Effect**: In your own words, explain the effect of the command you executed. For example, if you allowed a port, discuss what that means for incoming traffic on that port.

### Points to Consider
- How does the command you tried influence network security?
- Why is it important to understand these commands when managing a firewall?
- Discuss the practical applications of the command in real-world scenarios.

