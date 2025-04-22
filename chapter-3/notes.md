# Open SSH

- Open SSH is a remote management that gives you access to run commands on another machine through remote access
- Its a suite a utilities the most important of which are server and client components
- You can do ssh user-name@ip-address
- As it is difficult to remember ip-address you can create a file in .ssh/ named as config
  and can write the following in it :
- ssh -T <git@github.com> : Generally when you do ssh @user it gives you a Terminal interface
  In this instance that means Hey , I am not here to interact with a shell just do the auth and let github do whatever it wants
- There are two ways of copying ssh id_e25519 :

1. Copying pub key , logging into remote server and then pasting it in authorized_keys
2. ssh-copy-id -i ~/.ssh/id_ed25519.pub root/username@ip-address

```
Host (Give it any name)
  Hostname ip-a
  Port 22
  User user/root
```

Q)

1. What are ports ?
2. DNS Setup
3. What is the thingy with this IP ? How is he exposing it ? Is it a local IP ?
4. Write about man in the middle
