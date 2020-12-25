---
title: Head-first Kubernetes
description: A Kubernetes tutorial for complete beginners.
---

## Hello Docker World

### Hello Flask

In this chapter, we will learn a few things about Docker.

Lets start with a very simple Hello World application in Flask.

For those who do not know, Flask is a minimal web framework for Python. The examples in this book will use Flask. In case you are not familiar with Python or Flask, we will walk you through the code. It should be pretty simple and easy to follow.

As always, its good to get our feet wet with a simple Hello World web application in Flask.

```python
# hello.py

# Import the Flask object
from flask import Flask

# Create an object for our web application.
# __name__ in Python is bound to the name of the current module
# which is based on the file name.
# For this case, the name of our file is hello.py so the name of
# our module would be "hello".
app = Flask(__name__)

# This is a decorator. In Python decorators are used to hold
# code that sandwich the code in a function.

# Decorators are used to annotate functions. For instance,
# in the following line, we are saying that the hello function
# should be called whenever the root URL in our web application
# is hit.
@app.route("/")

# This is how you define a function in Python.
def hello():
	# Our function returns the famous "Hello World" string.
	# Like we said the code in the decorator sandwiches the
	# code in our function.
	# We also said that the toast at the top of our sandwich
	# essentially passes control to our function whenever the
	# root of our web application is hit.
	# The toast at the bottom of the sandwich takes whatever
	# the function returns and passes it back to the client
	# that hit the root of our web application.
	return "Hello World!"
```

In order to run this fun little application, we can do the following:

Firstly, we need to install flask. In Python, this is done using pip - which is the Python package manager with a name that Bell Labs would be proud of:  PIP Installs Packages.

We can totally install Flask using pip and get on with the rest of it but that would mean Flask would end up in our global Python packages space.

```bash
$ pip install flask
...

$ which flask
/usr/local/bin/flask

$ 🙄
zsh: command not found: 🙄
```

This is fine. Sometimes. But if you are doing a bunch of work in Python, you would end up with 100s and 1000s of packages on your system. Meh.

### Hello Sandbags

The thing that solves this problem is called virtual environments or venv in the Python world.

Virtual environments are cool because they let you install packages on a per-project bases without polluting your global Python installation. Virtual environments are also cool because they come built-in with Python 3.

Did I tell you that we will be using Python 3 in this book? Let me use this opportunity to remind you that Python 2 officially hit its end of life in April 2020  👻

So firstly, lets create a virtual environment for our little Hello World project. You can do it like so:

```bash
$ python -m venv ~/<path-to-the-virtual-environment>
```

I usually go with:

```bash
$ python -m venv ~/.venv/k8s
```

P.S. You can run many modules in Python by using the -m flag. I will come back to this shortly.

A virtual environment is nothing but a copy of all the files that are needed to run Python applications. You can see for yourself:

```bash
$ ls ~/.venv/k8s
drwxr-xr-x   6 alixedi  staff   192B Jul 31 13:01 .
drwxr-xr-x  36 alixedi  staff   1.1K Jul 31 13:01 ..
drwxr-xr-x  12 alixedi  staff   384B Jul 31 13:01 bin
drwxr-xr-x   2 alixedi  staff    64B Jul 31 13:01 include
drwxr-xr-x   3 alixedi  staff    96B Jul 31 13:01 lib
-rw-r--r--   1 alixedi  staff    75B Jul 31 13:01 pyvenv.cfg
```

Or more interestingly:

```bash
$ ls ~/.venv/k8s/bin
-rw-r--r--  1 alixedi  staff  2244 Jul 31 13:01 activate
-rw-r--r--  1 alixedi  staff  1300 Jul 31 13:01 activate.csh
-rw-r--r--  1 alixedi  staff  2452 Jul 31 13:01 activate.fish
-rwxr-xr-x  1 alixedi  staff   281 Jul 31 13:01 easy_install
-rwxr-xr-x  1 alixedi  staff   281 Jul 31 13:01 easy_install-3.7
-rwxr-xr-x  1 alixedi  staff   263 Jul 31 13:01 pip
-rwxr-xr-x  1 alixedi  staff   263 Jul 31 13:01 pip3
-rwxr-xr-x  1 alixedi  staff   263 Jul 31 13:01 pip3.7
lrwxr-xr-x  1 alixedi  staff     7 Jul 31 13:01 python -> python3
lrwxr-xr-x  1 alixedi  staff    22 Jul 31 13:01 python3 -> /usr/local/bin/python3
```

We can spot the whole cast in there including the python binary and pip.

Now in order to "activate" this virtual environment, we have - the activate script. Did you spot that in the last code snippet? Well done 👏

Here is how you activate a virtual environment:

```python
$ source ~/.venv/k8s/bin/activate
(k8s) $ wow!
zsh: command not found: wow!
```

😬

Right. Now that we have the virtual environment set up, we can install flask in it without polluting our global Python installation.

Here is how you would do it:

```python
(k8s) $ pip install flask
...
Installing collected packages: MarkupSafe, Jinja2, Werkzeug, click, itsdangerous, flask
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 flask-1.1.2 itsdangerous-1.1.0
```

In order to check if our virtual environment is doing what it said on the tin. Or what I said on the tin:

```python
(k8s) $ which python
~/.venv/k8s/bin/python
```

To double check:

```python
(k8s) $ python
Python 3.7.4 (default, Oct 12 2019, 18:55:28)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import flask
>>> awesome!
File "<stdin>", line 1
    awesome!
           ^
SyntaxError: invalid syntax
```

(Sorry again)

One final check. Installing flask in a venv would mean that its is not available globally:

```bash
(k8s) $ deactivate

$ which python
/usr/local/bin/python3

$ python
..
>>> import flask
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'flask'
```

ModuleNotFoundError. Music to me ears  🕺

Onwards. Flask. Web application.

We wrote ourselves an exciting little application in Flask. We should totally run it. Here is how:

