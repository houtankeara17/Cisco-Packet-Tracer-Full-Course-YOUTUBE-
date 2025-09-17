# 3. Router and Switch Configuration

👉 **Steps to configure**

1. **Switch0 Setup**
   - Assign IP addresses to PCs:
     - PC0: `192.168.1.10`
     - PC1: `192.168.1.11`
     - PC2: `192.168.1.12`
   - Gateway for all PCs: `172.16.1.1`

2. **Switch1 Setup**
   - Assign IP addresses to PCs:
     - PC3: `172.16.1.10`
     - PC4: `172.16.1.11`
   - Gateway for all PCs: `192.168.1.1`

3. **Router Setup**
   - Path: `Config -> GigabitEthernet0/0`
     - Port Status: **ON**
     - IPv4 Address: `192.168.1.1`
   - Path: `Config -> GigabitEthernet0/1`
     - Port Status: **ON**
     - IPv4 Address: `172.16.1.1`

👉 **Note:** Test by sending messages between **all PCs**.

=====================================================================

# 4. How to connect wireless to wired

👉 **Steps to configure**

1. **Access Point Setup**
   - Go to the **Access Point**
   - Click on **Port 1**
   - Set **Port Status**: ON
   - SSID: `yourname`
   - 2.4 GHz Channel: `6`
   - Coverage Range: `140 meters`
   - Authentication: `WPA2-PSK`
   - PSK Pass Phrase: `your number (ex: 123456789)`

2. **Smartphone Setup**
   - Path: `Config -> Wireless`
   - SSID: `yourname`
   - Authentication: `WPA2-PSK`
   - PSK Pass Phrase: `your number (ex: 123456789)`

3. **PC Setup**
   - Turn off the PC
   - Add **WPC300N**
   - Path: `Config -> Wireless`
   - SSID: `yourname`
   - Authentication: `WPA2-PSK`
   - PSK Pass Phrase: `your number (ex: 123456789)`
   - Path: `IP Config`
   - Select: **Static**
   - IP Address: `192.168.1.10`
   - Verify on Desktop -> IP Config

4. **Laptop Setup**
   - Turn off the Laptop
   - Add **WPC300N**
   - Path: `Config -> Wireless`
   - SSID: `yourname`
   - Authentication: `WPA2-PSK`
   - PSK Pass Phrase: `your number (ex: 123456789)`
   - Path: `IP Config`
   - Select: **Static**
   - IP Address: `192.168.1.11`
   - Verify on Desktop -> IP Config

👉 **Note:** Test by sending a message from **PC1 to PC0** or **Laptop0**.

=====================================================================

# 5. Step to config this DHCP with Email

👉 Steps to config

1. **Configure Server IP**
   - Path: `Server -> Config -> FastEthernet0 -> IP Config`
   - Mode: `Static`
   - IP: `192.168.1.1`

2. **Enable DHCP**
   - Path: `Services -> DHCP`
   - Turn Service: **ON**
   - Select: **Pool Name**
   - Change Start IP Address: `192.168.1.10`
   - Set Max and Min Users: `10` (or other as needed)
   - Click **Save**

3. **Enable Email Service**
   - Path: `Services -> Email`
   - Turn all options: **ON**
   - Domain Name: `gmail.com`
   - Add User:
     - Username: `ABC`
     - Password: `abc`
   - Click **Plus (+)**

4. **Configure Client PCs (PC1 and PC2)**
   - Path: `Desktop -> IP Config`
   - Select: **DHCP (Auto IP Address)**
   - Configure Email Login:
     - User Info:  
       - Your Name: `ABC`  
       - Email Address: `ABC@gmail.com`  
     - Server Info:  
       - Incoming Mail Server: `192.168.1.1`  
       - Outgoing Mail Server: `192.168.1.1`  
     - Logon Info:  
       - Username: `ABC`  
       - Password: `abc`  
   - Click **Save**

5. **Send Email from PC1 or PC2**
   - Compose new email
   - To: `cba@gmail.com`
   - Subject: `testing dhcp`
   - Description: `hello`
   - Click **Send**

6. **Check Email**
   - Go to **Receive**
   - Verify received mail is displayed

=====================================================================

# 6. How to apply user to read-write file in DNS and FTP

👉 Steps to config 

1. **Go to DNS and setup IP address**
   - IP address: `192.168.1.1`
   - DNS server: `192.168.1.1`
   - Path: `config -> FastEthernet -> DNS server (192.168.1.1)`

2. **Go to FTP setup**
   - Path: `config -> FastEthernet -> ip address (192.168.1.100)`
   - Go to: `services -> FTP -> apply for user set up`
   - Credentials:  
     - Username: `abc`  
     - Password: `123`  
     - Permissions: `(R-W-D-RE-L)`  
   - Click **Save**

3. **Create a file**
   - Path: `Desktop -> Text Editor`
   - Write text in the file
   - Save as: `abc`
   - Click **OK**

4. **Set IP address for PC0 and PC1**
   - Path: `desktop -> IP config`
   - Example:
     - IP address: `192.168.1.2`
     - DNS: `192.168.1.1`

5. **FTP Transfer using PC0**
   
   Desktop -> Command prompt -> Cisco Packet Tracer PC Command Line 1.0
   
   ```bash
   C:\>ftp 192.168.1.100
   Trying to connect...192.168.1.100
   Connected to 192.168.1.100
   220- Welcome to PT Ftp server
   Username:keara
   331- Username ok, need password
   Password: 123 
   230- Logged in
   (passive mode On)
   ftp> put abc.txt

   Writing file abc.txt to 192.168.1.100: 
   File transfer in progress...

   [Transfer complete - 34 bytes]

   34 bytes copied in 0.075 secs (453 bytes/sec)
   ftp> quit

   221- Service closing control connection.
   C:\>
   ```