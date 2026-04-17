# MARVEL-level-2-report

# Task1: AWS Lambda:
AWS Lambda is one of many services provided by Amazon Web Services. Using Lambda developers can execute code without needing to provision or manage servers. It follows and event driven architechure, where fucntions(Lambda function) are triggered in response to specific events such as HTTP request, file upload , database updates, etc...AWS Lambda is a Function-as-a-Service (FaaS) platform.

For this task i created a chat application using AWS Lambda and API gateway services. The following Lambda functions were developed to handle different stages of communication in the chat application:

1. websocket-connect
- Triggered when a client connects to the WebSocket API
- Establishes a connection between client and server
- Stores connection details if required
3. websocket-disconnect
- Triggered when a client disconnects
- Removes or cleans up connection data
- Ensures efficient resource management
4. chat-handler
- Core logic of the chat application
- Processes incoming messages from users
- Generates appropriate responses
- Implemented using Node.js runtime
5. websocket-send
- Responsible for sending messages back to clients
- Handles outgoing communication
- Ensures real-time message delivery

## How this works
- the user sends a request to the API gateway whilst interacting with the frontend
- API gateway receives the request and forwards it to the lambda function which is intended to be used
- Lambda function sends response to the user through API gateway.

![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(665).png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/AWS1.png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/AWS2.png?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(739).png?raw=true)



# Task 2: CI/CD Pipeline using Jenkins

CI/CD is a modern software development practice that enables developers to automate integration and deployment processes. It combines CI(Continuous Integration) which involves automatically building and testing whenever changes are pushed and CD(Continuous Delivery) ensures the application is automatically deployed after the CI is successfully completed.

The objective of this task was to understand and implement a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins. The pipeline automates the process of fetching code, building the application, and deploying it to a production environment.

The basic architecture goes like this:

GitHub Repository → Jenkins Pipeline → Docker (Node Environment) → Build → Vercel Deployment → Live Application

I pulled Jenkins using docker through WSL and required plugins such as Docker Pipeline were installed. Once the setup was completed I was able to open Jenkins. It was accessed through *localhost*. After creating my account I created a new pipeline and started writing the pipeline script. Once I completed the scripting part I ran the build , i ran into some errors before the build finally passed successfully. I learnt a lot of new things from failed builds and understood by reading the output terminal.

Finally when the CI part was sorted the CD automatically deployed it on vercel and the webapp was up and running.

