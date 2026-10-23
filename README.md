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

## OS Hardening

- I created a SSH users group, to limit the access to the server.
- I edit the sshd_config file to limit to achieve:
1. Don't allow users to set enviroment variables (specially the agent)
2. Disable the password login to avoid brute force attacks.
3. Disable port forwarding
4. Disable root login