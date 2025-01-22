### Assignment: SSH Attempt from Linux to Windows for Netstat Monitoring

#### Objective:
The purpose of this lab is to observe how **netstat** can monitor connection attempts,
even when the connection is not successfully established.
Students will attempt an SSH connection from a **Linux machine** to a **Windows machine** (with firewalls enabled) 
and analyze how netstat reflects the connection states.

Provide screenshots in a word document.

---

### Steps to Complete the Assignment:
#### 1. Lab Environment Setup:
- Ensure you are using the **Infosec Lab** environment.
- The Linux and Windows machines should be running on the same network or properly configured for communication.
- **Enable firewalls on the Windows machine** (this ensures the SSH attempt fails).
  - Open **Windows Defender Firewall**, ensure it is turned on, and block all incoming SSH connections.
- Note down the **IP address** of the Windows machine (e.g., `192.168.124.207`).

---

#### 2. Attempt SSH from Linux to Windows:

1. Open the **terminal** on the Linux machine.
2. Attempt to establish an SSH connection to the Windows machine using the following command:
   ```
   ssh Administrator@192.168.124.207
   ```
   - Replace `192.168.124.207` with the actual IP address of the Windows machine.
   - If prompted for a password, you can leave it blank for this test.

---

#### 3. Monitor the Connection on Linux Using Netstat:
- Before killing the SSH session, observe the connection state using **netstat**:
   ```
   netstat | grep 192.168.124.207
   ```
   - The output should display a `SYN_SENT` state, indicating that the Linux machine is attempting to initiate a connection to the Windows machine.

---

#### 4. Terminate the SSH Session:

- Press `Ctrl + C` in the Linux terminal to cancel the SSH attempt.
- The SSH session will close, and the connection attempt will end.

---

#### 5. Verify the Connection State on Netstat Again:

- Run the **netstat** command again:
   ```
   netstat | grep 192.168.124.207
   ```
   - This time, the output should be **blank**, indicating that there are no active connection attempts to the Windows machine.
