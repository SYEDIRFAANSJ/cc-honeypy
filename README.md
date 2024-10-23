![honeypy-logo-black-text](https://github.com/user-attachments/assets/da1b6a32-25ac-4250-9696-4e7eed4d821c)
# *HONEYPOT*
This honeypot simulates vulnerable systems to attract potential attackers and log their activity for analysis. By mimicking real services, it helps security professionals understand attack patterns, tactics, and tools. This project can be customized to simulate different network services, providing valuable insights into potential threats.

# Install

**1) Clone repository.**
`git clone https://github.com/SYEDIRFAANSJ/cc-honeypy.git`

**2) Permissions.**
Move into `ssh_honeypy` folder.

Ensure `main.py` has proper permisions. (`chmod 755 honeypy.py`)

**3) Keygen.**

Create a new folder `static`. 

`mkdir static`

Move into directory.

`cd static`

An RSA key must be generated for the SSH server host key. The SSH host key provides proper identification for the SSH server. Ensure the key is titled `server.key` and resides in the same relative directory to the main program.

`ssh-keygen -t rsa -b 2048 -f server.key`

# Technologies Used
**1) Backend: Python**

**2) Frontend: HTML**

**3) Monitoring & Logging: Uses various Python libraries for data capture and logging**

**4) Database: Stores logs and interactions for analysis (could be integrated with a database of choice)**

**Optional Arguments**

A username (`-u`) and password (`-w`) can be specified to authenticate the SSH server. The default configuration will accept all usernames and passwords.

```
-u / --username: Username.
-w / --password: Password.
-t / --tarpit: For SSH-based honeypots, -t can be used to trap sessions inside the shell, by sending a 'endless' SSH banner.
```

Example: `python3 main.py -a 0.0.0.0 -p 22 --ssh -u admin -w admin --tarpit`

# Logging Files

HONEYPY has three loggers configured. Loggers will route to either `cmd_audits.log`, `creds_audits.log` (for SSH), and `http_audit.log` (for HTTP) log files for information capture.

`cmd_audits.log`: Captures IP address, username, password, and all commands supplied.

`creds_audits.log`: Captures IP address, username, and password, comma seperated. Used to see how many hosts attempt to connect to SSH_HONEYPY.

`http_audit.log`: Captures IP address, username, password.

The log files will be located in `../ssh_honeypy/log_files/..`

# Honeypot Types
This honeypot was written with modularity in mind to support future honeypot types (Telnet, HTTPS, SMTP, etc). As of right now there are two honeypot types supported.

## SSH
The project started out with only supported SSH. Use the following instructions above to provision an SSH-based honeypot which emulates a basic shell.

💡 `-t / --tarpit`: A tarpit is a security mechanism designed to slow down or delay the attempts of an attacker trying to brute-force login credentials. Leveraging Python's time module, a very long SSH-banner is sent to a connecting shell session. The only way to get out of the session is by closing the terminal. 

## HTTP
Using Python Flask as a basic template to provision a simple web service, HONEYPY impersonates a default WordPress `wp-admin` login page. Username / password pairs are collected.

There are default credentials accepted, `admin` and `deeboodah`, which will proceed to a Rick Roll gif. Username and password can be changed using the `-u / --username: Username.
-w / --password: Password` arguments.

The web-based honeypot runs on port 5000 by default. This can be changed using the `-p / --port` flag option.

💡 There is currently not a dashboard panel supported for HTTP-based results. This will be a future addition.

# Future Features

- Write additional support for common protocols:
- Telnet 
    - HTTP ✅
    - HTTP(S)
    - SMTP
    - RDP
    - DNS
    - Telnet
- Custom DNS support.
- Docker support for host-based isolation and code deployment.
- Systemd support to run Python script in background. ✅
- Create a basic overview Dashboard. ✅
- Dynamic Dashboard Updates.
- Dashboard hosted on seperate host to get results independent on honeypot host.
- Add SSH Banner Tarpit to trap SSH sessions ✅ (`-t, --tarpit`)
