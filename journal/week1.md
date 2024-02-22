# Week 1 — App Containerization

The theme of the class this week was containerization and Docker files

Some of the main purposes of Containers:
1. Portability: The ability to package applications with everything needed, including dependencies, runtime, and libraries.
2. Isolation: Allowing applications to run independently.
3. Scalability: It's possible to scale based on changing workloads.
4. Efficient optimization within DevOps and CI/CD: Makes it easier to implement DevOps practices.

Create Dockerfile for Crudder [Backend]

- Docker Hub
    - A container registry provided by Docker
    - You can host your own container images (private and public)
- Open Container Initiative
    - The standard for building containers

### Create Dockerfile for Crudder [Backend]

'FROM python:3.10-slim-buster

WORKDIR /backend-flask

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]'

Each line contains instructions on how to run your application.

If you run it in your localhost with your requirement txt, you need every instruction in this recipe.

`FROM python:3.10-slim-buster` is a supported docker file.'

- `3.10-slim-buster`: It loads another docker file.
- Each command in a docker file will essentially create a layer.
- So creating a docker file is essentially creating layers.
- Containers use a Union File System.
    - Merges all the layers into one layer.
    - Example: One layer creates a file on a lower layer and a higher layer deletes that file.
    - Within the merged layer, you wouldn't see this file.
    - Everything builds on top and your view is looking downward.

`WORKDIR /backend-flask` = signals where this is going to work from when the container starts.

`COPY requirements.txt requirements.txt` =  takes something from OUTSIDE the Container and copies INSIDE the container.

`RUN pip3 install -r requirements.txt` =  is an action INSIDE the container. It runs `pip3 install` from the root (-r) file `requirements.txt`.

`COPY . .` =  copies everything in the current directory (/backend-flask) to the container directory (also called /backend-flask).

`ENV FLASK_ENV=development` = sets the environment Variables (Env Vars). It sits inside the container and remains set when the container is running.

`CMD ["python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]` = is the CMD Command.

    - In the context of Flask,  python3 -m flask run` is considered a shortcut because you don't need to explicitly write a script to execute your Flask application.

    - It's a concise way to run a Flask app without having a separate entry point script.

    - `-host=0.0.0.0` binds the Flask application to all network interfaces, making it accessible from any IP address.
    
    - `--port=4567` sets the Flask development server to listen on port 4567.

### Build Dockerfile

- `docker build -t backend-flask ./backend-flask` is the command to build the image.
    - `docker build` builds the image.
    - `-t` is used to tag the image with a name. In this case, "backend-flask".
    - `./backend-flask` is the path to the build context, where the Dockerfile and any associated files are located.

- `docker ps` lists only the running containers, while `docker ps -a` lists all containers, including those that are stopped. The `-a` flag stands for "all".

### NPM Install

- `npm i` is a shorthand for `npm install`. It's a command used in Node.js projects to install dependencies listed in the `package.json` file.

### Create Dockerfile for Crudder [Frontend]

```dockerfile
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install

Connected the Notifications backend and Front End

- As it mirrored much of the same behavior as the Home page, we copied much of the code and made minor adjustments so that it fit for notifications

EXPOSE ${PORT}
