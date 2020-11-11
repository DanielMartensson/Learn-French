# Learn French

This is a web application for lazy users that want to have a custom made memorize training tool.
Here you can insert all your sentences and French sentences and try to memorize them by using the train tab.

You don't need to modify anything if you want to use another language instead of French.

Translate French to your language 

![a](https://raw.githubusercontent.com/DanielMartensson/Learn-French/main/Pictures/Check%201.png)

It will correct you if you enter wrong sentence

![a](https://raw.githubusercontent.com/DanielMartensson/Learn-French/main/Pictures/Check%202.png)

You can also do the reverse way

![a](https://raw.githubusercontent.com/DanielMartensson/Learn-French/main/Pictures/Check%203.png)

And upload own sentencens in other languages. Please create a csv file with the format frenchSentence,yourSentence,yourLanguage e.g

```
Oui,Yes,English
Oui,Ja,Svenska
Bonjour,Goddag,Svenska
Au revoir,Good bye,English
Au revoir,Adjö,Svenska
```

![a](https://raw.githubusercontent.com/DanielMartensson/Learn-French/main/Pictures/Upload.png)

Here you can modify your database with the sentences

![a](https://raw.githubusercontent.com/DanielMartensson/Learn-French/main/Pictures/Database.png)


# How to install - Ubuntu user

1. Install Java 11, Maven, NodeJS

Java 11
```
sudo apt-get install openjdk-11-jdk
```

Maven
```
sudo apt-get install maven
```

NodeJS - This is used if you want to work on this project. If you only want to run this project, you don't need NodeJS.
```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
```

2. Begin first to install MySQL Community Server

```
sudo apt-get install mysql-server
```

3. Then create a user e.g `myUser` with the password e.g `myPassword`

Login and enter your `sudo` password or mysql `root` password
```
sudo mysql -u root -p
```

Create user with the host `%` <-- That's important if you want to access your server from other computers.
```
CREATE USER 'myUser'@'%' IDENTIFIED BY 'myPassword';
```

Set the privileges to that user
```
GRANT ALL PRIVILEGES ON *.* TO 'myUser'@'%';
```

4. Change your MySQL server so you listening to your LAN address

Open this file
```
/etc/mysql/mysql.conf.d/mysqld.conf
```

And change this
```
bind-address            = 127.0.0.1
```

To your LAN address where the server is installed on e.g
```
bind-address            = 192.168.1.34
```

Then restart your MySQL server
```
sudo /etc/init.d/mysql restart
```

If you don't know your LAN address, you can type in this command in linux `ifconfig` in the terminal

6. Download `Learn-French`

Download the `Learn-French` and change the `application.properties` in the `/src/main/resources` folder.
Here you can set the configuration for your database LAN address, user and password.

```
server.port=8080
# Ensure application is run in Vaadin 14/npm mode
vaadin.compatibilityMode = false
logging.level.org.atmosphere = warn

# Database
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.datasource.url=jdbc:mysql://YOUR_MYSQL_SERVER_ADDRESS:3306/LearnFrench?createDatabaseIfNotExist=true&serverTimezone=CET
spring.datasource.username=myUserSQL
spring.datasource.password=myPasswordSQL
```

7. Pack this project and run

First stand inside of the folder `Learn-French` and write inside your terminal
```
mvn package -Pproduction
```

Now a package named `learn-french-1.0-SNAPSHOT.jar` was created. Run it by this command

```
sudo java -jar learn-french-1.0-SNAPSHOT.jar
```

Now you can access this web application at your web browser with the URL link e.g `http://192.168.1.34:8080`
