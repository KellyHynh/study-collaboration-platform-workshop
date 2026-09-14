---

title: "Connect to EC2 Using SSH"

date: 2026-09-14

weight: 4

chapter: false

pre: " <b> 4.4.2.4. </b> "

---

After the instance is created, use SSH to access the server.

For example:

ssh -i <key-file> ec2-user@<EC2_PUBLIC_IP>

After the connection is successful, the terminal will switch to the environment of the EC2 instance.

For example:

[ec2-user@ip-172-31-xx-xxx ~]$

From this point, the following commands are executed directly on the EC2 instance.

![Connect to EC2 Using SSH](images/4-Workshop/4.4-EC2/6.png)