```bash
(k8s) $ FLASK_APP=hello.py flask run
* Serving Flask app "hello.py"
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Looks promising. Lets see if it works. In a different terminal:

```python
$ curl localhost:5000
Hello World!
```

wOot!  🙌

I managed to write my excitement in the right window this time 💪

Before I move to containers and specifically Docker containers, I want to press home my advantage and introduce one more little magic trick in pip.

So doing a pip install <awesome-package> is nice and all for development but what if you want to distribute your application?

Wait what? We just cobbled together a Hello World and now we are distributing it? What exactly is distribute anyway? Why is it cool?

Well, I agree that our little Hello World thing is not going to get into ycombinator or anything but its still a fully functional - albeit dumb - web application.

The thing with web applications - like all applications - is that they need to be chucked around fairly often. For instance:

1. You might want to put our Hello World application in a code repository like GitHub. Every time someone in your team adds a little feature to it, you might want to run some tests using e.g. GitHub actions. This is called CI and its all the rave. Now in order to run tests on your application, GitHub actions would need to be able to easily install it - along with all its dependencies no?
2. Once you have them features working, you might want to release the latest version of your application to your users. Generally, for web applications, this would mean putting them on a server. Same story here. On the server you would need to reproduce the environment that your web application needs in order to run. AKA install.
3. You got 2 new junior engineers on your team. They need to quickly and easily be able to run your massively complex Hello World application on their local machine in order to build new features and get you that VC 💰

Luckily, pip has a trick or two up its sleeve that lets us reproduce the environment needed by our web application in order to run.

We can do this in 2 easy steps.

In the first step, we will capture the dependencies required by our web application.

```bash
(k8s) $ pip freeze
click==7.1.2
Flask==1.1.2
itsdangerous==1.1.0
Jinja2==2.11.2
MarkupSafe==1.1.1
Werkzeug==1.0.1

```

This gives us a list of all the dependencies and their correct versions that are installed in our virtual environment right now.

Lets put these in a file like so:

```bash
(k8s) $ pip freeze > requirements.txt
```

Now that our dependencies are in a file, we can commit this to the repository along with the code and voila! we have taken our first step to enable the distribution of our web application to the CI, the server and other developers.

Anything or anyone who wants to run our web application should be able to do so by following some simple steps:

```python
$ # Clone the repo and CD into it
$ git clone k8s
$ cd k8s

$ # Create a new venv and activate it
$ python -m venv ~/.venv/k8s
$ source ~/.venv/k8s/bin activate

$ # Install required packages into the venv
$ pip install -r requirements.txt

$ # Run that thing!
$ FLASK_APP=hello.py flask run
```

You can put these steps in a bash script and it would work beautifully. More or less. Until it doesn't.

Time to talk about containers.

Before I do, a little reminder of what a Python virtual environment is.

```python
$ ls ~/.venv/k8s
drwxr-xr-x   6 alixedi  staff   192B Jul 31 13:01 .
drwxr-xr-x  36 alixedi  staff   1.1K Jul 31 13:01 ..
drwxr-xr-x  12 alixedi  staff   384B Jul 31 13:01 bin
drwxr-xr-x   2 alixedi  staff    64B Jul 31 13:01 include
drwxr-xr-x   3 alixedi  staff    96B Jul 31 13:01 lib
-rw-r--r--   1 alixedi  staff    75B Jul 31 13:01 pyvenv.cfg
```

It is a directory containing all the Python dependencies that are needed to run a Python application. This includes the python binary, pip etc.

```bash
$ ls -l ~/.venv/k8s/bin
total 72
-rw-r--r--  1 alixedi  staff  2244 Jul 31 13:01 activate
..
-rwxr-xr-x  1 alixedi  staff   263 Jul 31 13:01 pip
..
lrwxr-xr-x  1 alixedi  staff     7 Jul 31 13:01 python -> python3
```

It also includes the packages that are needed by our application e.g. Flask:

```bash
$ ls -a ~/.local/share/virtualenvs/head-1st-k8s/lib/python3.7/site-packages
drwxr-xr-x  21 alixedi  staff   672B Jul 31 13:09 .
drwxr-xr-x   3 alixedi  staff    96B Jul 31 13:01 ..
drwxr-xr-x   9 alixedi  staff   288B Jul 31 13:09 Flask-1.1.2.dist-info
drwxr-xr-x   9 alixedi  staff   288B Jul 31 13:09 Jinja2-2.11.2.dist-info
drwxr-xr-x   8 alixedi  staff   256B Jul 31 13:09 MarkupSafe-1.1.1.dist-info
drwxr-xr-x   8 alixedi  staff   256B Jul 31 13:09 Werkzeug-1.0.1.dist-info
..

```

Its kind of like a sandbag. Sandbags are a cool idea. Like most cool ideas, the sandbag idea increases in awesomeness if we turn it all the way up to 10.

This is what containers do. Well not all the way up to 10. That would be virtual machines. Maybe all the way to 8.

First, lets talk about why.

While putting the packages that our application needs (aka dependencies) to run in a directory so that we can distribute our application easily has been really cool.

But we are still in a half-way house here.

You see the copy of the python binary we spotted in the bin folder in our virtual environment still needs a bunch of operating system libraries to run. If you are running a Linux machine, you can observe this like so:

```bash
(k8s) $ strace -s 2000 -o strace.log python
Python 3.7.4 (default, Oct 12 2019, 18:55:28)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()

