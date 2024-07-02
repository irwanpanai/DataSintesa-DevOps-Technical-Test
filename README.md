# DataSintesa DevOps Engineer Take-home Test

## General Knowledge Check

1. What is your favorite Linux distro and why?
2. What do you know about Container and Virtual Machine?
3. How is Container different from Virtual Machine?
4. How can you sync two local directories in Linux?
5. What is swap in Linux and what is it used for?
6. You have to find all files larger than 20 MB in your Linux OS. How you do it?
7. What is happening when the Linux kernel is starting the OOM killer and how does it
choose which process to kill first?
8. Explain the following command : (date ; ps -ef | awk '{print $1}'| sort |
uniq | wc -l) >> Activity.log
9. Server A cannot talk to Server B. Describe possible reasons!
10. How to know which process in Linux listens on a specific port?
11. An engineer type http://www.yahoo.com in the browser and he/she presses enter.
What happens next? (hint: describe activities happening at every OSI layer - physical,
data link, network, transport, session, presentation, application layer)
12. What about if the engineer change from http://www.yahoo.com into
https://www.yahoo.com ? (hint : describe activities related to public/private
certificates, CAs, proxying, MiTM, etc)
13. A web developer is creating a new web application and you have to store the user’s
passwords in a database. How would you store the passwords securely?
14. A DevOps engineer have added a public ssh key of a developer into
authorized_keys but the developer is still getting a password prompt, what can be
wrong?
15. Describe the Linux boot process with as much detail as possible, starting from when
the system is powered on and ending when you get a prompt!

## Take-Home Tests

### Overview

Your goal is to set up a simple hello-world Node.js app called oss on a development VM /
container.
The code for the simple Express web server as follows :
```
// Simple Express web server
// @see http://howtonode.org/getting-started-with-express
// Load the express module
var express = require('express');
var app = express();
// Respond to requests for / with 'Hello World'
app.get('/', function(req, res){
 res.send('Hello world!');
});
// Listen on port 80
app.listen(80, () => console.log('Express server started successfully.'));
```
The package.json file as follows :
```
{
 "name": "examplenodeapp",
 "description": "Example Express Node.js app.",
 "author": "dtndevopscandidate <devopscandidate@datasintesa.id>",
 "dependencies": {
 "express": "4.x"
 },
 "engine": "node >= 0.10.6"
}
```
### Goals

The server should be running :
1. Centos ≥ 7
2. Nginx ≥ 1.15
3. Postgresql ≥ 11
4. Node.js >= 0.10.6

The server must have 3 easily executable bash scripts in /opt/oss/bin :
1. ```bin/stop``` → stop the Express server, nginx, and postgresql.
2. ```bin/start``` → start the Express server, nginx, and postgresql.
3. ```bin/backup``` → dump the postgresql database to a .sqlfile in
```/opt/oss/data/backups```

### Outputs

A dockerfile or a vagrantfile which fulfills all the goals listed above, along with the 3
executable bash scripts.
Submit the answer to the recruiter max 2 days after day of assignment.
