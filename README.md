
  

# About

  
Simple vagrant eviroment, that brings three machines.

- One that is haproxy that gives balance to other two

- two identical machines that are runing simple node server

App is taken from https://blog.risingstack.com/your-first-node-js-http-server/

  

# Disclamer

It is for learning process only. 

Works with ansible 2.0 and up

Ubuntu 16.X box is used - for now will not work on RedHat(and forks from it).

Testing was done on MacOs High Sierra. Probably will work on other. If not let me know.

  

# Usage

Machine names are:

- m1 - first node machine ip 192.168.101.12

- m2 - second node machine ip 192.168.101.13

- ha - loadbalance machine ip 192.168.101.10


## Set up enviroment

Run: `vagrant up`
Ansible should take care of it.

## Conect to machine

Run: vagrant ssh machine_name

Like: `vagrant ssh ha`

  

## Starting node server

Ansible starts server and manages so that second instance is not started

Manipulate by hand:

- connect to m1 or m2

- start: `forever start index.js`

- stop: `forever stopall`

- restart: `forever restartall`

!!! You can also use ID of running process. See forever documentation how it is done !!!

## Testing balance
connect to ha:
run: `curl localhost:8080`
With second run text should change.