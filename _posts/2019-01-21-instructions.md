---
layout: post
title:  "Getting started at ETH Tier3"
---

This page is intended to help semester/master students in the first steps of their work with ETH. Send comments to micheli@cern.ch

## 1. Get an account at Tier3

The starting point is to **get an account at the T3 @ PSI**. You can follow the instructions [here](https://wiki.chipp.ch/twiki/bin/view/CmsTier3/HowToGetAccount). In general, you can specify that you don't
need a GRID account. Ask your supervisor what to put in "physics group". The suggested login shell is /bin/bash.

Basic instructions on how to login and perform basic operations can be found [here](https://wiki.chipp.ch/twiki/bin/view/CmsTier3/HowToSetupYourAccount). **Please note that for ETH the user interface host name is t3ui02.psi.ch**. 

## 2. Preliminary steps

The first step is to setup the environement for running **ROOT** and **jupyter**. [This page](https://wiki.chipp.ch/twiki/bin/view/CmsTier3/HowToWorkInCmsEnv#The_ROOT_Environment_and_Jupyter) collects the needed informations. 
After that try to start a jupyter notebook on a t3 machine:

```python
jupyter notebook --port 8883 --no-browser 
```

where 8883 has to be changed with the number of the PORT you used for setup.

Open a local browser on your laptop and go to <http://localhost:8883/tree>

## 3. Setting up a web-page

We will need **a lot of plots**. A convenient way is to look at them is to create a web-page for them.

**Instructions**:

0- Access your directory on people.phys.etz.ch following <https://readme.phys.ethz.ch/storage/access/>

1- Cut an paste the lines in  "Creating the homepage - Short description for Linux and Mac command line users” from :  <https://readme.phys.ethz.ch/web/how_to_get_a_personal_homepage/>

2- create in public_html a directory called plots.

3- cd plots

4- git clone https://github.com/musella/php-plots.git 

5- Follow the instructios here <https://github.com/musella/php-plots/blob/master/README.md>

6- It is suggested to get [this php file](https://github.com/michelif/ETH-Students-instuctions/blob/master/index_for_students.php) and overwrite the one you got from git. This php allows a better management for plot display

7- change mdonega —>you_username in index.php
   (it’s the line    $script_path = "/~mdonega/plots”;   )
   
8- send a mail to isg@phys.ethz.ch and ask them to enable php in your directory adding your supervisor in cc (say it’s the same configuration they made for mdonega) 

9- if everything works you should get something like this: 
     people.phys.ethz.ch/~mdonega/plots/uglyPlots_v9/
     
## How to use GPUs on Tier3

1. Get a Tier3 computing account and make sure that you can log in to the /t3home (use pwd to check if you are in the correct home directory). In case you dont have an account yet or only a shome directory follow the steps above and/or contact Tier3 admins. The t3home space is limited to 10GB, for bigger files use the shome directory or storage element.

2. Login to the GPUs using:

```bash
ssh t3gpu01
```

3. Set correct environment in order to use python and all libraries needed:

```bash
export PATH=/scratch/musella/anaconda3/bin:$PATH
```

which loads 4 environments which can be shown by using:

```bash
conda env list
```

- base (loads all basic packages with jupyter)
- cern root (ROOT6, not compatible with jupyter, but has root numpy, root pandas) 
- tensorflow (most important environment to train NNs)
- pytorch

Choose correct environment (e.g. for training tensorflow) by running

```bash
source activate tensorflow
```

4. Check which GPUs are in use
```bash
nvidia−smi
```

set the GPU number to one that is not in use by setting the environment variable CUDA VISIBLE DEVICES
before executing the script, e.g. in order to use GPU 1

```bash
CUDA VISIBLE DEVICES=1 ./ train .py
```


in the python script the tensorflow device mapping can be checked by adding:

```bash
import tensorflow as tf
import tensorflow . keras . backend as K

sess = tf.Session(config=tf.ConfigProto(log device placement=True))
K. set session(sess)
```

5. after starting the training, open new terminal, login to GPUs again and check GPU usage by running
```bash
nvidia−smi
```

6. in case you have questions or want to join the mattermost channel in which we discuss questions or general stuff
regarding the GPUs, write an email to christina.reissel@cern.ch.

