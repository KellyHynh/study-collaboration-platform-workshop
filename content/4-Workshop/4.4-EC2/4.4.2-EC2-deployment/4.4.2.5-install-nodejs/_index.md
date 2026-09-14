---

title: "Update System and Install Node.js"

date: 2026-09-14

weight: 5

chapter: false

pre: " <b> 4.4.2.5. </b> "

---

After logging in to the EC2 instance, update the system packages:

sudo dnf update -y

Check the operating system:

cat /etc/os-release

Then install Node.js using a version that is compatible with the backend.

Check the installed versions:

node -v

npm -v

The result should confirm that Node.js and npm have been installed successfully.

![Node.js Installation](/images/4-Workshop/4.4-EC2/7.png)
