# Home Cybersecurity Lab

This is my personal cybersecurity lab using **VirtualBox**, with **Kali Linux** as the attacker machine and **Ubuntu Server** as the target.  

The goal of this lab is to learn basic networking, scanning, SSH, and web server interaction in a safe, isolated environment.

---

## Lab Setup

### Virtual Machines
- **Kali Linux** – attacker machine  
- **Ubuntu Server** – target machine  

Both VMs have **dual network adapters**:  
1. **Internal Network** – for VM-to-VM communication  
2. **NAT** – for internet access  

---

## Kali Linux Network Setup

**Adapter 1 (Internal Network)**  
![Kali Adapter 1](https://github.com/user-attachments/assets/f9699d96-4b35-418c-adf8-c23aae4c180e)  

**Adapter 2 (NAT)**  
![Kali Adapter 2](https://github.com/user-attachments/assets/f0266d58-b985-4d45-ba78-736b7e73d14c)  

**IP Address (Internal Network):** `192.168.56.20`  

---

## Ubuntu Server Network Setup

**Adapter 1 (Internal Network)**  
![Ubuntu Adapter 1](https://github.com/user-attachments/assets/da384025-5270-4b0f-bbb0-fa69831d573f)  

**Adapter 2 (NAT)**  
![Ubuntu Adapter 2](https://github.com/user-attachments/assets/d95ceb75-d3ce-435f-8ec7-4bdc7e2b66d5)  

**IP Address (Internal Network):** `192.168.56.10`  

---

## Step 1: Start the VMs and log in

Kali Linux is ready:  
![Kali Login](https://github.com/user-attachments/assets/b2d7ffec-1058-497a-8ab1-de53320a6ef0)  

Check Kali IP:  
![Kali IP](https://github.com/user-attachments/assets/41783e0e-8f32-4a24-bbfc-169db338b729)  

Check Ubuntu IP:  
![Ubuntu IP](https://github.com/user-attachments/assets/967f9df8-a762-44b3-bc75-6faef6e8989f)  

> **Note:** IP addresses must be in the same subnet (`192.168.56.x`) for them to communicate.

---

## Step 2: Test connectivity

Ping the other machine to make sure they can reach each other:

ping 192.168.56.10   # From Kali to Ubuntu

<img width="398" height="214" alt="image" src="https://github.com/user-attachments/assets/1479155c-bc2c-41e0-a0b7-2266581c9d20" />


ping 192.168.56.20   # From Ubuntu to Kali

<img width="418" height="80" alt="image" src="https://github.com/user-attachments/assets/4f031aa2-164d-4e0d-b9e1-84e59e8609f8" />

Thought: Ping success confirms the internal network is working properly.

---

## Step 3: Scan the target machine

From Kali, scan Ubuntu to see open ports:

nmap 192.168.56.10

<img width="398" height="161" alt="image" src="https://github.com/user-attachments/assets/c1a66dba-ccdf-4a1c-b530-53bf1c56d4b4" />

Observation: Port 22 (SSH) is open.
Note: Open ports are like doors – they tell you which services are available for remote access.

---

## Step 4: Check active connections on Ubuntu
netstat 192.168.56.10

<img width="399" height="298" alt="image" src="https://github.com/user-attachments/assets/cce684bb-6a22-41de-9ccc-83fccee49c66" />

Thought: netstat shows which services are listening and which ports are active. SSH should be active so I can log in remotely.

---

## Step 5: SSH into Ubuntu from Kali

Try to access SSH in ubuntu by using the username and password.

ssh username@192.168.56.10

<img width="401" height="246" alt="image" src="https://github.com/user-attachments/assets/01c54fff-69f5-42e9-9298-4ff4fab6ba74" />

<img width="398" height="298" alt="image" src="https://github.com/user-attachments/assets/c9af1190-cba8-4843-bcab-b708d4dd6b54" />

Note: SSH provides secure remote access. In real labs, attackers may try guessing passwords if SSH is open, but here it’s just for practice.

## Step 6: Install a web server on Ubuntu

  ### Step 6a: Update packages and install Apache
    sudo apt update
    sudo apt install -y apache2

  ### Step 6b: Start and enable the web server
    sudo systemctl start apache2
    sudo systemctl enable apache2

  ### Step 6c: Check status
    sudo systemctl status apache2

<img width="638" height="399" alt="image" src="https://github.com/user-attachments/assets/00b2d465-c07b-4b4c-8f89-7d41b8e5778e" />

Thought: Apache listens on port 80. This turns Ubuntu into a simple web server accessible from Kali.

---

## Step 7: Access the web server from Kali
Option 1: Terminal
curl 192.168.56.10

<img width="398" height="294" alt="image" src="https://github.com/user-attachments/assets/dc5512c8-a45e-49e6-b640-1d12c7c5b6b0" />


Option 2: Browser
firefox --new-window http://192.168.56.10

<img width="397" height="299" alt="image" src="https://github.com/user-attachments/assets/8bfb96e7-d2c6-4d35-976a-4c70371fdb43" />


Observation: Apache default page loads successfully.
Thought: Now I can practice interacting with a web server as a target safely.

<ins>Final Notes</ins>

- Internal Network + NAT setup helped me isolate lab traffic while still allowing updates.

- Ping, nmap, and netstat are simple but very useful to understand networking and services.

- Knowing IP addresses, open ports, and services is a critical first step before trying any attacks.

- SSH and Apache are safe ways to learn remote access and web server management.

- This lab helped me practice networking, reconnaissance, and basic server interaction in a controlled environment.
