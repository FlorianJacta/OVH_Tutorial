# Deploying a Taipy app on OVH
Deploying a Taipy app on OVH using Docker Hub and OVH is a great way to ensure your app is accessible and stable. With Docker Hub, you can store and manage your app's containers, while OVH provides a secure and reliable hosting environment.

In this article, we'll take you through deploying a Taipy app on OVH using Docker Hub.
## Step 1: Configure your app

When building a Docker container for your Taipy app, you must provide a Dockerfile and a requirements.txt file. Here are the steps to include these files in your project:
Create a Dockerfile
The Dockerfile is a text file that describes the steps required to build a Docker container for your app. You can create a new file in your project directory and name it "Dockerfile".
 
 ```
# Start from official Python image
FROM python:3.9


# Create a working directory
WORKDIR /workspace


# Install a few requirements, such as pandas, taipy, scikit-learn, ...
ADD requirements.txt /workspace/requirements.txt


RUN pip install -r requirements.txt


# Add your scripts to Docker image. Note : best practice is to put data outside, such as S3 storage
ADD app.py /workspace/
ADD dataset.csv /workspace/


# Create a HOME dedicated to the OVHcloud user (42420:42420). mandatory step
RUN chown -R 42420:42420 /workspace
ENV HOME=/workspace


# Run you script and BOOM :)
CMD [ "python3" , "/workspace/app.py" ]
```

Create a requirements.txt file:
The requirements.txt file lists all the dependencies required by your Taipy app. You can create a new file in your project directory and name it "requirements.txt". You can then list all the dependencies, one per line. For example:

```
taipy
scikit-learn
statsmodels
pandas
```

With these steps, you should now have a Dockerfile and a requirements.txt file in your Taipy app project. You can then use these files to build a Docker container for your app and deploy it to OVH using Docker Hub and OVH.
## Step 2: Create a Docker Hub account
If you still need a Docker Hub account, head to https://hub.docker.com/ and create one. Once you have made your account, you can store and manage your app's containers.
## Step 3: Build your Taipy app's Docker container
To deploy your Taipy app on OVH, you need to first build a Docker container for your app. This container will include all the necessary dependencies and configurations for your app. To create the container, you need a Dockerfile describing the steps involved in building the container.

Assuming you have your Dockerfile ready, you can build your container using the following command:

```
docker build -t <your-image-name> .
```
Replace <your-image-name> with the name you want to give to your Docker image.
## Step 4: Push the Docker image to Docker Hub
Once you have built your Docker container, the next step is to push it to Docker Hub. To do this, you need to tag your image with your Docker Hub account name and push it using the following commands:
```
docker tag <your-image-name> <your-dockerhub-username>/<your-image-name>
docker push <your-dockerhub-username>/<your-image-name>
```
Replace <your-dockerhub-username> with your Docker Hub account name and <your-image-name> with the name you gave to your Docker image.
## Step 5: Create a new server on OVH
The next step is to create an account on OVH Cloud. AI Deploy will be used to host your app. OVH provides various hosting solutions, including Virtual Private Servers (VPS), dedicated servers, and cloud instances. Choose the one that best suits your needs and create a new server.
## Step 6: Configure your app on your OVH server
Once you have created your server on OVH, the next step is installing Docker. You can do this by running the following command:
## Step 7: Test your app
With your Taipy app deployed on OVH

```
docker build -t my-taipy-app .
```

docker run -p 5000:5000 -d --name my-taipy-app my-taipy-app

docker image tag my-taipy-app:latest florianjacta/my-taipy-app:latest

Push


