0. Install Vysor and use it to interact with your phone:

- https://vysor.io

1. Install TermUX from Play store.

2. pkg install openssh curl tmux

3. Install ssh key trust:

    mkdir -p ~/.ssh
    curl https://github.com/ianblenke.keys > ~/.ssh/authorized_keys

4. Run sshd

    sshd

5. Find the current ip for your phone:

    ip addr show dev wlan0

In the below examples, we will assume that `192.168.1.3` is the ip of the android phone. 
Please substitute your phone's IP.

6. Run a tmux session to attach to:

    tmux

6. ssh into the phone:

    ssh 192.168.1.3 -p 8022

7. Attach to the floating tmux session:

    tmux a

Now you're in a termux context, over ssh. Interacting with the phone become easier.

Clone the apachespot demo docker repo on the phone:

    git clone https://github.com/Open-Network-Insight/spot-docker

Install the python dependencies:

    pkg install python python2-dev libzmq-dev
    apt install clang python python-dev fftw
    LDFLAGS=" -lm -lcompiler_rt" pip install numpy pandas pyzmq jinja2 tornado jsonschema ipython==3.2.0 jupyter

Generate a Jupyter config:

    jupyter notebook --generate-config

Set the Jupyter password (you will need this later):

    jupyter notebook password

Install the Node.js dependencies for the UI:

    pkg install node.js
    npm install -g browserify uglifyjs

Build the UI components:

    cd assets/spot-oa/ui
    npm install reactify d3-queue d3-hierarchy
    npm install
    npm run build-all

Now we can start the main interactive python service:

    bash runIpython.sh

Open the python notebook web interface:

- http://192.168.1.3:8889/

Enter the password you entered above while configuring Jupyter.

Navigate to the `ipynb/` folder by clicking on it.

Under the `dns/`, `flow/`, and `proxy/` folders there are `*/Edge_Investigation.ipynb` and `*/Thread_Investigation.ipynb` for each. Open these up and click Run to start running those notebooks.

Now you should be able to visit the web pages for each by directly on each, either locally:

http://127.0.0.1:8889/files/ui/flow/suspicious.html#date=2016-07-08

or remotely:

http://192.168.1.3:8889/files/ui/flow/suspicious.html#date=2016-07-08

Substitute `192.168.1.3` with the IP of your Android phone.


