# AWS-LOAD-BALANCER

## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## COMMANDS
No CLI commands are used in this experiment, as it is performed entirely through the AWS Management Console (GUI-based setup) using EC2, Elastic Load Balancing, Auto Scaling, and CloudWatch services.

## OUTPUT
### REG NUMBER: 212224040061
### NAME: DEEPIKA R

<img width="1919" height="866" alt="Screenshot 2026-08-18 093033" src="https://github.com/user-attachments/assets/aa82b865-02ce-480d-b650-7bb377089286" />
<img width="1918" height="889" alt="Screenshot 2026-08-18 093101" src="https://github.com/user-attachments/assets/517b9b0d-c13a-4d94-b77f-9b07f3113e52" />
<img width="1919" height="879" alt="Screenshot 2026-08-18 093417" src="https://github.com/user-attachments/assets/f09ff30a-55db-4628-86c3-9bc60a2b57ed" />
<img width="1919" height="879" alt="Screenshot 2026-08-18 093657" src="https://github.com/user-attachments/assets/37e8404b-b72f-4aa2-9dfe-670e8b504387" />
<img width="1919" height="889" alt="Screenshot 2026-08-18 094121" src="https://github.com/user-attachments/assets/2356b0cf-41e1-4db5-acf7-30369ec013c5" />

<img width="1918" height="872" alt="Screenshot 2026-08-18 094420" src="https://github.com/user-attachments/assets/9edbc58e-d197-4247-8b21-01f8dafb470b" />
<img width="1919" height="876" alt="Screenshot 2026-08-18 094431" src="https://github.com/user-attachments/assets/3844094c-5c14-4460-95c7-2c0835a5204a" />
<img width="1919" height="885" alt="Screenshot 2026-08-18 094742" src="https://github.com/user-attachments/assets/40ef9895-916b-4de4-9e31-51b2a6e9aaca" />
<img width="1919" height="879" alt="Screenshot 2026-08-18 094819" src="https://github.com/user-attachments/assets/1957c333-aa46-420f-95d7-46e460fa850f" />
<img width="1919" height="877" alt="Screenshot 2026-08-18 094924" src="https://github.com/user-attachments/assets/e5781fee-8b8b-418c-8250-d38ede62e583" />
<img width="1919" height="871" alt="Screenshot 2026-08-18 095031" src="https://github.com/user-attachments/assets/97ce9833-47c3-440d-8333-a79077b9c3f0" />

<img width="1919" height="941" alt="Screenshot 2026-08-18 100340" src="https://github.com/user-attachments/assets/1f838910-9f1b-42bc-801b-311d70da1fd9" />
<img width="1919" height="872" alt="Screenshot 2026-08-18 100436" src="https://github.com/user-attachments/assets/38b29755-616e-41e4-9994-6a387eb8a92e" />

<img width="1919" height="867" alt="Screenshot 2026-08-18 100419" src="https://github.com/user-attachments/assets/8e37bb9d-e29b-44da-ad97-f5928f55081f" />

<img width="1919" height="891" alt="Screenshot 2026-08-18 101551" src="https://github.com/user-attachments/assets/a202d579-49a6-454d-adc7-fc71dc5478cc" />

<img width="1919" height="892" alt="image" src="https://github.com/user-attachments/assets/7d3af913-10ad-41ef-8f11-6a3047df2954" />
<img width="1919" height="873" alt="Screenshot 2026-08-18 102645" src="https://github.com/user-attachments/assets/006f40e6-34e3-4473-a353-23219df1bbdb" />


<img width="1916" height="889" alt="image" src="https://github.com/user-attachments/assets/fbc320f5-2a01-4271-a6ed-e81ca0d26ecf" />


## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
