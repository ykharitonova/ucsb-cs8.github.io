---
topic: "Flask Webapps: 01"
desc: "Getting Started"
indent: true
---

{% include flask_webapps_header.html %}


This page describes how to get started with Flask, a "Python Microframework" for building web apps.

More specifically, this page describes how to get started with Flask on your ACMS accounts, which requires a few adjustments to the standard tutorial.

# Audience

The audience for this tutorial is students in CMPSC 8 or a similar intro Python course at UCSB.

Students are expected to be familiar with the following general computing concepts before diving into this tutorial.

* For CMPSC 8 students, using the Unix Command line (terminal windows) on the UCSB CoE Systems.
* For other students, using similar tools on their own laptop (Windows, Mac or Linux)
* Using the cd, ls and mkdir Unix commands.

In terms of Python, students should know how to:

* Simple function definitions in Python
* Execute a Python file at the Unix command line (as opposed to running it from with IDLE).

# About Flask

Flask is a Python module that provides an easy way to get started with web programming.

The easiest way to get started is to try some small examples.     Below is a small example of a Python program that uses Flask.  There are seven lines of code here (not including the blank lines), and before the end of this document, we'll explain every single part of every one of these lines.  But first, we'll do a few things that will allow us to run these seven lines of code, setting up a small web application.    That web application doesn't do much that is very interesting—it puts the words "Hello World!" up in the browser every time you send it a request.    But, it provides a starting point that we can then modify to do more interesting things.

* Make a directory under your `~/cs8` directory called `web-app-intro`
    * As a reminder, you can do that with the command `mkdir -p ~/cs8/web-app-intro`
* Then, cd into that directory
    * As a reminder, that looks like this: `cd ~/cs8/web-app-intro`
* Open up IDLE using the command `idle3 &` because we are going to write some code.
    * Putting the `&` on the command helps to make sure that we get to keep our cursor and type additional commands
    * If you are on Windows, instead of the `&`, just open a second terminal or command window, or open IDLE for Python 3 from an Applications menu or icon.

```
[pconrad@csil-01 ~]$ mkdir ~/cs8/web-app-intro
[pconrad@csil-01 ~]$ cd ~/cs8/web-app-intro
[pconrad@csil-01 web-app-intro]$ idle3 &
[pconrad@csil-01 web-app-intro]$ 

```


Using IDLE (or any other program editor of your choosing) put these lines of code in a file called `hello.py`, and save it into that `~/cs8/web-app-intro` directory

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run(port=5000)
```

To get this working, all you have to do is type this at a terminal prompt (NOT the Python `>>>` prompt, but instead, do it at the Unix (or Mac or Windows) command line, i.e. the Terminal window:

```
python3 hello.py
```

(Note: if you are working on your own system, you might use `python` instead of `python3` to run this example.   I won't mention that every time throughout this tutorial.)


Sadly, it probably won't work the first time you try it.  You'll probably get a message like this one:

```
$ python hello.py
Traceback (most recent call last):
  File "hello.py", line 1, in 
    from flask import Flask
ImportError: No module named flask
$ 
```

# Why do we have to install Flask?  Why isn't it already there for us to use?

By default, the Flask module is not part of the Python setup.    It is fairly common occurrence to need a module that is not part of the default Python installation.  There are so many modules out there that extend Python's capabilities in various ways, that it isn't a good use of disk space or time to install all of them in advance.   Typically, they get installed only "as needed".

How you do it depends on whether you are running on one of the CSIL systems, or your own machine.

On CSIL, we use the `pip3` command to install flask.   We need the `--user` option to ensure that we install it for just ourselves (we don't have permission to install it for the entire system):

```
pip3 install --user flask
```

If you are working on your own laptop, you might use either this command:


```
pip3 install flask
```

or, if the `pip` command work with Python3 on your system:

```
pip install flask
```


Here is an example of what a successful install looks like on CSIL.    The reason the output is so long is that Flask depends on other pieces of software to work properly.  The pip command figures out what those pieces are, and installs them as well along with everything else.
 
```
[pconrad@csil-01 ~]$ pip3 install --user flask
Collecting flask
  Downloading https://files.pythonhosted.org/packages/77/32/e3597cb19ffffe724ad4bf0beca4153419918e7fa4ba6a34b04ee4da3371/Flask-0.12.2-py2.py3-none-any.whl (83kB)
    100% |████████████████████████████████| 92kB 1.8MB/s 
