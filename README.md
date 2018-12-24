# RowanRooms
RowanRooms is the course project for the Fall 2018 Introduction to IoT course at Rowan University. 

## Web Frontend
This is the web frontend for the RowanRooms project. It serves as a user interface for the Rowan Rooms application.

### Implementation
The easiest way to test this web page is to run it on a [Flask](flask.pocoo.org) server. 

1. Begin by downloading the [python-docs-samples](https://github.com/GoogleCloudPlatform/python-docs-samples) repo, which contains numerous Python code samples for working with Google Cloud. 
2. Direct your browser and to the [python-docs-samples/appengine/standard/flask/tutorial/](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard/flask/tutorial) folder. Follow the steps for installing dependencies.
3. Follow the steps [here](https://cloud.google.com/appengine/docs/standard/python/download) to download the Google Cloud SDK. This comes with a development server for running the web frontend.
4. Open app.yaml in your IDE, text editor, etc. of choice and append the following code:
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
5. Append the following code to main.py. Much of the code is the same from the original main.py. The additional lines of code will create two JSON objects `room1` and `room2` for rooms:
```python
# Copyright 2016 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# [START app]
import json
import logging
import time
# [START imports]
from flask import Flask, render_template, request
# [END imports]
def get_room_list():
	rooms = []
	# change the following code
	room1 = {"room_name": "Room 1", 
			   "occupancy": 6, 
			   "temperature": 24.5, 
			   "room_image": "dummy_url1", 
			   "room_limit": 24, 
			   "timestamp": time.asctime(time.localtime(time.time()))}
	rooms.append(room1)
	room2 = {"room_name": "Room 2", 
			   "occupancy": 0, 
			   "temperature": 23.1, 
			   "room_image": "dummy_url2", 
			   "room_limit": 24, 
			   "timestamp": time.asctime(time.localtime(time.time()))}
	rooms.append(room2)
	# change the above code
	return rooms
# [START create_app]
app = Flask(__name__)
# [END create_app]
@app.route('/')
def index():
	return render_template('index.html')
 
@app.route('/rooms', methods=['GET'])
def rooms():
	return json.dumps(get_room_list())
# [START form]
@app.route('/form')
def form():
	return render_template('form.html')
# [END form]
# [START submitted]
@app.route('/submitted', methods=['POST'])
def submitted_form():
	name = request.form['name']
	email = request.form['email']
	site = request.form['site_url']
	comments = request.form['comments']
	# [END submitted]
	# [START render_template]
	return render_template(
		'submitted_form.html',
		name=name,
		email=email,
		site=site,
		comments=comments)
	# [END render_template]
@app.errorhandler(500)
def server_error(e):
	# Log the error and stacktrace.
	logging.exception('An error occurred during a request.')
	return 'An internal error occurred.', 500
# [END app]
```
6. Put index.html inside "..\templates\" and stylesheet.css inside "..\static\"
7. Set the FLASK_APP environment variable to main.py using `set FLASK_APP=main.py` in the command prompt.
8. Run the flask app with `run flask` in the command prompt.
