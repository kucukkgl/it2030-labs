### Assignment: Exploring Netstat Options for Monitoring HTTP Traffic

#### Objective:
The goal of this lab is to explore various **netstat** options (`-t`, `-u`, and others) and understand how they display connection states. The focus is on monitoring HTTP traffic to **httpbin.org** using **netstat** and observing how TCP connections behave over time.

---

### Steps to Complete the Assignment:

#### 1. Lab Environment:
- A **Linux machine** with access to the internet.
- The **netstat** tool installed (part of the `net-tools` package if not already installed).
- Use the host **httpbin.org** for the experiment:
  - Known IP addresses: `50.19.58.113`, `52.203.38.8`.

---
#### 2. Verify the HTTP Server's IP Addresses:

1. Use **nslookup** in the terminal to confirm the IP addresses of `httpbin.org`:
   ```bash
   nslookup httpbin.org
   ```

2. Alternatively, use the following online tool to find the IP addresses of `httpbin.org`:
   - Visit: [https://www.nslookup.io/domains/httpbin.org/webservers/](https://www.nslookup.io/domains/httpbin.org/webservers/)

3. Cross-reference the output with the known IP addresses: `50.19.58.113` and `52.203.38.8`.
---

#### 3. Monitor HTTP Traffic with Netstat -t (TCP):

1. Open **Terminal A** and keep it ready for monitoring with **netstat**:
   ```bash
   netstat -t
   ```
   - This terminal will monitor TCP connections.

2. Open **Terminal B** and issue the following command to send an HTTP GET request to `httpbin.org`:
   ```bash
   curl http://httpbin.org
   ```

3. Return to **Terminal A** and observe the connection to `httpbin.org` and its IP address (e.g., `50.19.58.113`):
   - The connection state should initially be `ESTABLISHED`.

4. Wait for a short time and recheck in **Terminal A**:
   - The connection will fall into the `TIME_WAIT` state and eventually disappear as the TCP session terminates.

---

#### 4. Monitor with Netstat -u (UDP):

1. Keep **Terminal A** open and switch to **Terminal B**.

2. Repeat the HTTP request to `httpbin.org`:
   ```bash
   curl http://httpbin.org
   ```

3. In **Terminal A**, check active **UDP** connections using:
   ```bash
   netstat -u
   ```
   - Observe that no connections are displayed.

4. **Analysis:**
   - Explain why UDP connections are not shown when making HTTP requests (hint: HTTP uses TCP, not UDP).

---

#### 5. Monitor Process IDs with Netstat Options:

1. Re-run the HTTP request in **Terminal B**:
   ```
   curl http://httpbin.org
   ```

2. In **Terminal A**, use the following command to display active connections along with their associated process IDs:
   ```
   netstat -tp
   ```
   - Observe the process ID associated with the `curl` command.
   - 
### 6. Observations and Analysis:

- **Screenshots:**
  - Provide screenshots from **Terminal A** showing:
    1. TCP connections during and after the `curl` request.
    2. The `TIME_WAIT` state.
    3. Results of the `-u` and `-tp` options.

- **Write a brief explanation** addressing:
  1. What was displayed using `netstat -t` during and after the HTTP request?
  2. Why does the connection fall into the `TIME_WAIT` state and eventually disappear?
  3. Why does `netstat -u` not display anything for HTTP requests?
  4. What did the `-tp` option reveal about the process handling the HTTP connection?
