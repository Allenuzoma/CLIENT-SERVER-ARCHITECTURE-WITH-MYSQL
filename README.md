# CLIENT-SERVER-ARCHITECTURE-WITH-MYSQL



Client-server architecture is a widely used system design where the client sends requests to the server, which processes those requests and returns the results. In the context of MySQL, this architecture enables the separation of concerns between the client (frontend or application) and the server (where MySQL runs to manage and store data).

Client: The client, which can be a web or desktop application, initiates a connection to the MySQL server. It sends SQL queries to retrieve, update, or manipulate data stored in the MySQL database.

Server: The server hosts the MySQL database. It listens for client connections over the network (typically on port 3306) and processes SQL queries sent by the client. It then returns the requested data or performs the specified operations (such as inserting or deleting data).

Communication: The client communicates with the server using MySQL's communication protocols over TCP/IP. The server processes each request, interacts with the database, and sends back the response, which the client then uses to display data or take further action.


**Steps: Implementing the Client-Server architecture with Mysql on AWS**
1. Create two ubuntu ec2 virtual servers on AWS named: mysql-server & mysql-client

   
   ![2 instances](https://github.com/user-attachments/assets/621ad5d3-b835-4269-8205-b3b3b8e3bab0)


2. Note the details of mysql-server

 
  
   ![instance 1 details](https://github.com/user-attachments/assets/d62c7d3d-1d3f-4e64-ae49-ac780c34cd64)


3. Note the details of mysql-client


   ![instance 2 details](https://github.com/user-attachments/assets/4b3aaa4b-21aa-4b9b-8d86-35b259e591b8)


4. Configure the security group of the 'mysql-server' as shown below:

   ![sg server](https://github.com/user-attachments/assets/7e4c2c3a-a089-4d94-a405-cbc394c278f1)

5. Configure the security group of the 'mysql-client' as shown below:
   
   ![sg client](https://github.com/user-attachments/assets/323662f9-368e-435c-8e39-87886578f806)

6. On the mysql-server install the Mysql-server software as shown below:

            #To update the repository


            sudo apt update


            #To install mysql-server software

   
            sudo apt install -y mysql-server
         
            #To see status of the installed mysql-server

   
            sudo systemctl status mysql
         
            #To enable mysql-server

   
            sudo systemctl enable mysql
         
            #To restart mysql-server

   
            sudo systemctl restart mysql
   
         
            #To enter the mysql console

   
            sudo mysql

   ![mysql server running systemctl](https://github.com/user-attachments/assets/ddb18553-aa44-4a74-9efe-bd19c2b3f86e)


6. You might need to configure MySQL server to allow connections from remote hosts. On the mysql-server, enter the command:


         sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf


7. Replace the Bind address 127.0.0.1 with 0.0.0.0 as shown below:


   ![changing bind address on server](https://github.com/user-attachments/assets/000e572d-f13d-4cc0-b83a-a6f86a62293c)

9. Enter mysql console by entering the command:

       sudo mysql

10. Now that we are in the console we would change the root user password using the command below:

       ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password123$';
![mysql alter user](https://github.com/user-attachments/assets/bf514030-4e35-4db3-815a-bab14a42571c)

11. Exit the console by entering:


          exit


12. Re-enter the mysql-server console as root user by using the command:

        sudo mysql -u root -p

13. We have to create a new user and grant all privileges to it. This user is the 
    mysql-client running in the second vm. Enter the command to do this:

          #Create remote_user
          CREATE USER 'remote_user'@'%' IDENTIFIED BY 'Password123$';
          
          #Grant all privileges
          GRANT ALL PRIVILEGES ON '*' TO 'remote_user'@'%' WITH GRANT OPTION;
      
          FLUSH PRIVILEGES;
   
      
 14. Exit the console.   
   

 15. On the mysql-client Instance Connect terminal, connect to the mysql-server 
     remotely by using the command:


           mysql -h <mysql-server-Public IP> -u <username> -p


     In this project we will use:

           mysql -h 3.82.5.9 -u remote_user -p


16. When prompted for password, enter 'Password123$'

17. Run the following command to test remote_user access to the mysql-server 
    database:

          SHOW databases;


    ![accessing server from client](https://github.com/user-attachments/assets/f8696908-c453-41a6-a942-418cef6d217c)




    We can connect to the database as shown above, this implies that the client-      server architecture has been created successfully.

        


    

    


      

