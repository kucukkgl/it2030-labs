
### Assignment: Using `netstat` for Monitoring

#### **Objective:**
The purpose of this assignment is to practice using **`netstat`** for monitoring network connections on **ports 135** and **5357** from a Windows machine,
while simulating a **malicious** **nmap** scan to detect unauthorized access or suspicious connections.
Students will learn how to monitor and analyze network activity for security purposes,
particularly when it comes to monitoring critical ports on a Windows system.

---

### **Steps to Complete the Assignment:**

#### **1. Simulate a Malicious Activity with `nmap` on Linux:**

- **On the Linux machine**, use **nmap** with the **`-sV`** option to scan **port 5357** (MS HTTP API) towards the Windows machine.
- This will help detect the service version running on that port.
- This scan is considered potentially **malicious** because **nmap** can be used by attackers to probe systems.
   Run the following command (replace `<Windows_IP>` with the actual IP address of the Windows machine):

   ```
   nmap -sV -p 5357 <Windows_IP>
   ```

#### **2. Monitor Active Connections on Windows Using `netstat`:**

- **On the Windows machine**, open **Command Prompt** and use `netstat` to monitor active network connections. Use the following command to filter the results and show specific activity for port 5357:

   ```
   netstat -a | findstr 5357
   ```

   - Look for the following connection states:
     - **LISTENING**: The port is open and waiting for incoming connections.
     - **ESTABLISHED**: An active connection has been made.
     - **TIME_WAIT**: The port was recently closed, and the system is waiting for a timeout before the port can be reused.

#### **3. Repeat the Process for Port 135:**

- Now, **repeat the same process** for **port 135** (MS RPC) to observe its activity. Use the following **nmap** command on Linux:

   ```
   nmap -sV -p 135 <Windows_IP>
   ```

   Then, on the Windows machine, use **`netstat`** to monitor port 135:

   ```
   netstat -a | findstr 135
   ```

#### **4. Analyze `netstat` Output:**

- **Observe the `netstat` output** for both ports (`135` and `5357`):
   - Check if the ports are in a **LISTENING** or **ESTABLISHED** state, which indicates that services are accepting or have accepted connections.
   - Pay attention to **TIME_WAIT** states, which could indicate that the connection was recently closed.
   - Record how long it takes for conenction to get disappear.

#### **5. Document the Findings with Screenshots:**
- **Capture screenshots** of the following and save them in a **Word file**:
   1. The output of the **`nmap`** scan showing results for **port 5357** and **port 135** (both scans).
   2. The **`netstat`** output showing the active connections on **ports 5357** and **135** before and after the **`nmap`** scans.
   3. The **connection states** for both ports, noting whether they are in **LISTENING**, **ESTABLISHED**, or **TIME_WAIT** states.

This assignment teaches students how to use **`netstat`** for monitoring network activity, focusing specifically on **ports 135** and **5357**. It also emphasizes the importance of recognizing **nmap** as a potential **malicious activity** and leveraging network monitoring tools for detecting unauthorized access and safeguarding systems.
