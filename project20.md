# DOCUMENTATION OF PROJECT 20

1. I launched an ubuntu OS Linux server and updated it
   
   ![Projec20](images/image30.PNG)
   ![Projec20](images/image31.PNG)

2. I installed the necessary dependencies
   
   ![Projec20](images/image32.PNG)
   ![Projec20](images/image33.PNG)

3. Then I installed docker
   
   ![Projec20](images/image34.PNG)
   ![Projec20](images/image35.PNG)

4. I pulled MYSQL image from docker hub registry

    `docker pull mysql/mysql-server:latest`

    ![Projec20](images/image36.PNG)

5. I deployed the MYSQL container to my docker engine and I confirmed if it is running

`docker run --name <container_name> -e MYSQL_ROOT_PASSWORD=<my-secret-pw> -d mysql/mysql-server:latest`
     `docker ps -a`

![Projec20](images/image37.PNG)


6. I created a docker network named "tooling_app_network" then I confirmed if it has been created


    `sudo docker network create --subnet=172.18.0.0/24 tooling_app_network && sudo docker network ls`

    ![Projec20](images/image38.PNG)


7. I exported my password then I pulled the image and run the container

     `export MYSQL_PW=  && docker run --network tooling_app_network -h mysqlserverhost --name=mysql-server -e MYSQL_ROOT_PASSWORD=$MYSQL_PW  -d mysql/mysql-server:latest `


    ![Projec20](images/image39.PNG) 


8. I craeted a file named "create_user.sql" and I updated it with the necessary command

    

    `sudo touch create_user.sql  && sudo vi create_user.sql`

    ![Projec20](images/image40.PNG)

9. Then I ran the script and it worked. 
     `docker exec -i mysql-server mysql -uroot -p$MYSQL_PW < create_user.sql `


     ![Projec20](images/image41.PNG)

10. I ran the MYSQL client container

      `docker run --network tooling_app_network --name mysql-client -it --rm mysql mysql -h mysqlserverhost -u  -p`


      ![Projec20](images/image42.PNG)
      ![Projec20](images/image43.PNG)


11. I cloned the toolong-app repository

    ![Projec20](images/image44.PNG)

12. Then I exported the tooling-database file
    
    ![Projec20](images/image45.PNG)

13. I used the 'SQL' script to create a database

     `docker exec -i mysql-server mysql -uroot -p$MYSQL_PW < $tooling_db_schema`

     ![Projec20](images/image46.PNG)


14. Then I edited the '.env' file 

    ![Projec20](images/image47.PNG)

15. I built the app and I ran the container


   `docker build -t tooling:0.0.1 . `

   `docker run --network tooling_app_network -p 8085:80 -it tooling:0.0.1 `

  ![Projec20](images/image48.PNG) 

  ![Projec20](images/image49.PNG)


16. I opened the link on my browser and it connected successfully

   
   ![Projec20](images/image50.PNG)