FROM python:3.10-slim-buster

# Container
# "Make a new folder inside the container called..."
WORKDIR /backend-flask

# Outside -> Inside
# Copy this file outside the container and put it IN the container
# This contains the libraries we want installed to run the app
COPY requirements.txt requirements.txt

# Inside Container
# Will actually install the python libraries used for the app
RUN pip3 install -r requirements.txt

# Outside Container -> Inside Container
# . means everything in the current directory
# first period . = /backend-flask (outside cointainer)
# second period . = /backend-flask (inside container)
COPY . .

# Set Environment Variables (Env Vars)
# Inside Container and will remain set when container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}

# CMD (Command)
# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]

