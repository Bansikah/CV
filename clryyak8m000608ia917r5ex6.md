---
title: "Creating a Docker Image for a Simple python-flask "hello world!" application."
datePublished: Mon Jan 29 2024 13:13:38 GMT+0000 (Coordinated Universal Time)
cuid: clryyak8m000608ia917r5ex6
slug: creating-a-docker-image-for-a-simple-python-flask-hello-world-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706533868712/43994669-72df-461c-a9a7-a60c1d16f57e.png
tags: docker, developer, devops, docker-images

---

**Building a Docker Image for a Simple Hello World Flask Application**

**Introduction to Docker**

Docker is a platform for developing, shipping, and running applications. It enables developers to package their code and dependencies into a standardized unit called a container. Containers are lightweight and portable, making them ideal for deploying applications across different environments.

**What is an Image?**

An image is a static representation of a container. It contains all the necessary code and dependencies required to run an application. Images can be created from scratch or by extending existing images.

**Building a Hello World Flask Application Image**

To build a Hello World Flask application image, follow these steps:

1. **Create a Dockerfile**:
    

A Dockerfile is a text file that contains instructions for building a Docker image. For a simple Hello World Flask application, the Dockerfile might look like this:

```bash
FROM python:3.8-slim-burster

WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

1. **Create the Python Flask Application Code**:
    

Create a file named [`app.py`](http://app.py) with the following code:

```bash
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello, World!"

if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

1. **Build the Image**:
    

To build the image, run the following command:

```bash
docker build -t hello-world-flask .
```

Expected results:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/55fitehp92nwxegq93yl.png align="left")

4\. **Run the Image**:

To run the image, run the following command:

```bash
docker run -p 5000:5000 hello-world-flask
```

This will start a container based on the Hello World Flask application image and expose port 5000 of the container to port 5000 of the host machine.

1. **Access the Application**:
    

To access the application, open a web browser and navigate to [`http://localhost:5000`](http://localhost:5000) . You should see the Hello World message.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sdarhdui2ghcr9qnm1uw.png align="left")

So, that's the end of this project, in case of any questions or errors, please write in the comments and i will resolve them.