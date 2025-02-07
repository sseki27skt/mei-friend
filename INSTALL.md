# mei-friend-online
mei-friend running within a browser

## To configure:

### Set up Github OAuth application:
* Go to https://github.com/settings/developers
* Click on "Register a new application"
* Enter application name = "mei-friend"
* Enter homepage = "https://iwk.mdw.ac.at"
* Enter callback URL = "http://localhost:4000/authorize"
* Click "Register application"
* Click "Generate a client secret" and log in if necessary
* Retain this page for configuration in the next steps:

### Set up mei-friend-online app
* `git clone git@github.com:mei-friend/mei-friend`
* `cd mei-friend`
* `cp env-template .env`
* Edit .env to add in CLIENT_ID and SECRET_ID from the Github OAuth application
* Add a random hard to guess string as FLASK_SECRET
* If required, add a REDIRECT_URL to override the flask url_for("authorize") route in deployment
* If required, add STATIC_URL_PATH and/or STATIC_FOLDER to override the Flask defaults in deployment
* For development mode, set FLASK_ENV to "development" => do not deploy in development mode!
* For deployment, *un*set FLASK_APP. This will cause wsgi.py to be used instead.
* Run `python -m venv venv` (if your system python is not python 3, run `python3 -m venv venv`)
* Run `. venv/bin/activate` (for Windows, use ` . venv\Scripts\activate`). Your prompt should update to show (venv) at the start.
* Run `pip install -r requirements.txt`
* Download CodeMirror 5.x from <https://codemirror.net/5> -> Get the current version
* Extract it and put it into app/static with directory name 'CodeMirror'

## To run:
### Development mode:
* `. venv/bin/activate` (for Windows, use ` . venv\Scripts\activate`)
* `flask run`

On Windows, if your browser blocks .js files because they are served wrongly as `text/plain`, add these lines to `routes.py`:

```python
import mimetypes
mimetypes.add_type('application/javascript', '.js')
```
### Production deployment:
* Use wsgi and gunicorn (instructions tbc)

### To update Python dependencies:
* The `cryptography` module requires rust, which may need updating
    - E.g., on Debian-based systems: `apt install rustc`
* Ensure current pip version: `pip install --upgrade pip`
* Run upgrade of dependencies: `pip install -r requirements.txt`
