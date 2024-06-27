# Cisco Email Threat Defense (ETD) - Remediation script (without M365)

Cisco ETD is a cloud AI/ML driven email security system that was meant to make security administrator life easier with all the automated detection and remediation features. However the report modules on ETD does not comes with notification services, hence administrator will have to login to the portal and view report manually. 

This python script is trying to be a temporary fix to close this feature gap. The script will pull ETD report data via API, and attached the JSON data and send an email to administrator. Administrator can then schedule this script in a cron job to generate report at the interval intended. 

The report in this case will be the Top Target with counts of each verdict. 

Release update 
- 23rd May 2024 - ETD API enforced the use of an API Key in every request. Updated the script to include this mandatory query string. 


Pre-requisite:-

* Mac/Linux
* SMTP server, can be any working one on the network, and allow your script host to relay email
* Working Python & library
  - smtplib
  - json
  - requests
  - datetime
* ETD API client credential and API Key - (From ETD -> Administration -> API Clients)
* Knowing your ETD instance location (check from the ETD URL)


The python library should be from the standard package. If it is not there, then install with pip, example:-
```bash
pip3 install requests
```


## Installation (required)

The main project file will be 'etd_top_target.py' script. Here are the steps to prepare and run the script.

1. Complete the prerequisites, check the library above, get ETD API client
2. Installation - Clone the repo
3. Configuration - Edit the script, fill up API client credentials and the instance URL
4. Execute the script
5. Schedule the script


Clone the repo
```bash
git clone https://github.com/ciscoketcheon/ETD-Email-Script.git
```
Go to your project folder
```bash
cd ETD-Email-Script
```
You may start editing the script using your favourite editor. Example:-
```bash
vi etd_top_target.py
```


## Configuration (required)

1. SMTP Server

Add SMTP server IP, email sender (username) and admin's email address (admin_email)


2. ETD API client credentials

Mandatory field is client_id, client_password and api_key example
```bash
client_id = "ac6991c4-df45-xxxx-xxxx-xxxxxxxxx"
client_password = "PxVRzLALsETnyrZri9oLiZ_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
api_key = "twBJkLMj8l3pmMWtxxxxxxxxxxxxxxxxxxx"
```
The rest of token_url and report URL is pre-populated with beta instance (api.beta.etc.cisco.com), if you are using other instances, e.g. apjc, then use (api.apjc.etc.cisco.com) 

## Usage (required)

Execute with python
```bash
python3 etd_top_target.py
```

## Email

Sample email report looks like this. It is not pretty, it can be further improved and customized. 
![](etd-email.jpg)



## Schedule (optional)

My sample cron job to run at 1am every midnight
```bash
crontab -e

0 1 * * *     python3 ~/ETD_Email_Script/etd_top_target.py
```

## References and useful links
ETD Guide -> https://www.cisco.com/c/en/us/td/docs/security/email-threat-defense/user-guide/secure-email-threat-defense-user-guide/intro.html

ETD API Guide -> https://developer.cisco.com/docs/message-search-api/


