# Guacamole + Docker Setup
Following are the instruction on how to setup Guacamole in docker and use it to SSH into the host Machine
## Step 1
Create the Guacamole Docker Container, i personally use this image `flcontainers/guacamole`. Source for the image can be found here https://github.com/flcontainers/guacamole.
Create Container like this
```
docker run -d --name=guacamole --restart=always -p 8080:8080 -v guacamole_data:/config flcontainers/guacamole
```
Change the command according to your need. Default username and password is 
```
guacadmin
```

## Step 2
After creating the container you need to find the ip address of `docker0` network, which will allow the container to make the SSH connection to the host machime.
It can be found using the following CMD
```
ip addr show docker0
```
Output may look something like this
```
5: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:98:77:38:cd brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:98ff:fe77:38cd/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
```
Then the IP address that will be used should look like this `172.17.0.1`

## Setp 3
Create an SSH connection in guacamole where in network it asks for hostname type the ip address of `docker0`
If everything was setup right you should be able to get a ssh terminal in guacamole.
