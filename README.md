# The Ultimate Cheatsheet for Flask in VSCode on Windows - Zero to deployment (for those of us who can NOT deal with git to save our lives). No prior flask experience required.
It is a little hard to create a Flask app on Windows without Git if you haven't done it before - I learned that the hard way - but luckily, here's a super easy way to set one up in those circumstances.

## Assumptions
I'm going to assume the following things. If you don't, this probably won't be really useful for you
- You've got Visual Studio Code installed.
- You've got Python3 installed.
- You have basic know-how in Python, HTML and CSS

## Setup
### Your virtual environment.
- Make sure you have the [Python extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-python.python) installed.

- Before we actually do any coding, we're going to have to set up a development enviroment first. On your file system, go ahead and create a folder to hold your flask app and everything that comes with it. You can name it whatever you please. 

- Once you've done that, Open up your VSCode and navigate to the folder you just created, setting it as your current workspace.

- Using CTRL+Shift+\` ,  open up a terminal window and run the following command to create yourself a so-called "virtual environment" named `.venv`. You'll see a folder named `.venv` appear in your workspace. Make sure you're using Windows Command Prompt, not Powershell. Like I said, Git will not exist here.
```
py -3 -m venv .venv
```
- This may take a while. Once you're done, run this command to activate your virtual environment. You may receive a pop up asking you if you want to set .venv as your python interpreter.
```
.venv\scripts\activate
```
- Next, hold Ctrl+Shift+P to open up your Command palette and select the "Python: Select Interpreter" command. And select the virtual environment in your project folder that starts with `./.venv` or `.\.venv.`

- Now that you have a virtual environment, run the following command to make sure our pip is installed and up to date.
```
python -m pip install --upgrade pip
```
- And now, we can install flask by running the following command in the terminal.
```
python -m pip install flask
```

We're all set to begin bulding our flask application! Happy Coding!

### Ideal directory structure for Flask
- Using the terminal or the GUI, whichever you prefer, create the neccessary folders until your directory structure resembles something like the following.
```
root
- .venv
- static
   - css
      - utils.css
      - style.css
   - js
      - utilities.js
      - scripts.js
      - jquery-3.6.0.min.js
   - images
      - logo-image.png
      - image.jpg
      - image(1).png
   - fonts
      - font-1.otf
      - font-2.ttf
   - uploads
      - // just in case users of your web application will upload files, they will be stored here.
- Templates
   - site
      - index.html
      - about.html
   - errors
      - 404.html
      - 500.html
      - 501.html
   - emails
      - automatic_email.html
- app.py
- helpers.py
- db_init.py
- db_schema.sql
- main.db
```
## Building a minimal flask app