Collecting itsdangerous>=0.21 (from flask)
  Downloading https://files.pythonhosted.org/packages/dc/b4/a60bcdba945c00f6d608d8975131ab3f25b22f2bcfe1dab221165194b2d4/itsdangerous-0.24.tar.gz (46kB)
    100% |████████████████████████████████| 51kB 1.4MB/s 
Requirement already satisfied: Jinja2>=2.4 in /usr/lib/python3.6/site-packages (from flask)
Requirement already satisfied: Werkzeug>=0.7 in /usr/local/lib64/python3.6/site-packages (from flask)
Collecting click>=2.0 (from flask)
  Downloading https://files.pythonhosted.org/packages/34/c1/8806f99713ddb993c5366c362b2f908f18269f8d792aff1abfd700775a77/click-6.7-py2.py3-none-any.whl (71kB)
    100% |████████████████████████████████| 71kB 1.8MB/s 
Requirement already satisfied: MarkupSafe>=0.23 in /usr/lib64/python3.6/site-packages (from Jinja2>=2.4->flask)
Building wheels for collected packages: itsdangerous
  Running setup.py bdist_wheel for itsdangerous ... done
  Stored in directory: /cs/faculty/pconrad/.cache/pip/wheels/2c/4a/61/5599631c1554768c6290b08c02c72d7317910374ca602ff1e5
Successfully built itsdangerous
Installing collected packages: itsdangerous, click, flask
Successfully installed click-6.7 flask-0.12.2 itsdangerous-0.24
You are using pip version 9.0.1, however version 9.0.3 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
[pconrad@csil-01 ~]$ 
```

* A note about that `itsdangerous` stuff: don't worry.  It isn't "dangerous" to install `itsdangerous`.   
    * On the contrary&mdash;the `itsdangerous` python module is designed to help you avoid danger from various security vulnerabilities that webapps can open up.  But more on that another time.

Once the Flask module is added to your individual user's Python installation, you can run the file again by typing:

```
python3 hello.py
```
Here is what that should look like:

```
[spis15t7@ieng6-240]:~:179$ python hello.py
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

If that works, great!   But if it doesn't work, it is likely that the problem will be this error message:

``` 
socket.error: [Errno 98] Address already in use
```

