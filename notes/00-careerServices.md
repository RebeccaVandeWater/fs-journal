# Career Services

#SECTION - Linkedin Review
- ✅ Change banner to look more tech-y
- ✅ Fill header with more skills and hobbies, life-long learner
- Make more connections (I'm about to graduate/I have graduated from Code Works, I'd love to connect)
  - Focus on people who work at companies that you want to work at, make these more personalized based on their job title or what they have posted
- About me:
  - Add quantifiable data like languages or softskills
  - Avoid paragraphs, make more bullet points
  - Add Headers and talk baout the skills or experiences in bullet points
  - Use Tyler Rice or Jordan as a reference, thomas powner
  - Connect to headers where it makes sense
- ✅ Activity: 
  - Engage as much as possible to stay in the algorithm:
    - Post, repost, comment, like, repost and comment on the reposted thing
    - Time box how often you stay on Linkedin to stay in the algorithm
- Experience: 
  - Move volunteering items into the volunteering section
  - ✅ Change the content of the experience into bullet points, use resume as a reference
  - ✅ Move the order of the skills so that employers can see the languages first
  - ✅ Get rid of irrelevant skills like seesaw and google classroom
- Get a free premium so that you can connect with recruiters, wait until after the final
- Education
  - ✅ Add GPA from graduation from BSU and CWI, any quantifiable data like hours working on a project


#SECTION - Career Week

#STUB - Tuesday Lecture
- SSH > Secure Shell
  - Works exclusively in the command line

- VPC > Virtual Private Cloud > Your private network within the cloud environment

- Subnet > Allows two computers to talk to each other on the same network. The computers will have the same IP address except for the last subset of numbers. A 0.0.0.0 IP address allows you to talk to any computer in the world.

- When working with cloud-based things, networking will be very important. However, networking is its own specialty and we will only know a small part of it to work with the cloud.

- Linux-based OS, with Ubuntu as the tool that talks to it

- Setting up a cloud-based service is configuring an OS, it will NOT work if you miss a step

- AWS gives us a public IP address that allows us access to the internet that forwards a user to your server

- An HTTPS request uses port 443, an HTTP request uses port 80. All requests on the internet use ports to communicate with servers and computers. 

- OpenVPN, free to deploy vpn that doesn't sell your info!

- DNS > A registry of url's that will go to a specific IP address. Makes it way easier to access websites!

- sudo !! will run the previous command with sudo in front of it

  #ANCHOR - Setting up an AWS Server
  - Create an account at aws.amazon.com

  - Click on Services Tab
    - Click on EC2 > Virtual Machines > An EC2 is a virtual computer that is deployed that you will have access to. 
  
  - Go to Instances, launch an instance
    - Stick to the servers that say "free"
    - Name your server
    - Switch to Ubuntu for the server > it's the typical version of Linux, doesn't have red tape that might get in your way.
    - a "yum" install need to be switched to an "ept" install, yum is AWS's Linux
    - Click the drop down to see the OS's that you can choose from. Click on 22.04 or 20.04, they are free
    - Make sure the architecture is on x86 as it supports software that Arm doesn't yet support
    - x86 is typically used by Windows, Arm is used by Apple. These specify the computer hardware that the server is run on. Make sure to research the difference as some cloud items are not compatible with one of them.
    - For instance type, use t2.micro as it is free. 
    - On Key pair, create a new key, leave the defaults, give it a name, and create it. 
      - You will have a download that will then launch, make sure not to delete it
    - Network Settings:
      - Create security group
      - Configure Security group
        - Leave the detault on the VPC > This sets up the router that allows your computer to talk to the rest of the world from a new IP address. Essentially, your computer's IP address will be put into a new, globally connected box.
      - No preferece on Subnet
      - Name your security group
      - Add a custom security group rule:
        - Type: MySQL/Aurora (will serve on port 3306)
        - Source Type: Anywhere (typically very dangerous, don't do it. It allows anyone who knows my IP address to connect to my database, which is really bad. However, since we're not storing important information it's okay. A production environment will not allow this, however.)
    - Leave configure storage as default. You get 30 GB of storage for free.
    - Leave Advanced details as is.
      - Spot instance only creates an instance in the cloud if it's available. It basically makes your cloud way cheaper to spin up.
    - Launch Instance!

  #ANCHOR - Setting up the MySQL server
  - Super User Do (sudo), acting as if you are the administrator
  - Python will come pre-installed in your Linux system!
  - The Linux OS costs almost nothing to run, hardware-wise
  - Nano > built in text-editor for Linux, like VSCode but less fancy > Not the CLI!
  - A d on a file means damien, which runs the server that runs the code
  - When creating a user, put their name in '' if you are using special characters. If you aren't using special characters, don't worry about it
  - The '%' means remote IP. It allows the user to access the database from a remote IP address. Make sure that your password is secure, otherwise malicious users can access your database from anywhere in the world.
  - The curl command allows you to make an HTTP request, you can even hit websites with that command
  - -o means output, it saves whatever you install to a file on your disc
  - pm2 is a node module that will spin up your service and keep it running. Nodemon will do the same thing, but doesn't have as many services as pm2
    - install with:
      npm install -g pm2