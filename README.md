# DOCARIZED STATIC WEBSITE ON NGINX RUNNING ON LOCALHOST:



## Step1: Prepare the app files on your local machine

- Create Dockerfile

```yaml
# Use the official Nginx image from Docker Hub
FROM nginx:latest

# Copy your HTML file to the Nginx HTML directory
COPY . /usr/share/nginx/html

```

- Create index.html

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker Nginx</title>
</head>
<body>
  <h2>  SINEM OZTURK SUMUS </h2>
  
  <!-- Gift Section -->
  <div id="gift-section">
    <h3>Heyyoo</h3>
    <p>This is a special gift for you!</p>
    <img src="MY-FRIENDS.gif" alt="Gift Image" width="300">
    <p>You did it!</p>
  </div>
</body>
</html>

```
- Use tje picture of your choise and make sure it is in the same app folder 

![](MY-FRIENDS.gif)

## Step2: SSH into Ubuntu server via CLI of your computer (I have windows so: Powersell)


```powersell
ssh ubuntu@hostname
```
## Step3: Copy source code to Ubuntu 

```powersell
scp "FILE PATH OF YOUR APP" ubuntu-name@hostname: <<path to your app file in the nginx server>>
```

## Step4: Build Docker Image with CLI


```sh
docker build -t give-a-name-to-your-image . 
```

- This command builds the Docker image using the `Dockerfile` in your current directory and tags it as you want. I will call it `my-app`


## Step6: Run the Docker Container 

```sh
docker run -d -p 8080:80 --name give-a-name-to-your-container my-app
```

- Give a name for your container and use image that we created in step4 and called as my-app
- This command runs the Docker container in `detached mode (-d)`
- This option `-p 8080:80 `maps a port on your host machine to a port inside the container.
- `8080:80` means that port 8080 on your host machine will be forwarded to port 80 inside the container.
- This allows you to access the container's services (such as a web server running on port 80) through port 8080 on your host machine.
- This option -> `--name give..` assigns a name to the container. Instead of `give-a-name-to-your-container`, you should provide a meaningful name for your container.
- This (`my-app `) is the name of the Docker image you want to use to create the container.
- Ensure that `my-app` is an existing image that you have built or pulled from a Docker registry.


## Step7: Access the Web via Localhost with exposed port

```txt
http://localhost:8080/

```


### Breakdown of http://localhost:8080/
- `http://`

This specifies the protocol used for the connection. In this case, it is HTTP (Hypertext Transfer Protocol), which is the foundation of data communication on the web.

- `localhost:`

This is a hostname that refers to the current machine. It is a loopback address that points to the computer you're currently using.
In networking terms, localhost translates to the IP address 127.0.0.1 (IPv4) or ::1 (IPv6).

- `:8080`:

This specifies the port number on the host machine to which the browser should connect.
The port number 8080 is often used as an alternative to the default HTTP port 80, especially when running web services in development or when port 80 is already in use by another service.

- `/`:

This indicates the root path of the server. When you access the root path, you are typically requesting the default page or index of the website or application served by the web server.