Actually, that error message will be the last line of a long sequence of messages, that look like these (the ... means I've left out many lines of output).

``` 
Traceback (most recent call last):
  File "hello.py", line 9, in 
    app.run()
  File "/home/linux/ieng6/spis15/spis15t7/.local/lib/python2.7/site-packages/flask/app.py", line 772, in run
    run_simple(host, port, self, **options)
...
  File "/software/common/python-2.7.10/lib/python2.7/socket.py", line 228, in meth
    return getattr(self._sock,name)(*args)
socket.error: [Errno 98] Address already in use
```

There will be times later when we will want to dive deep into that long "Traceback", but this is not one of those times. The last line, in this case, tells us everything we need to know. It tells us that the default port number that Flask listens for connections on, `5000`, is already being used by some other program on `ieng6-240.ucsd.edu`. In that case, no worries. We'll just choose a different number. We do that by change the line of code: `app.run(port=5000)` to `app.run(port=5001)`.  We keep doing this, i.e. adding one to the port number, until we find a port number that works for us.  

Now let's suppose it "works", meaning that when you type in python hello.py you get a message such as this one:
```
[spis15t7@ieng6-240]:~:179$ python hello.py
 * Running on http://127.0.0.1:5001/ (Press CTRL+C to quit)
```

This may not be very impressive. It gets a little more awesome when you realize that you've just put up a web server that you can connect to with a browser. 

* Bring up a browser on the SAME machine as the server
* To do this, bring up a browser, but&mdash;and this part is important&mdash;on the SAME machine as where you are running this server. For now, your server is not available to the entire internet—it is only available to browsers running on the same machine as the server.   We'll say what to do with that browser in a minute.

To be more clear, here are the different situations:

| Situation | What to expect |
|-----------|-----------------|
| Sitting at a Linux computer in a UCSB CS Computer lab (Phelps or CSIL) | No problem: fire up the web browser, and it will automatically be on the same machine as your terminal windows |
| Using your own laptop, but using `ssh -X ...` or MobaXTerm to access a CSIL machine | You'll need to fire up a web browser that is running ON THAT SAME CSIL MACHINE, instead of running on your local laptop.  Use can use the command `firefox &` to do that. |
| Using your own laptop, and running Python *directly on your laptop* | Your default web browser on your laptop should work fine |

Once you have your browser up, enter the web address `http://localhost:5000` or `http://127.0.0.1:5000` 

This is the web address where your server is located.   If you enter this in your browser, you should see the message "Hello World" come up in the browser, as shown here:


# What next?

Now, here are a few things to try, and some questions to answer.  As you try these things and think through what is happening, you should begin to understand a few things about how this code is working.

Before you start, arrange the windows on your screen so that you have the window where you typed python hello.py on the left side of your screen (we'll call this the server window), and the browser window on the right side of your screen.

* In the browser window, hit 'refresh' a few times.     What do you see in the server window?   
* In the window where you originally typed python hello.py, type a CTRL+C (that is, "Control-C"). Then try hitting "refresh" in the browser where you typed localhost:5000, and see what happens. Then, type the python hello.py command again, and try hitting refresh in the browser again.
* Use CTRL+C on the server side to stop the server, edit the hello.py file to change the string "Hello World" to something else, for example, if your name is Cory, make it say: "Hello from Cory's server".  Start the server up again and then hit refresh in your browser a few times.

# What to do next?   

There are two choices.

The next page of this tutorial suggest a few things we can do next to make our first Flask web app a bit more interesting.   If you are content to move ahead, and figure things out as you go, just skip the rest of this page, and click to go to 
[Web Apps Intro Part 2](/tutorials/flask_webapps_02)

If you are the type that wants to understand everything before moving on, the section below explains each line of code in our `hello.py` file, one at a time.  If you prefer, read through that first, before moving on.

# Explaining all the lines of code

Ok, here is an explanation of each of the lines of code.   Then, we'll walk through how to do a few things that are a bit more interesting.

{% highlight python linenos %}
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run(port=5000)
{% endhighlight %}

<style>
div.nicer-table table * td:first-child { 
   text-align:center;
   font-family: Courier New, fixed;
}
div.nicer-table table * td { padding: 4px; }
</style>


<div class="nicer-table" markdown="1">

| line | explanation  |   
|------|--------------|
|  1   | 	This code pulls in the definition of a new datatype called `Flask` (note the uppercase `F`) from a module called `flask` (note the lowercase `f`.) In Python, when you import something, you are telling the Python interpreter that you want to build your software on top of some software already written by someone else. |
|  2   |	This line of code is an assignment statement. The right hand side is evaluated, and then the variable on the left is set to the result of the right hand side. The right hand side, Flask(__name__) creates a new object of type Flask. The `__name__` parameter is explained further in the box "About the First Parameter" on this page of the api documentation. We'll defer the details for now, and just say: for very simple Flask applications, __name__ is always the correct choice. |
| 4	| The `@` signals that what follows is a Python annotation. It indicates that there is some special way the following function definition should be handled. In this case, the annotation `app.route("/")` indicates that this function is called whenever we ask for the main page on this web server (i.e. `"/"`. This will make more sense when we add other pages later. |
| 5	 | Lines 5 and 6 are a regular plain old Python function definition. We can see that the function is called `"hello"`, and takes no parameters.
| 6	 |  	This function returns a string, `"Hello World!"`, which is used as the page to display for the main page of the web server (`"/"`).
| 8	| Line 8 has an if test that checks the special variable `__name__` to see if it has the special value "__main__". This is the mysterious "conditional script stanza", which we aren't going to explain in detail here. Instead, we'll just say that whatever "main thing" a Python code is supposed to do when you select "Run" in IDLE, or type python filename.py, in this case python hello.py, should typically be wrapped in this if test. That makes your file much more useful, because then the definitions it contains can be included as a module in another file.
| 9	 | 	Line 9 is the line that actually causes our web server to start running. The dot-notation app.run() tells us that run is a method of the object app. By putting () after it, we are making a function call to that method, and starting things in motion.   The `port=5000` part indicates the port number we are going to listen for connections on.   By default, web servers listen for connections on port 80, and web browsers send requests to port 80.  We don't have the necessary permissions to set up a server on port 80 (port numbers lower than 1024 are restricted to system administrators), but we can set up a server on a "high numbered port", basically anywhere between 1024 and 65536.  For various reasons, its better to choose a number starting at 5000 (less likely to conflict with some other network service.)   Being able to specify a port number both on the server side and the browser side allows many users to set up servers and connect to them all on the same machine. |

</div>


{% include flask_webapps_table_of_contents.html %}
