### Steps
1. Create Node JS App
2. Create Dockerfile
3. Build Image from Dockerfile
4. Run image as container
5. Connect to web app from a browser

### Node JS Aps
* Have to install dependencies before running the app.
* Install deps by running "npm install"
* Assumes npm is installed

* Have to run command to start up the server
* Star teh server by running npm start
* Assumes npm is installed.

### You can always find an image

You can review [The docker Hub](https://hub.docker.com)

### Notes
* the container has its own isolated ports.
```shell
docker build -t username/image_name .
```
* If we change one file we should not rebuild everything (install all dependencies)

### Port Mapping
* Every time someone makes a request on your local network, mapped to the port in the container.
* Only talking about incoming requests.
* We set port forwarding as runtime constraint.

```shell
docker run -p 8080 : 8080 <imageid>
```

