# SOC-Log-Analysis-Lab

Lab Topology: Beginner Hands-On Projects


kali linux (Attacker) ----> Ubuntu Machine (Victim) ----> Ubuntu Machine (Defender)

Objective
As a beginner in the SOC analyst field, i am to simulate real-world attacks and analyze logs using native Linux tools to build foundational SOC analyst skills.

Tools Used
1. kali Liunx (this is the attacker machine, i used nmap, hydra and gobuster)
2. Ubuntu server (apache2, sshd, rsyslog)
3. rsyslog (we made use of this for our log forwarding and collections)
4. lnav (it is a log navigator)
5. grep, awk, sort, uniq (These are CLI log analysis)

Lab Setup Steps

step 1: I made sure to check the static IP configuration of all my virtual machine. (note: all the virtual machine must be in the same internal network so it will not affect your own internet communication, and if you want to make use the internet you will choose the VM and select NAT option in the network section)

Step 2: rsyslog configuration 
using rsyslog to forward logs data to my defender ubuntu machine for analysis.

Step 3: Enable services

Attack Simulation

Attack 1: using Nmao reconnaissance to check if the host was up
using the command: nmap -sS -sV 192.168.56.102

here is the picture of the attack:



here is the picture of syslog showing the connection attempt:


Attack 2: Using SSH Brute Force to try multiple password to get the admin password
using the command: hydra -l admin -P /usr/share/wordlists/rockyou.txt.gz 192.168.56.102

Here is picture of the log evidence:

Attack 3: Using of Directory Busting(web enumeration)
using the command: gobuster dir -u http://192.168.56.102 -w /usr/share/wordlists/dirb/common.txt

here is the picture of the attack:

Log Analysis Queries
1. Here is the total number of failed SSH attempts:

2. Here is the top attacking IP addr:

3. Here are the targeted usernames

4. Did any login succeed?


Recommendation 
1. you must disable root SSH login
2. ln other to block repeated failed attempts, you must implement the fail2ban
3. you must use SSH key authentication instead of password to aviod repeated failed attempts
4. you can restrict SSH access by IP using the allowlist

Lesson learned from the pratical hand-on project on lab topology and log analysis
1. linux logs contain everything you need to run initial triage
2. using the grep + awk commands are the most powerful combination for quick log analysis
3. correlation between auth.log and web logs reveal coordinated attacks.
