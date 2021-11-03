Here we prepare the data to build the MySQL container, proceed to extract the my.cnf file contained in mysql:latest:

docker run -it --rm -v /mycode/:/home/  mysql:latest cp /etc/mysql/my.cnf /home/my.cnf
After this command, copy the file my.cnf to the directory /mycode/db/my.cnf (remember this directory will later be used to map data to the container), open this file and add the content:

[mysqld]
default-authentication-plugin=mysql_native_password