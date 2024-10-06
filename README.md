# CLIENT-SERVER-ARCHITECTURE-WITH-MYSQL


**Step 0: Installing the prerequisites**
1. Create two ubuntu ec2 virtual servers on AWS named: mysql-server & mysql-client

   
   ![2 instances](https://github.com/user-attachments/assets/621ad5d3-b835-4269-8205-b3b3b8e3bab0)


2. Note the details of mysql-server

  ![instance 1 details](https://github.com/user-attachments/assets/41d038d8-7c00-47f9-a95a-0833785e50f7)


3. Note the details of mysql-server


![instance 2 details](https://github.com/user-attachments/assets/3ba8b067-50ee-422b-bcac-f4f97778ced6)


4. Configure the security group of the mysql-server as shown below:

   ![sg server](https://github.com/user-attachments/assets/7e4c2c3a-a089-4d94-a405-cbc394c278f1)

5. Configure the security group of the mysql-client as shown below:
   
   ![sg client](https://github.com/user-attachments/assets/323662f9-368e-435c-8e39-87886578f806)

You might need to configure MySQL server to allow connections from remote hosts.

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Replace the Bind address 127.0.0.1 with 0.0.0.0
