# Deploying-Node.js-Application-on-AWS-EC2
Demonstrates deploying a Node.js application on AWS, covering EC2 setup, IAM, environment variables, and scalability tips for beginners.

### 1] Set Up an AWS EC2 Instance

a.  Create an IAM User & Log in to Your AWS Console

Go to the IAM Console.
  - Click on Users on the sidebar, then click Add user.
  - Enter a username.
  - Select Access type: Choose Password.
  - Attach permissions: Select Attach existing policies directly and choose AdministratorAccess to give full access.
  - Complete the steps and save your Access Key ID and Secret Access Key for future use.

Log in to the AWS Console
  - Use the IAM user credentials you just created.

b.  Create an EC2 Instance

  - Navigate to EC2 Dashboard.
  - Click Launch Instance.
  - Configure Instance :
      - Region : Select N. Virginia (us-east-1).
      - Name : Enter Demo-nodejs.
      - Amazon Machine Image (AMI) : Choose Ubuntu Server 22.04 LTS.
      - Instance Type : Select t2.micro (Free Tier eligible).
      - Key Pair : Create a new key pair - Give it a name and download the `.pem` file. Save it securely, as it’s needed for SSH access.
      - Configure Security Group : Create a new Security Group with the following inbound rule -
          - Type: SSH
          - Protocol: TCP
          - Port Range: 22
          - Source: Anywhere (0.0.0.0/0)
  - Review and launch the instance.
  - Select the key pair you created earlier and acknowledge that you have access to the key.

c.  Connect to Your EC2 Instance

Open the terminal and use the following command to connect :
```
ssh -i /path/to/your/keypair.pem ubunutu@<IP_ADDRESS>
```
Replace /path/to/your/keypair.pem with the path to your `.pem` file and <IP_ADDRESS> with the public IP address of your EC2 instance.


### 2] Configuring Ubuntu on the Remote VM

a.  Update Packages and Install Dependencies
```
sudo apt update
```
b.  Install Git
```
sudo apt install git
```
c.  Verify Installation
```
git --version
```
d.  Install Node.js
```
sudo apt install nodejs
```
e.  Verify Node.js Installation
```
node -v
```
f.  Install npm (Node Package Manager)
```
sudo apt install npm
```
g.  Verify npm Installation:
```
npm --version
```

▪ References:
      - Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04)
      - Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)


### 3] Deploying the Node.js Project on AWS

a.  Clone Your Project
```
git clone [https://github.com/prajwalchapke055/Deploying-Node.js-Application-on-AWS-EC2.git]
```

b.  Set Up Environment Variables - Navigate to the Project Directory - 
```
cd AWS-Session
```
Create the .env File : 
```
touch .env
```
Open the .env file for editing :
``` 
vi .env 
```

Add the following environment variables:
```
DOMAIN=""
PORT=3000
STATIC_DIR="./client"

PUBLISHABLE_KEY="pk_test_XXXX"
SECRET_KEY="sk_test_XXXX"
```

Get Stripe API Keys:
  - Go to Stripe and create an account. [Stripe Link](https://stripe.com/in)
  - Navigate to Developers → API Keys to get your Publishable Key and Secret Key.
  - Update .env file with your Stripe keys and domain.

c.  Initialize and Start the Project
Install Dependencies:
```
npm install
```
Start the Application:
```
npm run start
```

d.  Update Security Group Rules
Go to EC2 Dashboard:
  - Select Instances and find your instance.
  - Click on the Security tab and then Edit inbound rules.
  - Add a New Rule:
    - Type: Custom TCP
    - Port Range: 3000
    - Source: Anywhere (0.0.0.0/0)
    - Save the rules.

e. Access Your Node.js Application
Open a browser and visit:
```
http://<YOUR_ELASTIC_IP>:3000
```
Replace <YOUR_ELASTIC_IP> with the Elastic IP address associated with your EC2 instance.


### 4] Troubleshooting
If you can’t access your application:
  - Ensure the security group rules are correctly configured.
  - Verify that the `.env` file contains the correct environment variables.
Check the application logs for errors:
```
npm run start
```
For any errors :
      - Look into the [Node.js documentation] or check relevant GitHub issues for solutions.
      - Reference GitHub Link [Day-12 Deploying `Node.js` Application on AWS EC2 | Feat.[[ @kunal](https://github.com/verma-kunal](https://github.com/verma-kunal/AWS-Session))]
      - Reference YouTube Video Link [Day-12 Deploying `Node.js` Application on AWS EC2 | [@AbhishekVeeramalla](https://youtu.be/NLmF64KdLN0?si=7TXILzusgqof6Oak) | Live Project]

### 5] ScreenShots(Output)

![Screenshot (609)](https://github.com/user-attachments/assets/d19f8f60-98a9-4262-a852-0bdd44c7dbf9)

![Screenshot (610)](https://github.com/user-attachments/assets/d2a1da32-2866-43b8-87c5-64a89603005a)

### Congratulations! 🎉 We’ve successfully deployed a Node.js application on AWS EC2.
