# Introduction 
This repository contains HTML files and a nginx config file needed to test  ansible.eda.webhook
source plugin by inserting data from a web page. Typically you would do this with a curl command and post a JSON payload.

The web page (webhook_test.html) allows you to send data to 2 different
webhooks listening on port 4444 and port 5555 directly from a Web browser.

The nginx conf file has these lines

```
        location /webhook1/ {
                proxy_pass http://localhost:4444/payload;
        }   

        location /webhook2/ {
                proxy_pass http://localhost:5555/payload;
        }
```

In this demo the nginx server is listening on port 9999

When the data is sent to http://localhost:9999/webhook2/payload/
it gets forwarded to the port 5555 where the ansible.eda.webhook source plugin
is listening.


# Steps to install

* Install ngnix locally on your machine
* Use the config file from the nginx_config directory or customize
  your nginx.conf to support the /webhook1 and /webhook2 location
* The data files are stored in nginx_data directory and it includes
   * webhook_test.html
   * dataflow.png

To locate where your nginx config file is you can use the following
command

```
nginx -t
```

The data directory that serves the files is defined in the nginx.conf

```
location / { 
            root   /users/fred/nginx_data;
            index  index.html index.htm;
        } 
```

In the above case you want to copy the files from ngninx_data to
/users/fred/nginx_data


To check if the setup is working after you have started nginx 
* Open Web browser
* Navigate to http://localhost:9999/webhook_test.html

