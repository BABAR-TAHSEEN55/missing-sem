# Open SSH

# SSH

- Open SSH is a remote management that gives you access to run commands on another machine through remote access
- Its a suite a utilities the most important of which are server and client components
- You can do ssh user-name@ip-address
- As it is difficult to remember ip-address you can create a file in .ssh/ named as config
  and can write the following in it :

```
Host (Give it any name)
  Hostname ip a  ## ( a is not a flag )
  Port 22
  User user/root
```

- ssh -T <git@github.com> : Generally when you do ssh user@ip it gives you a Terminal interface
  In this instance that means Hey , I am not here to interact with a shell just do the auth and let github do whatever it wants
- There are two ways of copying ssh id_e25519 :

1. Copying pub key , logging into remote server and then pasting it in authorized_keys
2. ssh-copy-id -i ~/.ssh/id_ed25519.pub root/username@ip-address

- It is always better to have different keys for different servers ( Recommended )
- ssh-keygen -t ed25519 -C "email/name (this is a comment , can be anything)"
  t-> Type
  C-> Comment
  if you don't comment it'll default it to username of the system

### Setting up SSH-Agent

- Type : eval $(ssh-agent)
  px aux | grep ssh-agent -> For checking if it works
  BOOM -> You have a staring ssh-agent
- ssh-add ~/.ssh/private_key

## Caveat

- If you have a bunch of ssh keys in your system and you are trying to access a server
  (SSH Connection) there is a high chance your server will be locked because it checks all the ssh keys to match the private key of the designated server
- ssh -i ~/.ssh/your_key user@host (NOTE: This has to be your private key )
  This is used to reference ( Hey ! Use this for the specific server for checking auth)

# Server-Side SSH config

- For Changes : go to /etc/ssh/sshd.config for Disabling password auth & Change ports etc

# Troubleshooting

1. Check & do tail -f /var/log/auth.log for live updates
   OR
   journalctl -fu ssh ( New way )
2. SSH dir should be accessed by solely by user and not root [ if this is the case ssh think its key is compromised and you wont be able to login into ]
   Q)
3. For changing ports in Ubuntu 22.10 or above you'll have to actually change it through systemd as it is the actual listener, even if you change it in /etc/ssh/sshd_config.d/ , it won't work
   Instead do this :

```
sudo mkdir -p /etc/systemd/system/ssh.socket.d
sudo nano /etc/systemd/system/ssh.socket.d/override.conf
Paste this in the above file
[Socket]
ListenStream=
ListenStream=2222
Run these :
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl restart ssh.socket
sudo systemctl restart ssh

Allow Ufw for desired PORT
sudo ufw allow 2222/tcp // Example 2222

```

# Setting Static Ip

- Ip is of two types :

1. Dynamic ip-address - Changes often when you are disconnected to the network for a long time etc..
   Solid Privacy
2. Static ip-address - Doesn't Change . Better for hosting etc

## How to set Static ip

Refer- <https://www.freecodecamp.org/news/setting-a-static-ip-in-ubuntu-linux-ip-address-tutorial/>

<!--- Get your networking concepts together-->

1. What are ports ?
   Ans : <https://www.plesk.com/blog/various/open-ports-in-linux/>
   It is a virtual point where all network connections start and end
   <https://www.plesk.com/blog/various/open-ports-in-linux/>
2. DNS Setup
3. What is the thingy with this IP ? How is he exposing it ? Is it a local IP ?
4. Write about man in the middle
5. Bots for looking into open PORTS like 22 as it is default as [ Changing Ports helps in securing like 1% ]
6. What is a firewall?
7. Learn about Systemd & systemclt & journalctl
8. What is VPN ? & VPS ?