[Tenzies](https://tenzies-cici2qxkw-krishna-prasad31s-projects.vercel.app/)

![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(763).png?raw=true)
![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(762).png?raw=true)
![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(764).png?raw=true)

[Tenzies](https://tenzies-cici2qxkw-krishna-prasad31s-projects.vercel.app/)


# TASK 4: Terraform

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It enables users to define, provision, and manage infrastructure using a declarative configuration language.

Instead of manually creating resources through cloud consoles, Terraform allows automation using code. This improves consistency, reduces human error, and enables easy and hassle free collaboration within a team. Terraform interacts with cloud providers such as **AWS, Google Cloud, Microsoft Azure, etc...**. Terraform connects to the cloud providers through API making it highly flexible and platform independent.

## Flow of Terraform Execution:

The process begins by defining infrastructure using Terraform configuration files (.tf files).

- `terraform.tf` → Defines required providers and Terraform settings
- `main.tf` → Contains infrastructure (VPC, subnets, EC2, etc.)
- `variables.tf` → Stores input variables
- `outputs.tf` → Defines output values

These files collectively describe the desired state of the infrastructure.

### commands used:

`terraform init`: During initialization Terraform downloads the AWS provider from HashiCorp registry Required modules (like VPC module) are installed Backend (local or cloud) is configured. This step prepares Terraform to interact with Amazon Web Services APIs.

`terraform validate`: This checks the for logical errors in the code, checks syntax and ensures the code runs errorless before execution.

`terraform plan`: Here Terraform Reads configuration files and compares with current state (terraform.tfstate) and finally Generates an execution plan.

Eg: creating VPC, subnets or creating EC2 instance

`terraform apply`: This is the execution phase .Terraform sends API requests to AWS , AWS provisions resources (VPC, subnets, etc.) A state file (terraform.tfstate) is updated. This is wher infrastructure goes live. Whenever you modify the configuration this command must me used to update the changes.

`terraform destroy`: Terraform reads the state file and identifies all managed resources then sends delete requests to AWS. finally after the command is ran the  created infrastructure is removed.

![terraform](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(611).png?raw=true)
![terraform](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(617).png?raw=true)

# TASK 10: NMap

Nmap (Network Mapper) is an open-source tool used for network discovery and security auditing. It is widely used by system administrators and cybersecurity professionals to identify active hosts, open ports, services, and operating systems in a network. Nmap works by sending specially crafted data packets to see how target systems respond and analyse the data received.

For this task I logged into Kali Linux from the VirtualBox. I pentesed the host windows system, to make the virtual machine a distinct machine from windows i selected the network adapter to bridged adapter. Then I opened the Linux terminal(command line) and started pentesting on the ip of the windows system.

Fristly I tried to check check if the host is alive or responding, for this purpose I used `ping <ip address>`. This command ran successfully and we can see that the target IP is responding.
![nmap](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2012.40.29.jpeg?raw=true)

for port scanning I used `nmap -sS -T4 192.168.56.1`. This performs a SYN(stealth) scan and -T4 is used for faster execution. Ports are of three states based on the response of the target IP

If it replies
- SYN-ACK - Open port
- RST - Closed port
- null - filtered ports

open ports actively accept connections, A closed port is reachable BUT no service is listening and A filtered port is being blocked by a firewall.

I used `nmap -sV 192.168.56.1` for service detection. By running this command I could clearly identify services running on open ports and detect service versions

Some important PORTS are:

## 445 : SMB 

These are big targets

File sharing, Network communication, Historically vulnerable (e.g., EternalBlue)

This is usually the first thing pentesters look at.

## 3306 : MySQL

This means:

A database server is running
Might allow: Weak passwords and remote access

## 3389 : RDP

Remote Desktop Protocol

Allows remote login to Windows , Huge attack surface: Brute force, Credential attacks

![nmap](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/nmap2.jpeg?raw=true)

## Observation
- SMB (445) was open but did not reveal data due to authentication
- RPC (135) available for communication
- NetBIOS (139) exposed legacy services
- HTTP API (3380) identified as potential entry point

![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2012.40.27.jpeg?raw=true)
![website](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2012.40.27%20(1).jpeg?raw=true)

# TASK 5: Wireshark

Wireshark is a network packet analyzer used to capture, inspect, and troubleshoot data being transmitted across a network. It allows users to monitor traffic over different network interfaces such as Wi-Fi and Ethernet.

Wireshark provides detailed insights into how data flows across a network and how different protocols operate.

## 2. Working of Wireshark

To verify that Wireshark is functioning correctly:

- Start packet capture  
- Open a web browser and search for any website  
- Observe packets being captured in real time  

This confirms that network traffic is being monitored successfully.

## 3. Filters in Wireshark

Filters are essential for efficient packet analysis.

### Capture Filters
- Applied before capturing packets  
- Capture only specific traffic  

### Display Filters
- Applied after capturing packets  
- Hide unwanted packets and show relevant ones  

### Examples
tcp
dns
ip.addr == 192.168.56.1


### Logical Operators
- AND  
- OR  
- NOT (`!=`)  

## 4. Important Features in Wireshark

### Statistics Menu
Used to analyze traffic patterns:

- Capture summary  
- Conversations  
- Endpoints  
- Packet lengths  

### Flow Graph
- Visual representation of packet communication  
- Helps understand request-response flow  

### TCP Stream Graphs
Used to analyze:
- Latency  
- Throughput  
- Packet behavior  


## 5. Key Networking Concepts

### DHCP (Dynamic Host Configuration Protocol)
- Assigns IP addresses dynamically to devices on a network  

### TCP Three-Way Handshake

- Client → SYN → Server
- Server → SYN,ACK → Client
- Client → ACK → Server


Establishes a reliable connection between client and server.

### Connection Reset (RST Packet)

- If the server sends an **RST (Reset)** packet  
- It indicates that the connection has failed or was rejected
  
## 6. Observations

- Network traffic was successfully captured using Wireshark  
- Filters helped isolate specific protocols  
- TCP communication patterns were observed  
- Three-way handshake process was identified  
- RST packets indicated failed or rejected connections  
- Retransmissions and duplicate acknowledgments may indicate packet loss or congestion

## 7. Conclusion

Wireshark is a powerful tool for analyzing network traffic and understanding communication between systems. It helps in identifying network issues, analyzing protocols, and detecting anomalies in packet flow.

![wireshark](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2015.11.58.jpeg?raw=true)
![wireshark](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2015.27.28.jpeg?raw=true)
![wireshark](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2015.27.29%20(2).jpeg?raw=true)
![wireshark](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2015.27.29.jpeg?raw=true)

# TASK 6: Docker

Docker is an open-source containerization platform that enables applications to be packaged along with their dependencies into lightweight containers. These containers ensure that applications run consistently across different environments such as local machines, cloud platforms, and distributed systems.

Unlike traditional virtual machines, Docker containers share the host operating system, making them faster, more efficient, and lightweight.


## Flow of Docker Execution:

The process of using Docker follows a simple workflow:

![docker](https://editor.analyticsvidhya.com/uploads/40489Capture.PNG)

## Key concpets:

### Container:
A container is a lightweight and portable environment that runs an application along with its dependencies.

### Image:
A Docker image is a read only, pre-packaged template that contains an application along with all its dependencies, libraries, and environment needed to run it, and is used to create containers.

### Dockerfile:
A Dockerfile is a script that contains instructions to build a Docker image.

### Docker Hub:
Docker Hub is an online repository used to store and share Docker images.

### Docker Volume:
A Docker volume is a way to store data outside a container so that the data is not lost when the container stops or is deleted.

### Docker daemon:
A Docker daemon is the background service that manages Docker containers, images, networks, and volumes, and handles all Docker operations on the system.

## Virtual Machines (VMs) also provide isolated environments similar to Docker containers. Why should we choose Docker over Virtual Machines?

Although both Virtual Machines and Docker containers provide isolated environments, Docker is generally preferred due to its efficiency, speed, and lightweight nature.
Virtual Machines run a complete operating system along with the application, which makes them heavy, slower to start, and resource-intensive. Each VM requires its own OS, memory, and storage, leading to higher overhead.
In contrast, Docker containers share the host operating system kernel and only include the application and its dependencies. This makes containers lightweight, faster to start, and more efficient in resource utilization.
Additionally, Docker enables faster deployment and scalability, allowing multiple containers to run on the same system with minimal overhead. This is especially useful in modern DevOps and cloud environments.
However, Virtual Machines provide stronger isolation since each VM has its own OS, making them more suitable for scenarios requiring high security and complete system isolation.
![docker](https://k21academy.com/wp-content/uploads/2020/11/Docker-and-Vm-blog-image-1_result-1.webp)

## Docker commands

- `docker pull <image>`  : Download an image from Docker Hub  

- `docker images` : List all downloaded images  

- `docker rmi <image_id>` : Remove an image  

- `docker run <image>`  : Create and run a container  

  `docker run -d <image>`  : Run container in background (detached mode)  

- `docker run -p <host_port>:<container_port> <image>` : Run container with port mapping  

- `docker ps` : List running containers  

- `docker ps -a` : List all containers (including stopped ones)  

- `docker stop <container_id>` : Stop a running container  

- `docker start <container_id>` : Start a stopped container  

- `docker restart <container_id>` : Restart a container  

- `docker rm <container_id>` : Remove a container  

- `docker build -t <image_name> .` : Build an image from a Dockerfile  

- `docker tag <image> <new_name>` : Tag/rename an image  

- `docker logs <container_id>` : View container logs  

- `docker exec -it <container_id> bash`  : Access container terminal  

- `docker inspect <container_id>` : View detailed container information  

- `docker port <container_id>` : Show port mappings
  
- `docker volume create <name>` : Create a volume  

- `docker volume ls` : List volumes  

- `docker volume rm <name>`  : Remove a volume

  ![docker](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%202026-04-14%20164211.png?raw=true)
  ![docker](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(772).png?raw=true)

# TASK 7: Dockerize

## Aim  
Dockerizing an application is the process of packaging the application along with all its dependencies, configurations, and runtime environment into a container image, so that it can run consistently across different systems.

Dockerizing an application can be compared to packing a complete travel suitcase before going on a trip. Instead of relying on the destination to provide everything you need, you pack all essentials—clothes, charger, documents—into one suitcase so you’re fully prepared wherever you go

 
In this task, I created a Dockerfile for the backend, ran a database container, connected both using a bridge network, and used volumes for storing data.

### Bridge Network:

A bridge network in Docker is the default network driver that allows multiple containers to communicate with each other on the same host. It creates a private internal network where containers can interact using IP addresses or container names. Containers connected to a bridge network are isolated from external networks unless explicitly exposed through port mapping.

### Volumes:

A Docker volume is a persistent storage mechanism used to store and manage data independently of containers. Volumes are managed by Docker and exist outside the container’s filesystem, ensuring that data is retained even if the container is stopped, removed, or recreated. They are commonly used for databases, user data, and application state.

### Storage:

Container storage refers to the data stored within a container’s writable layer. This storage is temporary and tied to the lifecycle of the container, meaning any data stored inside the container is lost when the container is deleted. It is suitable for short-term or non-critical data, while persistent data should be stored using volumes or external storage.
 


First, I created a custom bridge network so that my containers could communicate with each other:
![docker](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(773).png?raw=true)


Then, I created a Dockerfile for my backend application:
![docker](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(800).png?raw=true)

After that, I built the Docker image and then I ran a MongoDB container and also created a volume so that my data would not be lost, Finally, I ran my backend container and connected it to the same network
![docker](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(805).png?raw=true)


# TASK 9: Hashing

Hashing is a technique used to convert data (like a password) into a fixed-length string of characters, called a hash. You can think of it like a fingerprint for your data — every input produces a unique output.

For example, if I hash the password:
`hello123`

I might get something like: `ef92b778bafe771e89245b89ecbc...`

The same input will always produce the same hash. But even a tiny change (like hello124) will produce a completely different hash
So instead of storing the actual password, systems store the hash, and during login they compare hashes instead of raw passwords.

## Hashing vs Encryption:
![hashing](https://miro.medium.com/v2/resize:fit:1400/1*8uhYhVj4xDnKZ3clEYMKSA.png)

Hashing functions are designed to be one-way functions. It is easy to generate a hash from input, but extremely hard (practically impossible) to reverse it. There is no “decrypt hash” function. The only way to guess the original password is to try inputs and compare hashes, which is computationally expensive.

## Collision:
A collision happens when two different inputs produce the same hash.

for example:

- input1 → hash X  
- input2 → hash X

This is rare in strong hashing algorithms (like SHA-256), but theoretically possible.

Good hashing algorithms are designed to:
- Minimize collisions
- Make them extremely difficult to find

 # Rainbow Tables & Dictionary Attacks

Even though hashes cannot be reversed directly, attackers use tricks:

1. Dictionary Attack

They take a list of common passwords like:

- 123456, password, admin, qwerty

Hash them, and compare with stolen hashes.

2. Rainbow Tables

These are precomputed databases of passwords and their hashes.
Instead of calculating hashes every time, attackers just look them up.

We can prevent this by :

### Salting
Salting is a method used to improve password security by adding a random string (called a salt) to the password before hashing it. This ensures that even if two users have the same password, their hashes will be different. It also protects against rainbow table attacks, since attackers cannot rely on precomputed hashes. The salt is usually stored along with the hashed password and does not need to be kept secret.

### Peppering
Peppering is similar to salting, but the key difference is that the pepper is kept secret. It is a fixed value added to the password before hashing, but it is not stored in the database. Instead, it is stored securely in the application. This means that even if the database is compromised, attackers cannot easily crack the passwords without knowing the pepper, making the system more secure.

this is the program I created to hash passwords, it uses `hashlib` and SHA256 as cryptic function used to generate fixed size 256-bit data. Here the user can register and input the password and can login using those credentials. the hashed password will get stored in a json file.
![hashing](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(806).png?raw=true)
![hashing](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(808).png?raw=true)

# Task 8: Webscraping flight ticket prices

Web scraping is a technique used to extract data from websites automatically. Modern websites like Kayak use dynamic content loading and interactive user interfaces, which makes data extraction more complex than simple static HTML parsing.

For this task I built a program that automatically searches for flights on Kayak and extracts relevant flight data then stores the data in a structured format and finally automatically sends the results via email

From this task I learnt how selenium works and how it helps in automation of actions in a website which we can see in realtime , in addition to that I understood how to fine tune the program to execute with minimal failures. Got a good understanding of how the data is converted into a csv and sent to email addresses.

In this task I faced some challenges such as some class names were not reliable and the date selector was not working correctly. I countered the problems by understanding the DOM clearly and started using label instead of classed.

## What is Selenium?

Selenium is an open-source automation tool used to control web browsers programmatically.

It allows developers to:

- Open websites
- Click buttons
- Fill forms
- Navigate pages
- Extract data

In this project, Selenium is used to simulate real user interaction with the Kayak website.

## Working of Selenium:

1. Python code sends commands
2. Selenium WebDriver translates them
3. ChromeDriver communicates with the browser
4. Browser executes actions
5. Response is returned back

`driver.find_element(By.XPATH, "//button").click()`

Tools used:

| Tool               | Purpose                   |
| ------------------ | ------------------------- |
| Python             | Programming language      |
| Selenium           | Browser automation        |
| ChromeDriver       | WebDriver for Chrome      |
| CSV module         | Data storage              |
| SMTP (smtplib)     | Email automation          |
| DevTools (Inspect) | DOM analysis              |

For this task i tried scraping for flights from Bengaluru to Los Angeles.


![scraping](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(809).png?raw=true)
![scraping](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(810).png?raw=true)
![scraping](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/WhatsApp%20Image%202026-04-14%20at%2021.53.59.jpeg?raw=true)

# TASK 3: SSH

Secure Shell (SSH) is a network communication protocol that enables secure remote access between systems. It uses encryption to protect data transfer and allows users to execute commands on remote machines.

The objective of this task is to understand SSH communication, identify sensitive key files on a system, and transfer them securely between servers.

## Tools and Technologies Used
- Docker (to simulate servers)
- Ubuntu (base container image)
- SSH (Secure Shell)
- SCP (Secure Copy Protocol)
- Linux Commands (find, scp, ssh)

Two Docker containers were created to simulate two independent servers:

- Server A → Source server (contains key files)
- Server B → Destination server (receives files)

Both containers were connected using a custom Docker network to enable communication between them.

SSH was installed and configured on both servers to allow remote access.

- Firstly I created two docker containers
  `docker run -dit --name serverA` 
  
`docker run -dit --name serverB ubuntu`

- Then installed and started SSH

`apt update`

`apt install -y openssh-server`

`service ssh start`

- Generated SSH Keys in serverA:

  `mkdir -p /home/keys`

  
`ssh-keygen -t rsa -f /home/keys/id_rsa_test -N "" `

This created:

- Private key → /home/keys/id_rsa_test
- Public key → /home/keys/id_rsa_test.pub

- Searched Entire System for Keys

  `find / -type f \( -name "id_rsa*" -o -name "*.pem" -o -name "*.pub" \) 2>/dev/null`

- Configuring SSH Authentication (Server B)

The SSH configuration file was modified:

`nano /etc/ssh/sshd_config`

Changes made:

- PermitRootLogin yes
- PasswordAuthentication yes

Then SSH service was restarted:

`service ssh restart`

- Transferring Keys Using SCP

  
`scp /home/keys/id_rsa_test root@serverB:/home/`



Finally SSH connection successfully established between servers and key files were identified using the find command. File transfer using SCP was successfully completed, the transferred file was verified on Server B

This task successfully demonstrated secure communication between two servers using SSH. It also highlighted how sensitive key files can be discovered and transferred across systems. The exercise provided practical knowledge of system security, file handling, and debugging in a controlled environment.

![ssh](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(815).png?raw=true)
![ssh](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(816).png?raw=true)
![ssh](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(818).png?raw=true)
![ssh](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(825).png?raw=true)
