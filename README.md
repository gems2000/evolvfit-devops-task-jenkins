
# **EvolvFit DevOps Challenge**
The task was to create ***Jenkins Pipeline*** with a line-by-line explanation. I have created a sample ***Flask*** web app for the development pipeline demonstration in ***Jenkins***. 
## **Prerequisites**

You need to have a functional Python 3 environment to run this project. I recommend [pyenv](https://github.com/pyenv/pyenv) and [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv).

After you can download and install the python modules into a segregated virtualenv.

```bash
# install python and create virtualenv
## NOTE: pcre grep requires GNU grep, e.g. grep -oP
LATEST_PYTHON3=$(
 pyenv install --list | tr -d ' ' | grep -oP '^3\.*\d+\.\d+$' | sort -V | tail -1
)

pyenv install $LATEST_PYTHON3
pyenv virtualenv $LATEST_PYTHON3 evolvfit-devops-task-jenkins
# change to virtualenv
cd .
# update pip module
pip install --upgrade pip
```

## **Running the Application**

These instructions and scripts have been tested on Windows / WSL with Python installed.

### **Test using Python**

```bash
# Install Required Packages
pip install -r requirements.txt
# Run Server
./app.py &
# Manually Test
curl -i localhost:5000/
curl -i localhost:5000/hello/gems2807
```

### **Using Docker Compose**

```bash
# Start containerized service on Docker
docker-compose up -d
# Determine Guest is native Docker, Docker-Machine or Docker-Desktop
[ -z ${DOCKER_MACHINE_NAME} ] || WEBSERVER=$(docker-machine ip ${DOCKER_MACHINE_NAME})
WEBSERVER=${WEBSERVER:-localhost}
# Manually Test
curl -i $WEBSERVER:5000/
curl -i $WEBSERVER:5000/hello/gems2807


## **Running Automated Tests**

```bash
./test.py
```
**Running A Job in Jenkins**
I'm assuming, we have a system preinstalled with **Docker Desktop** as well as **Jenkins** (haha perfect world xD).

 - Bring up the environment by simply typing: `docker-compose up`. This will print out the initial password we can use to bring up an environment.
 - Once logged in, you can now create the initial [**Jenkins**](https://jenkins.io/) account. I typically use `gems2807` user for my local environments. Afterward, you can create pipelines.
## Creating a Pipeline Steps

To create the repository on your system :-

-   [https://github.com/gems2000/evolvfit-devops-task-jenkins](https://github.com/gems2000/evolvfit-devops-task-jenkins)

Then clone the repository locally.

**ACCOUNT**="gems2000"  
**git** clone git@github.com:**$ACCOUNT**/evolvfit-devops-task-jenkins.git  
**cd** evolvfit-devops-task-jenkins

Add the  **Jenkinsfile** 
   

After adding this, push the changes:

    git add .  
    git commit -m "Adding CI Pipeline (Jenkinsfile)"  
    git push

On the local Jenkins server,  [http://localhost:8080](http://localhost:8080/), you can add a new item, chose  `Pipeline`:
![1](1.jpg))
Then hit  `OK`  and select the Pipeline tab, paste the URL of the forked repository:


![2](2.jpg)

His save and run this. Click on the  `Open Blue Ocean`  link of the left panel to view the pipeline using the  [**BlueOcean**](https://jenkins.io/projects/blueocean/)  interface, which looks something like this below:



![](3.jpg)
## Resources

* Python Web Microframework
    * [Flask](http://flask.pocoo.org/)
* Testing
    * [Testing Flask Applications](http://flask.pocoo.org/docs/1.0/testing/)
    * [Python unittests in Jenkins?](https://stackoverflow.com/questions/11241781/python-unittests-in-jenkins)
* Python Environment
    * [python](https://www.python.org/) - language versions
    * [pyenv](https://github.com/pyenv/pyenv) - manage python versions
    * [virtualenv](https://virtualenv.pypa.io) to isolate packages with both Python 2 and Python 3.
    * [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) - pyenv plugin for ease-of-use pyenv + virtualenv integration.  Can automatically switch virtualenv based on setting in `.python-version`.# **Flask Web Microframework**
