# General Cheatsheet for Flask in VSCode on Windows - Zero to deployment (for those of us who can NOT deal with git to save our lives). No prior flask experience required.
It is a little hard to create a Flask app on Windows without Git if you haven't done it before - I learned that the hard way - but luckily, here's a super easy way to set one up in those circumstances.

## Assumptions
I'm going to assume the following things. If you don't, this probably won't be really useful for you
- You've got Visual Studio Code installed.
- You've got Python3 installed.
- You have basic know-how in Python, SQL, HTML and CSS

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
   - base.html
   - layout.html
- app.py
- helpers.py
- db_init.py
- db_schema.sql
- main.db
```
## An extremely simple flask app
### Coding
- In `app.py`, write out the following code to import the Flask library from your virtual enviroment and create an instance of the flask object.
```
from flask import Flask
app = Flask(__name__)
```
- Also in `app.py` write out the following code to define your homepage. Use Flask's `app.route` decorator to map the URL route `/` to that function. In this case, our homepage will just show a simple string "Hello World!"
```
@app.route("/")
def home():
    return "Hello, World!"
```
- Save your changes.
### Run your Flask app.
- Execute the following code in your terminal to run your app in a development server.
```
flask run
```
- You should see something similar as the output.
```
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```
- You by clicking on the link provided to you in the terminal, a web browser will be opened, displaying your flask app. A white page with two very unconspicious words on it reading "Hello World!". Congradulations, you are now an expert in Flask!

## Jinja Templating (pt. 1)
- Flask comes with a template called Jinja which works with HTML and helps you to build several similar webages without having to repeat common lines of HTML. The example below demonstrates this functionality - sit tight!

### base.html
```
<!-- everything that is neccessary but won't actually appear on your page-->

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <!--meta config-->
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!--external stylesheets-->
    <link rel="stylesheet" href="../static/css/utils.css">
    <link rel="stylesheet" href="../static/css/style.css">
</head>
<body>
    {% block template %}{% endblock %} 
    <!--external javascripts-->
    <script src="../static/js/jquery-3.6.0.js"></script>
    <script src="../static/js/scripts.js"></script>
</body>
</html>
```
### layout.html
```
<!-- Everything that would appear on every (or more than two) pages. -->
<!-- This is usually the footer and the header-->

{% extends "base.html" %}
{% block template %}
    <!--top navigation bar-->
    <header>
        <a href="/"><img class="header-logo" src="../static/images/logo.png" alt="logo"></a>
        <div>
            <p class="contact-detail" style="text-align: right; color: silver; font-size: 14px; padding:0px 10px;">
                <img src="../static/images/whatsapp20x20.png" style="margin-bottom: -5px;" alt="">
                078 774 7326
            </p>
            <nav>
                <a class="navlink" href="/">Home</a>
                <a class="navlink" href="/">Page1</a>
                <a class="navlink" href="/">Page2</a>
                <a class="navlink" href="/">Page2/a>
            </nav>
        </div>
    </header>
    <!--end of navigation bar-->
    <main style="min-height: 100vh;">
        {% block main %}{% endblock %}
    </main>
    <!--bottom footer-->
    <footer>
        <div class="social-icons" style="text-align: center;">
            <img src="../static/images/insta45x45.png" alt="">
            <img src="../static/images/pinterest45x45.png" alt="">
            <img src="../static/images/facebook45x45.png" alt="">
            <img src="../static/images/whatsapp45x45.png" alt="">
        </div>
        &copy; Company Name 2022
    </footer>
    <!--end of footer-->
{% endblock %}
```
### index.html
```
<!--Everything that appearsbetween the footer and the header on the homepage-->

{% extends "layout.html" %}
{% block main %}
<main style="min-height: 100vh; padding-top: 70px;">
    <section>
        <h1>Header here</h1><br>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Sapiente minus voluptas maiores explicabo corporis placeat alias blanditiis eos fugiat doloribus,              corrupti esse perspiciatis, consectetur porro incidunt debitis. Quaerat, quod perferendis!</p><br>
        <a href="about">
         <button>Learn More</button>
        </a>
    </section>
</main>
{% endblock %}
```
### about.html
```
<!--Everything that appears between the header and footer on the about page-->
{% extends "layout.html" %}
{% block main %}
<main style="min-height: 100vh; padding-top: 70px;">
    <section>
        <div class="about">
            <h1>About Us</h1>
            <br>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quaerat obcaecati id libero exercitationem dolorum totam corporis, hic nisi, cum possimus aspernatur reprehenderit omnis commodi tenetur cumque ratione qui itaque Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptate perspiciatis atque, pariatur enim ex impedit qui eveniet sed vero asperiores, aperiam officia praesentium aut ab. Aliquid voluptatum voluptate laborum ipsa.  Lorem ipsum dolor sit amet consectetur adipisicing elit. Fugiat id placeat cupiditate quaerat autem odit eaque laboriosam omnis velit nulla cum repellat illum repellendus sit veniam quas, necessitatibus est atque.</p><br>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Vero possimus, earum neque veritatis inventore quas omnis sint eaque, repellendus cumque soluta blanditiis delectus! Harum eius quas eligendi maiores fugit minus! Lorem ipsum dolor sit amet consectetur adipisicing elit. Est, tempora ratione necessitatibus nulla quos explicabo voluptate? Facere laborum natus delectus voluptate earum, dolores saepe libero, dolorum quas nesciunt nulla fugiat!</p>
        </div>
    </section>
</main>
{% endblock %}
```
### app.py
```
# Landing
@app.route("/")
def index():
    return render_template("site/index.html")

# About
@app.route("/about")
def about():
    return render_template("site/about.html")
```

- Now, when you restart the developmet server by executing `Shift-C` and then `flask run` in your terminal, you should see a complete webpage, header, footer, contents and all, as well as all the things that run in the background, such as the links to external stylesheets etc.

### Explanation
- In base.html, you'll see a line containing `{% block template %}{% endblock %}`, placed exactly where everything in layout.html would be placed if you were to write the whole thing in HTML without using Jinja. In layout.html, we see the same blocks again, this time with contents between them. This content was, in essence, taken from layout.html and placed into base.html in the proccess of displaying the page.
- The first line of layout.html contains `{% extends "base.html" %}`. This tells Jinja which file to look to in order to find the matching blocks.
- In this example, to display the homepage, Jinja starts with `site/about.html` as specified by the render_template function, takes content from that file to `layout.html`, and takes content from `layout.html` to `base.html`, in order to put together a full html webpage.

## Working with a SQL database
