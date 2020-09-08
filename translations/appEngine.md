# Translation of the lab Google Cloud fundamentals: Getting started with App engine

## Objectives
    -Initialize App Engine
    -Preview an App Engine running locally in the Cloud shell
    -Deploy an App Engine application, so that others can reach it
    -Disable an App Engine application when you nolonger want it to be visible

## Setting up your lab Environment

List the active account 
    gcloud auth list
     The output should look like this:
            Credentialed account:
                -<account>@<domain>.com (active) where <account> is your account name and <domain> is your doamin name

List the your project id
    gcloud config list project
     The output should look like this:
        [core]
        project = <project_ID>
    

## Task 1. Initialize App Engine

Initialize your App Engine app with your project and choose its region:
    gcloud app create --project=$DEVSHELL_PROJECT_ID 

    '$DEVSHELL_PROJECT_ID' is just an environment variable holding your project id
    When prompted, select the region for your App Engine application

Clone the source code repository for a sample application in the hello_world directory:
    git clone https://github.com/GoogleCloudPlatform/python-docs-samples

Navigate to the source directory:
    cd python-docs-samples/appengine/standard_python3/hello_world

## Task 2 Run Hello World application locally

Update the packages list:
    sudo apt-get update

Install virtual environment:
    sudo apt-get install virtualenv

Activate the virtual environment in which you will run your application:
    virtualenv -p python3 venv

Activate the virtual environment:
    source venv/bin/activate

Navigate to your project directory and install dependencies:
    cd ..
    pip install -r requirements.txt

Run the application:
    python main.py
    Please ignore the warning if any

Preview the application by navigating to Web preview on the cloud shell and clicking Preview on port 8080
Result: A web page with a text Hello World!
Press CTRL+C while on the cloud shell window to abort the deployed serveice
List deployed app engine services:
    gcloud app services list
    Result No services deployed

## Task 3 Deploy and run Hello World on App Engine

Navigate to the source directory
    cd ~/python-docs-samples/appengine/standard_python3/hell_world

Deploy your Hello World application
    gcloud app deploy
    if prompted press Y and ENTER

Launch the browser to view the app
    gcloud app browse
    Copy and paste the url into a new browser window
    Result: Web page with text Hello World!

## Task 4 Disable the application
Delete the deployed service:
    gcloud app services delete SERVICES

    this deletes all the deployed services
    Refreshing the browser window of the application site gives a 404 error

That's it.



