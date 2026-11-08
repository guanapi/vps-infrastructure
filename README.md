# Code Factory, Cloud Infrastructure & Linux Hardening

## Porject

This a code factory project that I have with a friend who is a senior developer. The goals for this project are:

1. Learn more how to use agents and configure them.
2. In my case, get into the AI world and learn from his experience.
3. Put in practise what I learned and learned more about Linux infrastruture by doing.
4. Get passive incomes through the apps and see if it can generate other business.

- **Cloud:** Oracle Could Infrastructure (OCI Compute) - Always free tier (AMR 2 OCPU + 12 GB RAM)

- **OS:** Ubuntu 26.04.1 LTS

- **Security:** Only SSH port available inbound, UFW, Fail2ban, SSH Key-pair with passphrase

- **Services:** Telegram bot 

## OS Hardening & Security

- I created a SSH users group, to limit the access to the server.
- I edit the sshd_config file to limit to achieve:
1. Don't allow users to set enviroment variables (specially the agent)
2. Disable the password login to avoid brute force attacks.
3. Disable port forwarding
4. Disable root login
5. Dasable user environment
6. Disable X11Forwarding
7. Disable port forwarding
8. Use DNS to match IP
9. Disable TCP Keep Alive
10. Limit the users alive to 3
11. Set the listening IP address
12. Limit the max sessions to 2
13. Limit the max startups to 10:30:60
14. Closed all ports because I am using Tailscale.

- I remove the Shrot Diffie-Hellman Keys

- I limit the who can use sudo and su, so the groups with privileges can only use it. Even we are only two people working in this project, but I have to limit the agents.

- I configurate NTP because many security protocols leverage the time, so I want to avoid negative impacts in the server

### Automatic Security Updates and Alerts

- I want to be as safe as possible, so I automatize the unattended, updatesof critical security patches and the server will send me an email to notify me.