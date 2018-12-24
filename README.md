# RowanRooms
RowanRooms is the course project for the Fall 2018 Introduction to IoT course at Rowan University. 

## Web Frontend
This is the web frontend for the RowanRooms project. It serves as a user interface for the Rowan Rooms application.

### Implementation
The easiest way to test this web page is to run it on a [Flask](flask.pocoo.org) server. 

1. Begin by downloading the [python-docs-samples](https://github.com/GoogleCloudPlatform/python-docs-samples) repo, which contains numerous Python code samples for working with Google Cloud. 
2. With a command prompt, navigate to the [../python-docs-samples/appengine/standard/flask/tutorial/](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard/flask/tutorial) folder.
3. Follow the steps [here](https://cloud.google.com/appengine/docs/standard/python/download) to download the Google Cloud SDK. This comes with a development server running the web frontend.
4. Open app.yaml your IDE, text editor, etc. of choice and append the following code:
```yaml
runtime: python27
api_version: 1
threadsafe: true

libraries:
- name: ssl
  version: latest
  
# [START handlers]
handlers:
- url: /static
  static_dir: static
- url: /.*
  script: main.app
# [END handlers]
```
5. Append the following code to main.py:
```python

```
6. Put index.html inside "..\templates\" and stylesheet.css inside "..\static\"
7. Set the FLASK_APP environment variable to main.py using `set FLASK_APP=main.py` in the command prompt.
8. Run the flask app with `run flask` in the command prompt.
