# WordPress-Docker-compose-deploy

### Deploying the popular WordPress blogging platform with MySQL database using docker compose

```
###### What is WordPress?
```
WordPress is a free and open source blogging tool and a content management system (CMS) based on PHP   
and MySQL, which runs on a web hosting service. Features include a plugin architecture and a template   
system. WordPress is used by more than 22.0% of the top 10 million websites as of August 2013. WordPress   
is the most popular blogging system in use on the Web, at more than 60 million websites. The most popular   
languages used are English, Spanish and Bahasa Indonesia.

(Visit Wordpress Wiki)[wikipedia.org/wiki/WordPress]

###### Important imformation about this image  

```
  -e WORDPRESS_DB_HOST=... (defaults to the IP and port of the linked mysql container)
  -e WORDPRESS_DB_USER=... (defaults to “root”)
  -e WORDPRESS_DB_PASSWORD=... (defaults to the value of the MYSQL_ROOT_PASSWORD environment variable   
    from the linked mysql container)
  -e WORDPRESS_DB_NAME=... (defaults to “wordpress”)  
  -e WORDPRESS_TABLE_PREFIX=... (defaults to “”, only set this when you need to override the default   
    table prefix in wp-config.php)
  -e WORDPRESS_AUTH_KEY=..., -e WORDPRESS_SECURE_AUTH_KEY=..., -e WORDPRESS_LOGGED_IN_KEY=...,   
  -e WORDPRESS_NONCE_KEY=..., -e WORDPRESS_AUTH_SALT=..., -e WORDPRESS_SECURE_AUTH_SALT=...,   
  -e WORDPRESS_LOGGED_IN_SALT=..., -e WORDPRESS_NONCE_SALT=... (default to unique random SHA1s)  
```

If the WORDPRESS_DB_NAME specified does not already exist on the given MySQL server, it will be created   
automatically upon startup of the wordpress container, provided that the WORDPRESS_DB_USER specified has   
the necessary permissions to create it.

###### Deploying using docker-compose  

> By default docker-compose files are named docker-compose.yaml or docker-compose.yml so that docker-compose up identifies the file and does the work

```
    docker-compose up
```

> If you name the yaml file than docker-compose.yaml or docker-compose.yml you need to specify -f flag with the name of the file along with up. Let us consider the file name to be stack.yml

```
    docker-compose -f stack.yml up
```

> Docker official documentation provides an example template file with to launch wordpress using docker-compose. There is a major issue that people were facing while using that code is it is missing the port binding for mysql image on which wordpress depends. It results following errors.

```stacktrace
             | MySQL Connection Error: (2002) Connection refused
wordpress_1  | 
wordpress_1  | Warning: mysqli::mysqli(): (HY000/2002): Connection refused in - on line 22
wordpress_1  | 
wordpress_1  | Warning: mysqli::mysqli(): (HY000/2002): Connection refused in - on line 22
wordpress_1  | 
wordpress_1  | MySQL Connection Error: (2002) Connection refused

```

> In order to overcome this issue provide a port binding to the mysql service as follows

```yaml
  ports:
    - "3306:3306"
```



