Vibe.d setup
==========

##Goal of this guide


This is a guide on how to quickly install dub and vibe.d on Ubuntu!

##What is DUB?

  Dub is very usefull build tool for D projects with support for automatically retrieving dependencies and integrating them in the build process. 
  
##Install DUB on systems like Debian, Ubuntu, LinuxMint, etc

  The easiest way is through 'd-apt' repository.
  
  ```Linux
  sudo wget http://master.dl.sourceforge.net/project/d-apt/files/d-apt.list -O /etc/apt/sources.list.d/d-apt.list
  sudo apt-get update && sudo apt-get -y --allow-unauthenticated install --reinstall d-apt-keyring && sudo apt-get update
  ```
  
  Now you are ready ti install DMD and DUB. Full list of packages available in the repository can be found at http://d-apt.sourceforge.net/
  
  Install DMD
  ```Linux
  sudo apt-get install dmd-bin
  ```
  Install DUB
  ```Linux
  sudo apt-get install dub
  ```

##Additional setup on Linux (Debian/Ubuntu/Mint)
  
  ```Linux
  sudo apt-get install libevent-dev libssl-dev
  ```
  
  You also need g++
  
  ```Linux
  sudo apt-get install g++ gcc-multilib xdg-utils
  ```
  
##Start new vibe.d project
  
Then you can easily starting a new vibe.d project.
  
  ```Linux
  dub init <name> vibe.d
  cd <name>
  dub
  ```

##Additional resources

The official vibe.d repository - https://github.com/rejectedsoftware/vibe.d

#Setup NGINX as web proxy

  For security reasons it is good to setup NGINX as a web proxy for your vibe.d server. Here is how you can configure NGINX to proxy the http requests to vibe.d and also make NGINX serve the static resources like images, css and js files. The config file for NGINX is in /etc/nginx/sites-available or in /etc/nginx/conf.d
  
    server {
      listen 80;
      server_name dev.mysite.com;

      location / {
        #if your vibe.d is listening on port 8080
        proxy_pass http://localhost:8080/;
        proxy_redirect off;
      }
      
      # http://site/public/js/file.js will reffer to /vibedproject/public/js/file.js
      location ~ ^/public/((images/|css/|js/).*)$ {
        alias /path/to/project/[public]/$1;
        access_log off;
        expires max;
      }
    }

  
  
