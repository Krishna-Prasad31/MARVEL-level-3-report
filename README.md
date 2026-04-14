# MARVEL-level-3-report

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

I installed Jenkins using docker through WSL and required plugins such as Docker Pipeline were installed. Once the setup was completed I was able to open Jenkins was accessed through *localhost*. After creating my account I created a new pipeline and started writing the pipeline script. Once I completed the scripting part I ran the build , i ran into some errors before the build finally passed successfully. I learnt a lot of new things from failed builds and understood by reading the output terminal.

Finally when the CI part was sorted the CD automatically deployed it in vercel and the webapp was up and running.

[Tenzies](https://tenzies-cici2qxkw-krishna-prasad31s-projects.vercel.app/)

![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(763).png?raw=true)
![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(762).png?raw=true)
![Jenkins](https://github.com/Krishna-Prasad31/MARVEL-level-3-report/blob/main/Screenshot%20(764).png?raw=true)


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

