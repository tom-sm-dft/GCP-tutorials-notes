# GCP deploy python application

## Objectives
* Create a project - Projects bundle code, virtual machines and other resources together for easier development and monitoring.
* Build and run your 'Hello World!' app - how to run app using Cloud shell directly in browser. Then deploy app to the web using gcloud command.
* After will be able to experiment with it.

## Project set-up
GCP organises resources into projects, which collect all of the related resources for a single application in one place.
Begin by creating a new project or selecting an existing project for this tutorial.
[Creating and managing project set-up](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project?hl=en-GB)

## Using cloud shell
Shell is a built-in command-line tool for the console. We're going to use Cloud Shell to deploy our app.
To activate click >_ button in the top right.
### Clone the sample code
Use Cloud Shell to clone and navigate to the 'Hello World' code. The sample code is cloned from your project repository to the Cloud Shell.
Note: If the directory already exists, remove the previous files before cloning.
In Cloud Shell, enter the following:
```bash
git clone https://github.com/GoogleCloudPlatform/python-docs-samples
```
Then switch to the tutorial directory:
```bash
cd python-docs-samples/appengine/standard_python37/hello_world
```

## Configuring your deployment
### Exploring the application
Files that configure the application
```bash
ls
>>> app.yaml  main.py  main_test.py  requirements.txt
cat main.py
```
```python
# If `entrypoint` is not defined in app.yaml, App Engine will look for an app
# called `app` in `main.py`.
app = Flask(__name__)
@app.route('/')
def hello():
    """Return a friendly HTTP greeting."""
    return 'Hello World!'
if __name__ == '__main__':
    # This is used when running locally only. When deploying to Google App
    # Engine, a webserver process such as Gunicorn will serve the app. This
    # can be configured by adding an `entrypoint` to app.yaml.
    app.run(host='127.0.0.1', port=8080, debug=True)
# [END gae_python37_app]
```
The application is a simple Python application that uses the Flask web framework. This Python app responds to a request with an HTTP header and the message Hello World!.
### Exploring the configuration
App Engine uses YAML files to specify a deployment's configuration. app.yaml files contain information about your application, like the runtime environment, environment variables and more.
This file contains the minimal amount of configuration required for a Python 3 application. The runtime field specifies the python37 run-time environment.
```bash
cat app.yaml
```
```yaml
runtime: python37
```
[Configuration options for python.](https://cloud.google.com/appengine/docs/standard/python3/config/appref?hl=en-GB)

## Testing your app

### On cloud shell
Cloud Shell lets you test your app before deploying to make sure that it's running as intended, just like debugging on your local machine.

To test your app, first create an isolated virtual environment. This ensures that your app does not interfere with other Python applications that may be available on your system.
```bash
virtualenv --python python3 ~/envs/hello_world
```
Activate your newly created virtual environment:
```bash
source ~/envs/hello_world/bin/activate
```
Use pip to install project dependencies. This 'Hello World' app depends on the Flask microframework:
```bash
pip install -r requirements.txt
```
Finally, run your app in Cloud Shell using the Flask development server:
```bash
python main.py
```

### Preview your app with 'Web preview'
Your app is now running on Cloud Shell. You can access the app by clicking the Web preview  button at the top of the Cloud Shell pane and choosing Preview on port 8080.

### Terminating the preview instance
Press Ctrl+C in cloud shell.















