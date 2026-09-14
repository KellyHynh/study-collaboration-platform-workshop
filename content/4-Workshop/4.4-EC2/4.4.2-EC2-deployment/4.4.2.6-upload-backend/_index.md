---

title: "Upload Backend Source Code to EC2"

date: 2026-09-14

weight: 6

chapter: false

pre: " <b> 4.4.2.6. </b> "

---

The backend source code needs to be uploaded to the EC2 instance.

Git can be used to clone the repository:

git clone <repository-url>

Then move into the backend directory:

cd <backend-directory>

Check the source code:

ls

Then install the required dependencies:

npm install

Check `package.json` and make sure that the required backend dependencies are available.