(k8s) $ cat strace.log | head -n 10
execve("/home/alixedi/k8s/bin/python", ["python"], 0x7ffee2a890b0 /* 24 vars */) = 0
brk(NULL)                               = 0xc01000
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=17010, ...}) = 0
mmap(NULL, 17010, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f8719d60000
close(3)                                = 0
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
```

So while the Python virtual environment provides nice isolation within the Python universe, it is still relies on being able to make a bunch of calls to operating system libraries (syscalls) that are not bundled inside the virtual environment.

Not quite a sandbox then is it? What if those junior devs are sporting the trendy surface machines running MS Windows?

### Hello Containers

This is where containers come in.

Containers provide a sandbox for your process to run in. This sandbox is to Python virtual environment what Messi is to your Sunday league playmaker or for those of you who aren't into football (why?) what Beyonce is to Britney Spears.

Specifically:

- Containers provides file system isolation. A process running in a container cannot access the file system outside of the container.
- Containers provide memory and CPU usage isolation. A process running in a container can only access the memory and CPU that has been assigned to it.
- Container provide namespace isolation i.e. network, process IDs, hostnames, users etc.
- Containers provide security. A process running in a container can only do what it has been permitted to do.

Finally, Docker is a type of a container. The most popular one no less. It also comes with a bunch of nice-to-haves which makes it easy for beginners.

Enough talk. Lets create our first container. Who is excited?  ✋

The first thing we need to do is to write the Docker equivalent of our requirements.txt file i.e. a file that lay out what would go into our container. Standard naming convention dictates that we call this file Dockerfile.

A very basic Dockerfile for our application would look like the following:

```docker
# Every docker container has a base image (More on images in the following paras).
# It is specified using the FROM keyword on the first line of the Dockerfile.
# Python.org conveniently publishes a bunch of base images that we can use to run Python applications.
# We are using the python base image with the tag `alpine`.
# This would give us a Python environment running on Alpine Linux - a light-weight distribution that is popular in the container world.
FROM python:alpine

# This copies our files to the root of our container.
COPY hello.py requirements.txt /

# This is pretty standard pip and we have already covered it.
# The only interesting thing here is that we are choosing not to use venv.
# We totally can but it will be like running an environment inside a more awesome environment so no need.
RUN pip install -r requirements.txt

```

The attentive reader might ask:

Hang on a minute, we are moving straight to requirements.txt

What happened to being able to create a virtual environment by running:

```bash
$ python -m venv ~/.venvs/k8s
```

Followed by activating the virtual environment and installing a bunch of packages by:

```bash
$ source ~/.venv/k8s/bin/activate
(k8s) $ pip install flask
```

To which, the clever 🙇 writer would say:

1. Good question.
2. Python venv as the analogy for Docker died as soon as we moved from the What (isolation) to the How (API).

![](assets/images/hello-docker-world/Untitled.png)

Docker has its own opinions on sandboxes, how they should be built and how processes should be run inside them.

Some of these opinions are informed by the difference in nature of a docker sandbox to a Python venv sandbox.

The clever writer would then move on swiftly to Docker concepts and hope that the analogy with Python venv has caused more good than harm.

Back to Dockerfiles. We have one. What do we do with it?

Without any obvious exceptions, the most awesome thing you could do with a Dockerfile is to use it to produce a Docker image.

What is a Docker image?

It is a tarball that contains all the dependencies needed to run your application.

The act of building a Docker image, among other things, downloads these dependencies from the inter webs onto your machine.

How do you build a docker image?

Simple. Like so:

```bash
$ docker build .

Sending build context to Docker daemon  5.632kB

Step 1/3 : FROM python:alpine
alpine: Pulling from library/python
df20fa9351a1: Pull complete
36b3adc4ff6f: Pull complete
3e7ef1bb9eba: Pull complete
78538f72d6a9: Pull complete
c9fdb169601a: Pull complete
Digest: sha256:1edaccf11f061da18842e3cb7bb14d9f7336b6b2a24248219ab5c363b8454336
Status: Downloaded newer image for python:alpine
 ---> 872c3118ec53

Step 2/3 : COPY hello.py requirements.txt /
 ---> 70bd00cce758

Step 3/3 : RUN pip install -r requirements.txt
 ---> Running in 9527747772b7
Collecting click==7.1.2
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting Flask==1.1.2
  Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting itsdangerous==1.1.0
  Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Jinja2==2.11.2
  Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
Collecting MarkupSafe==1.1.1
  Downloading MarkupSafe-1.1.1.tar.gz (19 kB)
Collecting Werkzeug==1.0.1
  Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Building wheels for collected packages: MarkupSafe
  Building wheel for MarkupSafe (setup.py): started
  Building wheel for MarkupSafe (setup.py): finished with status 'done'
  Created wheel for MarkupSafe: filename=MarkupSafe-1.1.1-py3-none-any.whl size=12629 sha256=7020159b31f20b65caec66087f40ff4a4e235219689d8235bbbc8b5187ef717d
  Stored in directory: /root/.cache/pip/wheels/0c/61/d6/4db4f4c28254856e82305fdb1f752ed7f8482e54c384d8cb0e
Successfully built MarkupSafe
Installing collected packages: click, Werkzeug, MarkupSafe, Jinja2, itsdangerous, Flask
Successfully installed Flask-1.1.2 Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 itsdangerous-1.1.0

Removing intermediate container 9527747772b7
 ---> 1ddb10e93851

Successfully built 1ddb10e93851
```

I have put new lines in the snippet above to distinguish the various steps that were needed for building our docker image.

An attentive reader would notice that the steps correspond to the lines in the Dockerfile. Well done attentive reader. Hold that thought. We will revisit this pretty soon.

Back to the image. We just built one. Where is it though?

```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              1ddb10e93851        4 minutes ago       53.4MB
python              alpine              872c3118ec53        2 days ago          42.7MB
```

Hmm. That is not very helpful.

The python image sort of makes sense. I specified it as a base image in my Dockerfile. I presume when I built my image, it got downloaded.

But what about MY image? It doesn't seem to have a REPOSITORY (seems like a name) or a TAG. And what is even a tag anyway?

Lets answer these questions by running the following bit of command-line:

```bash
$ docker image tag 1ddb10e93851 hello:v1
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello               v1                  1ddb10e93851        11 minutes ago      53.4MB
python              alpine              872c3118ec53        2 days ago          42.7MB
```

Much better.

Except next time, we could bundle up the naming and tagging in the build command itself:

```bash
$ docker build . --tag hello:v1
```

Now that we know HOW to name and tag our images, its probably useful to understand WHY.

One popular WHY is versions. Learn to take a hint? hello:v1  😉

Imagine a world where every time you release a new version of your app, you build an image and push it to an image-store of sorts.

You would need someway to differentiate hello 1.0 with hello 2.0.

One way to do it would be to name the images hello1 and hello2 respectively.

A better way would be to name the images hello and tag them v1 and v2 respectively.

In docker world, you would refer to these as hello:v1 and hello:v2.

You can also assign multiple tags to an image.

For instance, imagine you test your application in a staging environment before promoting it to production. In this case, it is common to tag the image as staging when it is published. Once you are happy that the thing works, you can assign a production tag to it.

P.S. Assigning staging and production tags wouldn't automatically deploy your application to staging and production environment respectively. There is a missing piece here. We will come back to it when we talk about Kubernetes.

I started on this spiel of names and tags; Conveniently ignoring a small but important detail: There is no name. Its actually repository. Its time we smooth this out.

Now that we know how to build an image, its time to revisit why we started on this path in the first place. We wanted some way to distribute our application in a reproducible way.

Building an images is a strong start but that doesn't quite solve the distribute bit. This is where repositories come in. A repository is a central store for your images. There are several options but for the purpose of learning about repositories, we would run with dockerhub.

Go make an account at Dockerhub. While you are at it, also create a new repository. You can call it hello.

Done? Cool. We can now do the following:

```bash
$ docker image tag hello:v1 <dockerhub-username>/hello:v1
$ docker push alixedi/hello:v1
The push refers to repository [docker.io/alixedi/hello]
b36cb4db8a04: Pushing [=============>                                     ]   2.84MB/10.76MB
fa9b430b6d13: Pushing [==================================================>]  3.072kB
2e628e2d9dc4: Pushing [==================>                                ]  2.693MB/7.236MB
26e08b3268b4: Pushing [==================================================>]  4.608kB
adf6e7b1c68f: Pushing [======>                                            ]  3.643MB/29.33MB
408e53c5e3b2: Waiting
50644c29ef5a: Waiting
```

This will push the hello:v1 image to dockerhub.

The CI script that deploys your application to production could then do the following:

```bash
$ docker pull alixedi/hello:v1
```

With a sensible combination of repositories, tags, dockerhub, push and pull, you have just sorted the distribution of your app.

Phew.

But also I realise that we haven't actually run the damned thing yet!

We could run it now but I am inclined to shamelessly double down on the BS and introduce one more concept before that.

This one has been there all along. Looming in the shadows. I have been  trying to hold off explaining it. Until now. I am left with no choice. Sorry.

Each instruction in a Dockerfile produces a layer. This layer is a diff of changes in the filesystem from the previous layer. A docker image is a stack of these layers.

One more thing: All the commands produce layers but except for FROM, COPY and RUN, the layers are intermediate. Intermediate layers are squashed in the resulting image.

Finally, how can I inspect these layers? Lets do that now. Break the COPY statement in your Dockerfile:

```bash
FROM python:alpine
COPY hello.py /
COPY requirements.txt /
RUN pip install -r requirements.txt
```

Build a new version of the image:

```bash
$ docker build . hello:v2
```

In order to inspect the layers:

```bash
$ docker history hello:v2
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
5433ece6bdd7        9 minutes ago       /bin/sh -c pip install -r requirements.txt      10.8MB
a320b983dea1        9 minutes ago       /bin/sh -c #(nop) COPY file:11d578baaa9f1fd5…   95B
57d793585c4c        9 minutes ago       /bin/sh -c #(nop) COPY file:35f7847638831fbf…   106B
872c3118ec53        2 days ago          /bin/sh -c #(nop)  CMD ["python3"]              0B
<missing>           2 days ago          /bin/sh -c set -ex;   wget -O get-pip.py "$P…   7.24MB
..
```

And compare the layers with those of hello:v1

```bash
$ colordiff <(docker history hello:v1) <(docker history hello:v2)
2,3c2,4
< 1ddb10e93851        3 hours ago         /bin/sh -c pip install -r requirements.txt      10.8MB
< 70bd00cce758        3 hours ago         /bin/sh -c #(nop) COPY multi:63205105974020a…   201B
---
> 5433ece6bdd7        11 minutes ago      /bin/sh -c pip install -r requirements.txt      10.8MB
> a320b983dea1        11 minutes ago      /bin/sh -c #(nop) COPY file:11d578baaa9f1fd5…   95B
> 57d793585c4c        11 minutes ago      /bin/sh -c #(nop) COPY file:35f7847638831fbf…   106B
```

Finally, all these layers are not for nothing. Each layer can be re-used by an unlimited number of images. Also, when you are building a new image, Docker is smart enough to only download layers that are not present in the local file system.

Alright, I am now satisfied that we have touched most of the bits in docker that matter.

Time to run that fucking image.

First thing you could do is to run your container with a shell and faff about:

```bash
$ docker run --interactive --tty hello:v1 sh
```

I would also invite you at this point to summon the help and find out what —interactive and —tty means:

```bash
$ docker run --help
```

Nice innit? You would be delighted to find out that this help is not limited to docker run.

```bash
$ docker --help
$ doker build --help
$ docker image --help
$ etc.
zsh: command not found: etc.
```

😐

Back to docker run. Lets try and faff about as promised:

```bash
$ docker run -it hello:v1 sh
# ls -l -Sr
total 68
dr-xr-xr-x   12 root     root             0 Aug  7 13:16 sys
dr-xr-xr-x  144 root     root             0 Aug  7 13:16 proc
-rw-r--r--    1 root     root            95 Aug  7 09:30 requirements.txt
-rw-r--r--    1 root     root           106 Jul 10 10:14 hello.py
..
```

I see them files and I cannot resist:

```bash
# FLASK_APP=hello.py flask run &
 * Serving Flask app "hello.py"
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

# python
Python 3.8.5 (default, Aug  4 2020, 04:11:56)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import urllib.request
>>> urllib.request.urlopen('http://127.0.0.1:5000').read()
127.0.0.1 - - [07/Aug/2020 13:22:43] "GET / HTTP/1.1" 200 -
b'Hello World!\n'
```

There it is 😅

Now we just want to lift up whatever we did in that container to get our little app running. Here is a decent first go:

```bash
$ docker run hello:v1 sh -c "FLASK_APP=hello.py flask run"
 * Serving Flask app "hello.py"
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Now wouldn't it be fun if we can get that beautiful Hello World back? I am one for trying:

```bash
$ curl localhost:5000
curl: (7) Failed to connect to localhost port 5000: Connection refused
```

There are 2 bits missing here I suspect:

1. The host should not be able to access the [localhost](http://localhost) for a container. This can be easily fixed by running our app on 0.0.0.0
2. We need some way to forward a port from our host to the container.

Lets see if you can find out how to map ports from the host to the container?

```bash
$ docker run --help | grep port
      --expose list                    Expose a port or a range of ports
      --health-retries int             Consecutive failures needed to report unhealthy
  -p, --publish list                   Publish a container's port(s) to the host
  -P, --publish-all                    Publish all exposed ports to random ports
```

Looks promising. Lets try the publish bit:

```bash
$ docker run -p 5000:5000 hello:v1 sh -c "FLASK_APP=hello.py flask run -h 0.0.0.0"
```

Moment of truth 🤞

```bash
$ curl localhost:5000
Hello World!
```

![](assets/images/hello-docker-world/Untitled%201.png)

Now then 🚀

I am taking it as a win but lets be honest. This is a bit of a mouthful:

```bash
$ docker run -p 5000:5000 hello:v1 sh -c "FLASK_APP=hello.py flask run -h 0.0.0.0"
```

I wonder if we could do something about it?

Turns out we could. Remember that old Dockerfile? Yup. You can totally move a bunch of things in this tedious command line into the Dockerfile.

For starters, you could set environment variables. In addition, you could also specify the command to run when a container is spawned.

Here is how:

```bash
FROM python:alpine
COPY hello.py requirements.txt /
RUN pip install -r requirements.txt
ENV FLASK_APP=/hello.py
CMD ["flask", "run", "-h", "0.0.0.0"]
```

Lets build and run this baby:

```bash
$ docker build . hello:v3
$ docker run -p 5000:5000 hello:v3
```

And:

```bash
$ curl localhost:5000
Hello World!
```

![](assets/images/hello-docker-world/Untitled%202.png)

I hope this was fun.

We started with a little Hello World application in Python, introduced Python's virtual environment to make our application **reproducible** and **distributable** (I am actually surprised this is a word).

We then ventured into containers, specifically Docker. We touched upon docker images and how to build them. Finally, we talked about how to run our application inside docker containers.

Using a Hello World application was a bit of a necessity because we wanted complete attention on the container and not what was running inside it. I think we managed to do that but we do not intend to keep at it.

## Hello Application

In the previous chapter we introduced Flask and Docker (containers). Although it might be very interresting if you aren't familiar with it, the end result was a bit boring. Hello World is something you usually learn in the first 5 minutes of a programming tutorial. To make things a bit more interresting we say good bye to Hello World examples! Instead of showing some very fabricated standard examples, we will be building a real application. And like real developers 😉, we will be building up the application bit by bit.

We are building an interactive Python web console. It's basically a webpage where users can run python without installing anything. There exists plenty of examples which do this: [Jupyterhub](https://jupyter.org/try), [Kaggle](https://www.kaggle.com/), [Google Colab](https://colab.research.google.com/), or even [Python's homepage](https://www.python.org/). Jupyterhub is also open source and you can run it locally. It looks like this:

![](assets/images/hello-application/Screenshot_2020-08-14_at_07.39.40.png)

It might sounds complicated, but Python wouldn't be Python if it wouldn't expose everything it can do to developers! It is actually very easy. A minimal example:

```python
from code import InteractiveConsole
console = InteractiveConsole()

inp = True
while inp:
    inp = input('>>> ')
    console.runcode(inp)
```

Which behaves like a very basic python command line:

```python
>>> print('Hello World')
Hello World
>>> a = 1 + 2
>>> print(a)
3
```

We can easily combine this with our Docker hello world example and we have a (multi-user) interactive web console. The following little mini application can actually build with the same docker file from the previous chapter:

```python
import code
import, ioimport, contextlibimport

flaskapp = flask.Flask(__name__)

app.consoles = {}

class WebConsole:

	def __init__(self):
		self.console = code.InteractiveConsole()

	def run(self, code):
		output = io.StringIO()
		with contextlib.redirect_stdout(output):
			with contextlib.redirect_stderr(output):
				for line in code.splitlines():
					self.console.push(line)
					return {'output': str(output.getvalue())}

@app.route('/api/<uname>/run/', methods=['POST'])
def run(uname):
	if not uname in app.consoles:
		app.consoles[uname] = WebConsole()
		return flask.jsonify(
			app.consoles[uname].run(
				flask.request.get_json()['input']
			)
		)
```

Ok, you got me there. I was lying, this is not a full web app. We won't actually build the front end, just the JSON api which would power it. A little demonstration on how to use it from a python script (pip install a handy package called `requests` first).

```python
import requests
print(requests.post(
	'http://localhost:5000/api/ali/run/',
	json={'input': 'print("Hello World")'}
).json())
```

Of course this is far too simple. As always with development, having a proof of concept, is nothing compared to actually creating something you can run on production. Not to mention: you are allowing anyone to run any code on your servers! I'm sure that if you leave this running for a day, your application pissed of a lot of all of your users, and someone managed to get access to your server.

![](assets/images/hello-application/1_AjjSTJG6cqaMcBUSROPw0Q.jpeg)

As this book is about Kubernetes we will address most of these issue with Kubernetes. We will introduce you to everything you need to run most applications on Kubernetes, and even use some of it's advanced features.

## Hello Kubernetes World

When I started writing this in my head, I decided that I will not go into too much details about the why of Kubernetes.

You - the reader - are reading this book so it is a fair assumption on my part that you have figured out your whys, and they are all lined up like:  🦆 🦆 🦆

On the other hand, having just written the chapter on Docker, half of which - to be honest - was expanding on why, I feel uncomfortable in stopping short of putting down something on the why of Kubernetes.

I feel that my main job, as an author, is to get the readers excited about something because lets face it: Excitement leads to motivation. Motivation leads to action. Action lead to Stack Overflow. which does a far better job of solving any specific issues that you might run into during the course of your actions.

There are two possible whys of Kubernetes.

### Big Corp Kubernetes

You work at a company that has implemented some kind of microservices architecture. Possibly,  promulgating an engineering culture where the respective teams oversee particular features of the broader application from conception, design, development, all the way into production.

You are a junior developers hired because you traversed that f**king binary tree on the whiteboard in 5 minutes of sharpie-ballet. Well done for the gumption to read CTCI. Twice. Now that you are in, you want to get cracking.

Your CTO - in his/her infinite wisdom - have chosen to use Kubernetes to orchestrate all those microservices.

Orchestrate is a word that is used often to describe Kubernetes. Lets nail down what that means before we move on with the rest of our story.

![](assets/images/hello-kubernetes-world/Untitled.png)

Orchestration in the context of Big Corp running a microservices architecture means 3 main things:

#### Service Discovery

Containers are meant to be ephemeral. Like cattle and not like pets.

A set of containers that are running a particular microservice need a PO box - A layer of abstraction over the (IP) addresses of individual containers.

The abstraction would mean that the containers could ephemeral all they like and the rest of the cluster wouldn't care.

This abstraction is called Service Discovery. Kubernetes provides it out of the box.

#### Load Balancing

So Big Corp has launched this awesome new product. They marketed it till the cows came home and now its time to launch.

What do you think would happen?

I would reckon a bunch of people would pop in because of the marketing until they find out that the awesome new product is shit.

Big Corp know this too.

But even with the shitty product, they would not want the embarrassment of being brought down by a TechCrunch article.

![](assets/images/hello-kubernetes-world/Untitled%201.png)

I mean the tweets write themselves  🤷‍♂️

Kubernetes has your back. Sort of. It will happily distribute the traffic to ensure a stable deployment. But if you want to scale the cluster (you might), that is between you and your cloud provider of choice.

When you do choose to scale your cluster, Kubernetes will automatically create new containers on the new nodes and divert traffic to them.

You can also specify the amount of CPU and RAM each container needs and Kubernetes would be happy to take that into account while bin-packing.

Finally, Kubernetes takes care of the container health. It replaces the ones that fail a user-defined health check, taking care of not announcing them until they are ready etc.

#### Automated rollouts and rollbacks

Finally, hopefully, someone would realize that the first version of awesome product was shit. At which point, they will iron out some of the bugs, rework some features etc. and try to push out a new release.

I have worked at companies where a release was like a ceremony. Someone would actually set out to do it and 3 days later, everyone will get a slice of cake.

The advent of DevOps have meant many things to many people but for me, it means no cake. The releases are no longer like Christmas and more like Wednesdays.

There is nothing exciting about it. Its just a day that comes around every week.

In some companies releases are more like coffee breaks  🤷‍♂️

From my experience in such companies, it was often Kubernetes that made this happen.

It comes out of the box with the tools you need to rollout releases - and in case a release doesn't work, roll it back.

### Startup Kubernetes

You work at a startup that has implemented a microservices architecture... 😂

Sorry. I was kidding. Please don't.

How about you work at a startup that is trying to find a product-market fit by deploying e.g. that SaaS application on a Linode box worth $30/month.

Why would you want to use Kubernetes?

Funny enough, I first came upon Kubernetes at such a startup. Our problem - like every other startup was optimizing the infrastructure costs to try and get the maximum bang our buck.

This lead us towards services.

Not because we had a million teams and services was the only way to stop them from treading on toes

Not because of resume-driven development.

![](assets/images/hello-kubernetes-world/Untitled%202.png)

We split our API into 2 services because we had endpoints with drastic variance in load characteristics. The only way to utilize our infrastructure efficiently was to put these endpoints on different nodes.

On top of that the demand for our service had huge variances. We wanted to be able to scale up when it was time to make money and scale down when we didn't have active customers.

Our cloud provider tried to sell us proprietary options but we didn't want a lock-in. We were on startup credits. As soon as the credits ran out, there was a possibility that we would move shop for cost efficiency.

Finally, we were 2 engineers in total. We wanted all the good things - docker for reproducible and distributable artifacts, CI/CD and a high release cadence without locking down 50% of our engineering resources.

Kubernetes helped us do all of that and it can help you too.

Lets run our thing on Kubernetes 🚀

### Setup

In order to start on our adventure into the world of Kubernetes, we are going to install the awesome Minikube.

Minikube will let you fiddle away at that Kubernetes cluster without having to pull out your wallet and spend your hard-earned AWS credits.

Minikube runs a kubernetes cluster inside a VM. On your machine.

Installing Minikube is about following [this excellent guide](https://minikube.sigs.k8s.io/docs/start/).

I went with:

```bash
$ brew install minikube
```

Following this, it might be prudent to point your docker cli to the docker daemon that is running inside the VM. Instead of the one that is running on your machine, outside the VM.

```bash
$ eval $(minikube -p minikube docker-env)
```

Finally, some of the stuff we are about to do would be less of a mouthful if you can do the following:

```bash
$ alias minikube kubectl --=kubectl
```

You are welcome! Lets get started.

#### kubectl

Hopefully, you would have noticed by now that the underlying principle of this book is "Show me or it didn't happen".

In keeping with this principle, we would like to fiddle with Kubernetes. kubectl - the CLI tool for Kubernetes lets us do just that.

For starters, we should just type kubectl in our terminal and see what that does:

```bash
$ kubectl
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/

Basic Commands (Beginner):
  create         Create a resource from a file or from stdin.
  expose         Take a replication controller, service, deployment or pod and expose it as a new Kubernetes Service
  run            Run a particular image on the cluster
..
```

Lots of interesting things under the ellipses but honestly, do we really feel like reading beyond **run**?

```bash
$ kubectl run
Error: required flag(s) "image" not set

Examples:
  # Start a single instance of nginx.
  kubectl run nginx --image=nginx
..
```

Absolutely fucking beautiful! 😍

I love a CLI tool that goes out of its way to be helpful. kubectl has made a very good start. Not only is it telling me what I am missing but it goes one step further and provides me examples.

In the last chapter, we learned how to build an image. I would propose that you build one for our application right now.

We are about to feed that image into kubectl:

```bash
$ kubectl run webconsole --image pyconuk-2018-k8s:step2
deployment.apps/webconsole created

$ woOt!
zsh: command not found: woOt!
```

Hmm, so we have ~~something~~ the promise of something called a deployment. We will come to it later.

Right now, it seems that we have succeeded at *something.*

It also seems that this *something* is called deployment.apps/webconsole.

It may be interesting to step back to kubectl and find out if it would help us explore the size and shape of what we have just done here.

```bash
$ kubectl
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/

Basic Commands (Beginner):
  create         Create a resource from a file or from stdin.
  expose         Take a replication controller, service, deployment or pod and expose it as a new Kubernetes Service
  run            Run a particular image on the cluster
  set            Set specific features on objects

Basic Commands (Intermediate):
  explain        Documentation of resources
  get            Display one or many resources
..
```

The second block of Basic Commands sounds promising but more importantly, **Intermediate** already ****(!) LOL.

Explain seems to suggest documentation of some kind. Lets ask it about deployments shall we?

```bash
$ kubectl explain deployment
KIND:     Deployment
VERSION:  apps/v1

DESCRIPTION:
     Deployment enables declarative updates for Pods and ReplicaSets.
..

$ in plain english please
zsh: command not found: in
```

I will step in at this point.

Deployments in the Kubernetes universe is the layer that runs multiple replicas of your application. It is the thing that you can scale up or down. The thing that ensures that when an instance of your application goes down, it is replaced with a healthy instance.

With that out of the way, the output of our kubectl explain deployment mentions 2 other things: Pods and ReplicaSets. Lets see if kubectl does a better job of explaining that these are:

```bash
$ kubectl explain pods
KIND:     Pod
VERSION:  v1

DESCRIPTION:
     Pod is a collection of containers that can run on a host. This resource is
     created by clients and scheduled onto hosts.
```

Not bad but perhaps I can expand on this with an example.

Often, an instance of application comprises of 2 or more containers. For instance, I recently built an app that needed to send some metrics to a Prometheus server. To cut a long story short, in order to do this, I needed to pair each container running my app with one [running StatsD exporter](https://github.com/prometheus/statsd_exporter#using-docker).

**Pods** are the smallest deployable object in Kubernetes. A Pod can contain multiple containers. Kubernetes ensures that all the containers in a Pod are run on the same host, managed as a single entity and be able to share resources such as network and storage.

Lets look at ReplicaSet:

```bash
$ kubectl explain ReplicaSet
KIND:     ReplicaSet
VERSION:  apps/v1

DESCRIPTION:
     ReplicaSet ensures that a specified number of pod replicas are running at
     any given time.
```

**tl;dr** ReplicaSet sits between a Deployment and its Pods. ReplicaSet is how a deployment guarantee that the availability of specified number of application instances.

As a user, we will generally deal with Deployments and Pods instead of ReplicaSets.

We are now in a position to make **some** (but not complete) sense of this:

```bash
$ kubectl explain deployment
KIND:     Deployment
VERSION:  apps/v1

DESCRIPTION:
     Deployment enables declarative updates for Pods and ReplicaSets.
..
```

Some sense is enough for now. Lets move on to the next interesting bit in our kubectl tour:

```bash
$ kubectl get
You must specify the type of resource to get. Use "kubectl api-resources" for a complete list of supported resources.

$ kubectl api-resources
NAME                              SHORTNAMES   APIGROUP                       NAMESPACED   KIND
bindings                                                                      true         Binding
componentstatuses                 cs                                          false        ComponentStatus
..

$ hmm
zsh: command not found: hmm

$ kubectl api-resources | grep deployment
deployments                       deploy       apps                           true         Deployment

$ yup
zsh: command not found: yup

$ kubectl get deployment
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
webconsole   1/1     1            1           37m

$ kubectl get pod
NAME                          READY   STATUS    RESTARTS   AGE
webconsole-5b559bf485-6dnv9   1/1     Running   0          42m

$ kubectl get ReplicaSet
NAME                    DESIRED   CURRENT   READY   AGE
webconsole-5b559bf485   1         1         1       42m
```

How cool is that?!

We just ran our thing on a cluster and now we are querying the cluster and its telling us the nuts and bolts of how its running our thing.

So we now know that we have a Deployment running on a cluster with a ReplicaSet and a Pod. We kinda know what these terms mean. At least from a utilitarian perspective.

Perhaps its time to dive back into the kubectl 🧰 and see what else we have at our hand 🙂

```bash
$ kubectl
..
Basic Commands (Intermediate):
  explain        Documentation of resources
  get            Display one or many resources
  edit           Edit a resource on the server
  delete         Delete resources by filenames, stdin, resources and names, or by resources and
label selector
```

Delete is always interesting. If we are successful in deleting the stuff that we created, it will provided us with the opportunity to create it again. If we are successful a second time, it would mean we have something on our hands that is reproducible.

```bash
$ kubectl delete deployment webconsole
deployment.apps "webconsole" deleted

$ kubectl get deployment
No resources found in default namespace.

$ kubectl get pods
No resources found in default namespace.
```

🙌

And now again:

```bash
$ kubectl run webconsole --image pyconuk-2018-k8s:step2
deployment.apps/webconsole created

$ kubectl get deployment
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
webconsole   1/1     1            1           9s

$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
webconsole-5b559bf485-rtsk5   1/1     Running   0          5s
```

We have something that is reproducible and not a ❄️

There was another thing that caught my eye in the kubectl help:

```bash
$ kubectl
..
Deploy Commands:
  rollout        Manage the rollout of a resource
  scale          Set a new size for a Deployment, ReplicaSet, Replication Controller, or Job
  autoscale      Auto-scale a Deployment, ReplicaSet, or ReplicationController
```

This is like the 3 most exciting things in Kubernetes. Lets start by exploring scale.

```bash
$ kubectl scale
Error: required flag(s) "replicas" not set

Examples:
  # Scale a replicaset named 'foo' to 3.
  kubectl scale --replicas=3 rs/foo

  # Scale a resource identified by type and name specified in "foo.yaml" to 3.
  kubectl scale --replicas=3 -f foo.yaml

  # If the deployment named mysql's current size is 2, scale mysql to 3.
  kubectl scale --current-replicas=2 --replicas=3 deployment/mysql
```

I think I have a idea on how to do example #3 for our thing.

I don't know about you but I ❤️the examples. Not enough CLI tools have them IMO.

```bash
$ kubectl scale --current-replicas=1 --replicas=4 deployment webconsole
deployment.apps/webconsole scaled

$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
webconsole-5b559bf485-2zkt5   1/1     Running   0          4s
webconsole-5b559bf485-6bm5j   1/1     Running   0          4s
webconsole-5b559bf485-fvb6c   1/1     Running   0          4s
webconsole-5b559bf485-rtsk5   1/1     Running   0          8m35s

$ whoa webscale lol
zsh: command not found: whoa

$ kubectl scale --current-replicas=4 --replicas=1 deployment webconsole
deployment.apps/webconsole scaled

$ kubectl get pods
NAME                          READY   STATUS        RESTARTS   AGE
webconsole-5b559bf485-2zkt5   0/1     Terminating   0          117s
webconsole-5b559bf485-6bm5j   0/1     Terminating   0          117s
webconsole-5b559bf485-fvb6c   0/1     Terminating   0          117s
webconsole-5b559bf485-rtsk5   1/1     Running       0          10m

$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
webconsole-5b559bf485-rtsk5   1/1     Running   0          10m
```

This is an actual picture of me from 2 years ago:

![](assets/images/hello-kubernetes-world/Untitled%203.png)

Bring on the hordes TechCrunch.

Except, hold on.

We still haven't figured out how to talk to our thing.

You know - try and run arbitrary Python code for ourselves? Before we start running arbitrary Python code for millions of users 🤑

Lets step back and take stock for what we have right now.

We have a cluster. Sort of. We have Minikube. Its running a VM on our machine essentially. Inside that VM is a Kubernetes cluster.

We have - by now - figured out:

How to deploy our application to a Kubernetes cluster.

We have also managed to figure out how to scale our application.

If only we could **expose** our application to the universe outside the cluster.

```bash
$ kubectl | grep expose
  expose         Take a replication controller, service, deployment or pod and expose it as a new Kubernetes Service
```

Don't you ❤️ it when the API is this good? I do.

```bash
$ kubectl expose
error: You must provide one or more resources by argument or filename.
Example resource specifications include:
   '-f rsrc.yaml'
   '--filename=rsrc.json'
   '<resource> <name>'
   '<resource>'
See 'kubectl expose -h' for help and examples

$ kubectl expose -h
Expose a resource as a new Kubernetes service.

 Looks up a deployment, service, replica set, replication controller or pod by name and uses the
selector for that resource as the selector for a new service on the specified port. A deployment or
replica set will be exposed as a service only if its selector is convertible to a selector that
service supports, i.e. when the selector contains only the matchLabels component. Note that if no
port is specified via --port and the exposed resource has multiple ports, all will be re-used by the
new service. Also if no labels are specified, the new service will re-use the labels from the
resource it exposes.

 Possible resources include (case insensitive):

 pod (po), service (svc), replicationcontroller (rc), deployment (deploy), replicaset (rs)

Examples:
  # Create a service for a replicated nginx, which serves on port 80 and connects to the containers
on port 8000.
  kubectl expose rc nginx --port=80 --target-port=8000
..
```

Service selector service selector label resource blah blah blah blah..

Lets break this down shall we?

```bash
$ kubectl explain service
KIND:     Service
VERSION:  v1

DESCRIPTION:
     Service is a named abstraction of software service (for example, mysql)
     consisting of local port (for example 3306) that the proxy listens on, and
     the selector that determines which pods will answer requests sent through
     the proxy.
```

This is more like it. It seems like a Service is an abstraction over a Deployment that handles the comms between pods in a deployment and the rest of the world.

Sounds simple. Except for the **selector -** The bit that links a service to the pods.

Lets use another kubectl subcommand to help us out here:

```bash
$ kubectl describe deployment webconsole
Name:                   webconsole
Namespace:              default
CreationTimestamp:      Fri, 28 Aug 2020 09:02:22 +0100
Labels:                 run=webconsole
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               run=webconsole
..
```

It seems our deployment has something called a selector.

```bash
$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
webconsole-5b559bf485-rtsk5   1/1     Running   0          34m

$ kubectl describe pods webconsole-5b559bf485-rtsk5
Name:         webconsole-5b559bf485-rtsk5
Namespace:    default
Priority:     0
Node:         minikube/192.168.64.2
Start Time:   Fri, 28 Aug 2020 09:02:22 +0100
Labels:       pod-template-hash=5b559bf485
              run=webconsole
```

And our pod have a label that matches the selector.

Let me explain. Its all quite simple really.

A Label is a key-value pairs that can be attached to any Kubernetes resource.

A Selector is a string that selects a set of resources in a Kubernetes cluster based on their labels.

Simple enough? Good.

Back to the bit where we were trying to expose our application running inside a Kubernetes cluster to the internet.

Lets refer to the help and pay close attention to the Usage:

```bash
$ kubectl expose -h
..
Usage:
  kubectl expose (-f FILENAME | TYPE NAME) [--port=port] [--protocol=TCP|UDP|SCTP]
[--target-port=number-or-name] [--name=name] [--external-ip=external-ip-of-service] [--type=type]
[options]
```

You will notice the switch that specifies the service type.

This needs a bit of an explainer. As we established earlier, a service is the abstraction that exposes a deployment to the rest of the world.

"Rest of the world" could mean different things depending on the situation at hand though.

For instance, you might be running a Web application as well as a Redis cache inside your Kubernetes cluster.

"Rest of the world" for your web application would mean the internet.

On the other hand, "Rest of the world" for the Redis cache should mean rest of the cluster. There is no reason to expose your Redis cache to the internet right?

As it turn out, theses are the 2 types of services in Kubernetes that you should be aware of at this instant in time:

1. **ClusterIP**: Exposes a Service inside the cluster.
2. **LoadBalancer:** Exposes the Service outside the cluster.

The attentive reader might ask at this point: "Why do we need a service for exposing our application inside the cluster?".

Good question.

See, while you can access your application from inside the cluster (we haven't quite got around to this yet but trust me), it will inevitably involve referring to resources (e.g. Pods) that are ephemeral.

A service on the other hand provides a stable DNS that points to the right ephemeral resource so you don't have to.

Back to service types. It seems we are looking for 2 at this moment.

```bash
$ kubectl expose deployments/webconsole --port=5000 --type=LoadBalancer
service/webconsole exposed
```

We should now - by all accounts - have a way of pointing to our application from outside the cluster.

There is one more step though.

Remember our setup? We are running Minikube - which runs a Kubernetes cluster on our machine. Inside a VM.

We have figured out a way to expose our service to the world outside the cluster but that world is just a VM.

Here is the final step. I promise. This is only needed for Minikube. It bridges the service that has now been exposed to the Minikube VM with your localhost:

```bash
$ minikube service webconsole

|-----------|------------|-------------|---------------------------|
| NAMESPACE |    NAME    | TARGET PORT |            URL            |
|-----------|------------|-------------|---------------------------|
| default   | webconsole |        5000 | http://192.168.64.2:31075 |
|-----------|------------|-------------|---------------------------|

🎉  Opening service default/webconsole in default browser...
```

We are in business it seems.

```python
>>> import requests
>>> requests.post('http://192.168.64.2:31075/api/ali/run', json={'input': '5+5'}).json()
{'output': '10\n'}
>>> Fucking awesome!
File "<stdin>", line 1
    Fucking awesome
            ^
SyntaxError: invalid syntax
```

**No MP4 SUPPORT?**

Hold on to your 🏇though.

We should try one more trick at this point.

```python
$ kubectl scale --replicas=4 deployment webconsole
deployment.apps/webconsole scaled
$ python
Python 3.8.5 (default, Aug 24 2020, 07:14:09)
[Clang 11.0.3 (clang-1103.0.32.62)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> requests.post('http://192.168.64.2:31075/api/ali/run', json={'input': '5+5'}).json()
{'output': '10\n'}
```

**No GIF SUPPORT?**

I have one last trick left up my sleeve. Might as well:

```bash
$ python
Python 3.8.5 (default, Aug 24 2020, 07:14:09)
[Clang 11.0.3 (clang-1103.0.32.62)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> requests.get('http://192.168.64.2:31075/api/crash')
<Response [500]>
```

Yes. We left a little endpoint in our application for the [chaos monkey](https://en.wikipedia.org/wiki/Chaos_engineering):

```python
@app.route('/api/crash/', methods=['GET'])
def crash():
    shutdown_server()
```

As soon as a pod crashes, Kubernetes restarts it. I know. "Show me or it didn't happen". Here you go:

```python
$ kubectl get pods --watch
NAME                          READY   STATUS             RESTARTS   AGE
webconsole-5b559bf485-q5rgq   1/1     Running            1          7d2h
webconsole-5b559bf485-rtsk5   1/1     Running            1          7d3h
webconsole-5b559bf485-v9zsx   1/1     Running            1          7d2h
webconsole-5b559bf485-vjrw8   1/1     Running            1          7d2h

# Here is when we hit /crash
webconsole-5b559bf485-q5rgq   0/1     Completed          1          7d2h
webconsole-5b559bf485-q5rgq   0/1     CrashLoopBackOff   1          7d2h
webconsole-5b559bf485-q5rgq   1/1     Running            2          7d2h
```

P.S. Lookup the —watch switch. Very useful 🙂

Right. Happy?

Good. Nothing like a bug to regulate those endorphins:

```python
$ python
Python 3.8.5 (default, Aug 24 2020, 07:14:09)
[Clang 11.0.3 (clang-1103.0.32.62)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> requests.post('http://192.168.64.2:31075/api/ali/run', json={'input': 'a=5'}).json()
{'output': ''}
>>> requests.post('http://192.168.64.2:31075/api/ali/run', json={'input': 'a'}).json()
{'output': 'Traceback (most recent call last):\n  File "<console>", line 1, in <module>\nNameError: name \'a\' is not defined\n'}
```

Now, can you figure out whats happening here and why?