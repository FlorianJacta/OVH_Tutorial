# Taipy to create your Web apps in Python

[Taipy](https://www.taipy.io/) is an **Open-Source** user-friendly Python package tool that provides an easy and intuitive way for users to create graphical user interfaces. With Taipy, you don't need advanced knowledge of web design to create beautiful and interactive interfaces. Taipy uses a simple augmented Markdown syntax to help you create web pages with custom features and functionality.

In addition to its GUI capabilities, Taipy provides a powerful pipeline orchestration package called **Taipy Core**. Taipy Gui & Core make it possible to handle the front end and back end of a complete application within the same tool. It simplifies creating and managing **complex data pipelines** by providing intuitive DAG modeling, intelligent scheduling, robust data caching, and scenario-enabled pipelines. This makes Python development more accessible and efficient for users of all levels of expertise.

Overall, Taipy is a complete solution for businesses and individuals who want to streamline their Python development process and create professional-looking interfaces without needing advanced web design skills.

For the following steps, you can clone this [repository](https://github.com/FlorianJacta/OVH_Tutorial) to deploy your first Taipy app on OVH.

# Deploying a Taipy app on OVH

To deploy your Taipy app, you only need Docker Hub and AI Deploy from OVH. This process will allow you to make your app accessible within minutes. With Docker Hub, you can store and manage your app's docker, while OVH provides a secure and reliable hosting environment.

In this article, we'll take you through deploying a Taipy app on OVH using Docker Hub.

## Step 1: Configure your app

When building a Docker for your Taipy app, you must provide a _Dockerfile_ and a _requirements.txt_ file. Here are the steps to include these files in your project:

1. Create a Dockerfile

The _Dockerfile_ is a text file that describes the steps required to build a Docker image for your app. You can create a new file in your project directory and name it "Dockerfile".
 
 ```
# Start from the official Python image
FROM python:3.9


# Create a working directory
WORKDIR /workspace


# Install a few requirements, such as pandas, taipy, scikit-learn, ...
ADD requirements.txt /workspace/requirements.txt


RUN pip install -r requirements.txt


# Add your scripts to the Docker image. Note: best practice is to put data outside, such as S3 storage
ADD main.py /workspace/
ADD dataset.csv /workspace/


# Create a HOME dedicated to the OVHcloud user (42420:42420). mandatory step
RUN chown -R 42420:42420 /workspace
ENV HOME=/workspace


# Run your script
CMD [ "python3" , "/workspace/main.py" ]
```

2. Create a requirements.txt file:
The _requirements.txt_ file lists all the dependencies your Taipy app requires. You can create a new file in your project directory and name it "requirements.txt". You can then list all the dependencies, one per line. For example:

```
taipy==2.2
yfinance==0.1.96
prophet==1.1.2
```

With these steps, you should have a _Dockerfile_ and a _requirements.txt_ file in your Taipy app project. Using Docker Hub, you can then use these files to build a Docker for your app and deploy it to OVH.

## Step 2: Create a Docker Hub account

If you still need a Docker Hub account, head to https://hub.docker.com/ and create one. Once you have made your account, you can store and manage your app's containers.

## Step 3: Build your Taipy app's Docker image

To deploy your Taipy app on OVH, you must build a Docker image for your app. It will include all the necessary dependencies and configurations for your app.

Assuming you have your Dockerfile ready, you can build your image using the following command:

```
docker build -t <your-image-name> .
```

Replace `<your-image-name>` with the name you want to give to your Docker image.
 
## Step 4: Push the Docker image to Docker Hub

Once you have built your Docker, the next step is to push it to Docker Hub. To do this, you need to tag your image with your Docker Hub account name and push it using the following commands:

```
docker tag <your-image-name> <your-dockerhub-username>/<your-image-name>
docker push <your-dockerhub-username>/<your-image-name>
```

Replace `<your-dockerhub-username>` with your Docker Hub account name and `<your-image-name>` with the name you gave to your Docker image.

## Step 5: Deploy your app using AI Deploy

The next step is to create an account on OVH Cloud if not done yet. AI Deploy will be used to host your app. You can find this service going to Public Cloud. Then, click on "Deploy an app". You will have to choose:
- Location
- Application to deploy: put the path to the Docker Hub image
- Resources
- Attach a container
- Configure your app
- Review

At the end of this step, OVH will use your Docker Hub image to create and deploy the app.

## Step 6: Test your app

Test your app on OVH by accessing its URL.

## To conclude

Taipy is an open-source Python package tool that simplifies the creation of graphical user interfaces without requiring advanced web design skills. It also provides a pipeline orchestration package, Taipy Core, that simplifies creating and managing complex data pipelines. By following a few steps, users can deploy their Taipy apps on OVH using Docker Hub and AI Deploy. Overall, Taipy is an ideal solution for businesses and individuals looking to streamline their Python development process and create professional-looking interfaces.
