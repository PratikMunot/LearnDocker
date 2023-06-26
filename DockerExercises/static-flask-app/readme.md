### Step 1
Lets create our required folder structure and a virtual environment to setup and run flask app.
```
mkdir static-flask-app
cd static-flask-app/
sudo apt install python3-venv
python3 -m venv python-flask-app
source python-flask-app/bin/activate
pip install flask

```

### Step 2
Our virtual environment is now working. Lets create a python file named app.py which contains our source code for static page.
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello Pratik - from Docker - flask"

if __name__ == "__main__":
    app.run(host ='0.0.0.0', port = 5001, debug = True)

```

### Step 3
Next we create Dockerfile which contains instructions to build the image
```
FROM python:3.9-slim-buster
WORKDIR /app
COPY ./requirements.txt /app
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5001
ENTRYPOINT [ "python" ]
CMD [ "app.py" ]

```

### Step 4
Lets try to verify if our flask app is running correctly by executing the command. The flask server must be running on localhost:5001
```
python3 app.py
curl localhost:5001
```

### Step 5
Now we generate the requirements.txt file which contains the list of all the packages and dependencies required to run our flask app
```
pip freeze > requirements.txt
```

### Step 6
We need to correct our folder structure inorder to build the image of our application. Lets create .dockerignore which will contain list of files and folders 
which will be ignored while building the image. Once .dockerignore file is created then paste the virtual environment folder name in the file.
```
python-flask-app
```

### Step 7
Our folder structure is now good. Lets build docker image of our application and then we check if image is working as expected by running the container.
```
docker build -t flask-static-app:1.1 .
docker run docker-flask-app:1.1
```

### Step 8
Lets tag the image as per docker hub convention so that we will be able to push it on docker hub. Finally we run our image once again to check how its executing
```
docker tag docker-flask-app:1.1 pmunot11/docker-flask-app:1.1
docker push pmunot11/docker-flask-app:1.1
docker run -d -p 5001:5001 pmunot11/docker-flask-app:1.1
```











