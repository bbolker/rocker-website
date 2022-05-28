---
title: "Networking: tips and tricks"
---

###  <i class="material-icons">https</i> HTTPS 

Any RStudio instance on a remote server is accessed over an unencrypted http by default (though RStudio encrypts the password entered to log in through client-side javascript.)  The easiest way to connect over a secure https connection is to use a reverse proxy server, such as [Caddy](https://caddyserver.com).  To establish an encrypted https connection, you must first have control of a registered domain name: https cannot be used when connecting directly to a given ip address. Once you have pointed your domain name at the ip address of the server, Caddy provides a quick way to get set up with https using LetsEncrypt certificates.  Below is an example `Caddyfile` specifying the necessary configuration, along with a `docker-compose` file which sets up an RStudio server instance behind a separate container running `caddy`.  This approach also makes it easy to map ports to subdomains for cleaner-looking URLs:

Example `site/Caddyfile`:

```
rstudio.example.com {
  
  tls you@email.com
  proxy / rstudio:8787 {
    header_upstream Host {host}
  }

}

```

Example docker-compose file:

```yml
version: '2'
services:
  caddy:  
    image: joshix/caddy
    links:
      - rstudio
    volumes:
      - ./site/:/var/www/html
      - ./.caddy/:/.caddy
    ports:
      - 80:80
      - 443:443
    restart: always

  rstudio:
    image: rocker/verse 
    env_file: .password 
    volumes:
      - $HOME/students:/home/
    restart: always
```


More details about the use of [docker-compose](https://docs.docker.com/compose/) and [Caddy Server](https://caddyserver.com/) are found on their websites.



### <i class="material-icons">data_usage</i> Monitoring 



### <i class="fa fa-database"></i> Linking database containers
