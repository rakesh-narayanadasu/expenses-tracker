# Frontend

The frontend is the service in Expense to serve the web content over Nginx. This will have the web frame for the web application.

This is a static content and to serve static content we need a web server. This server

Developer has chosen Nginx as a web server and thus we will install Nginx Web Server.

Install Nginx
```
dnf install nginx -y 
```
Enable nginx
```
systemctl enable nginx
```
Start nginx
```
systemctl start nginx
```

**Try to access the service once over the browser and ensure you get some default content**

Remove the default content that web server is serving.
```
rm -rf /usr/share/nginx/html/*
```
Clone the frontend code
```
git clone https://github.com/rakesh-narayanadasu/expenses-tracker.git
```
```
cd expenses-tracker/expense-frontend-v2
```
Copy the frontend code
```
cp -r $HOME/expenses-tracker/expense-frontend-v2/* /usr/share/nginx/html
```

**Try to access the nginx service once more over the browser and ensure you get expense content.**

Create Nginx Reverse Proxy Configuration.
```
vim /etc/nginx/default.d/expense.conf
```
Add the following content
```
proxy_http_version 1.1;

location /api/ { proxy_pass http://localhost:8080/; }

location /health {
  stub_status on;
  access_log off;
}
```

**Ensure you replace the localhost with the actual ip address of backend component server. Word localhost is just used to avoid the failures on the Nginx Server.**

Restart Nginx Service to load the changes of the configuration.

```
systemctl restart nginx
```
