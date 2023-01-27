# Step-by-Step docomentation :notebook:

In this section, I will try to explain every step I took to achieve the main goal of this project. Step by step, I will go through the mandatory changes I made. Well, now maybe you ask yourself, "What exactly is the goal?" The main goal is to have a small t2.micro instance that boots up with different software packages that allow me to create an email address from the domain I bought for it and allow me to connect from each device to the mailbox. Besides that, since we already have the domain, we could also host a simple nginx webserver. But this is not everything - doing all this and matching the requirements is not hard enough for me. I want to build this in one step with one click, and this is possible with cloud-init. This means I need to set it up so that cloud-init understands what I actually want to have.

## First things first :point_up:

The first thing I did was search for and find a valid good-and-nonsense domain for this project. After a few research tactics and recent stories about Andrew Tate and his entire scandal story, I decided to come up with:

>**[BORINGTATE.STORE](https://boringtate.store)**


After buying the domain for 1.20 CHF from [GoDaddy](https://www.godaddy.com/de-ch) I also created a nonsense email address to later open a brand new AWS account. The chosen email provider was, amazingly, not Google it was GMX. After creating the email address, I needed a name for the suitable domain, which I decided to come up with.

>boringtate.aws01@gmx.at

Now that we have a suitable domain and a valid email address for our project, the last thing that we need to do is create an [AWS Free Tier](https://portal.aws.amazon.com/billing/signup#/start/email) account. After creating the AWS account and going through the activation of the account, we could actually start working on our project.


### The first instance :boom:

As usual, I created the standard EC2 t2.micro with Ubuntu 22.04, 25GB of space, and no special network group instance to see which packages I needed to install to get this working. After researching, I could find out the necessary software packages that needed to be installed and configured. 

<img src='/img/ec2_name.png' alt="ec2_name"></img>
<img src='/img/t2micro.png' alt="t2micro" ></img>
<img src='/img/network_group.png' alt="network" ></img>
<img src='/img/ports.png' alt="ports" ></img>
<img src='/img/cloud-config.png' alt="cloud-config" ></img>


### Could-config what the ..? :dizzy_face:

Since I had touch points with YAML and Ansible, I could really quickly understand what could-config is and how it works on AWS EC2 instances. This whole setup can help a lot if you have a clear and nice cloud-config file. The advantage of it is that you are freaking fast if you have to setup, for example, 20 nginx webservices at one time, and every one of them is built like the other, so there aren't any more human mistakes.

### The second instance but with cloud-config :poop:

I tried to setup the could-config file according to the requirements that he needs regarding the syntax. I could already configure the instance's fqdn and which software packages he needed to install, but there was a longer list of different unix commands that needed to be run before everything worked as expected. As you can imagine, at first I had a lot of issues because there was sometimes a syntax error because I overtyped it or because I didn't setup enough sleep time for the system to cool off after specified commands. 


### The last run :runner:

After tweaking and configuring the software packages as I wanted to, I could create a cloud-config with the perfect changes. The only manual interaction was at the first sleep time for the system that I needed to change on [GoDaddy](https://www.godaddy.com/de-ch) the necessary DSN changes with the public IP from the instance. This needs to be done to create the Let's Encrypt certificate for the domain. Only with the certificate does the postfix software package function properly.