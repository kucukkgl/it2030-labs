### Assignment: Ping Windows for Network Monitoring in the Infosec Lab

#### **Objective:**
The objective of this assignment is to observe and analyze the behavior of **ping (ICMP)** traffic between a **Linux** and **Windows** machine,
and understand its implications for **network monitoring**. Students will explore how the **ping** command reacts when the Windows machine is powered on versus
when it is powered off, and how this can be used for network diagnostics and monitoring in an **Infosec Lab** environment.

### **Steps to Complete the Assignment:**

#### **1. Start the Windows Machine:**

- **Power on the Windows machine** using the **sandbox**.
  - Go to the **sandbox deployment tab**.
  - Under the **components sections**, select the **Windows machine** and start it.
- Wait for the system to boot and establish network connectivity.

#### **2. Get the IP Address of the Windows Machine:**

- **On the Windows machine**, open **Command Prompt** (press `Win + R`, type `cmd`, and hit Enter).
- Type the following command to get the IP address of the Windows machine:

   ```
   ipconfig
   ```

- **Note down the IPv4 address** of the machine (e.g., `192.168.1.10`).

#### **3. Ping the Windows Machine from the Linux Machine (While Windows is Running):**

- **On the Linux machine**, open a terminal.
- Ping the Windows machine using the IP address obtained from the `ipconfig` command:

   ```
   ping <Windows_IP>
   ```

   Example:
   ```
   ping 192.168.1.10
   ```

- Observe the following:
   - The **ping request** should flow, and you will see responses coming back from the Windows machine. The output should look like this:

     ```
     PING 192.168.1.10 (192.168.1.10) 56(84) bytes of data.
     64 bytes from 192.168.1.10: icmp_seq=1 ttl=128 time=2.35 ms
     64 bytes from 192.168.1.10: icmp_seq=2 ttl=128 time=2.12 ms
     ```

#### **4. Stop the Windows Machine:**

- **Turn off the Windows machine** using the **sandbox**.
  - Go to the **sandbox deployment tab**.
  - Under the **components sections**, select the **Windows machine** and click **stop** to power off the machine.

#### **5. Ping the Windows Machine from the Linux Machine (While Windows is Stopped):**

- **On the Linux machine**, ping the same IP address as before:

   ```
   ping <Windows_IP>
   ```

- Observe the following:
   - Since the Windows machine is turned off, the **ping will not receive a response**. The ping will continue to try sending requests and will **freeze** or **timeout**, showing an output like this:

     ```
     PING 192.168.1.10 (192.168.1.10) 56(84) bytes of data.
     Request timeout for icmp_seq 1
     Request timeout for icmp_seq 2
     ```

- After a few attempts, the ping may stop or show:

   ```
   ping: sendto: No route to host
   ```

#### **6. Observations and Analysis:**

- **Document your observations:**
   - While Windows is running, **ping requests successfully flow** and you receive responses back.
   - When Windows is stopped, the **ping freezes**, and no responses are returned.
   - The ping command either times out or shows a "No route to host" message. (OPTIONAL)
   
- **Write a brief analysis:**
   -Provide necessary screesnhots.
   - Why does the ping freeze when the Windows machine is turned off?
   - What does this behavior indicate about how the **ping** command relies on network connectivity and the active status of the target machine?
   - Discuss the role of **ICMP** and how network communication is disrupted when a device is powered off or not responsive.

