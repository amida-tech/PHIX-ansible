# Config Management: PHIX

Use these scripts to get up and runing with:
 * Personal Health Information eXchange [http://github.com/amida-tech/PHIX](http://wiki.directproject.org/message/view/Java+Reference+Implementation/60702540)

##  Two cloud servers (AWS/EC2)

Use same servers you used for installation of DIRECT


##### 1. Provision two fresh Ubuntu 12.04 VM in the cloud (use m1.medium instances) and setup DIRECT on them
##### 2.  Install dependencies (ansible) and clone repo of this playbook to your machine
##### 3.  Configuration your environment (see below)
##### 4.  Run this playbook
##### 5.  Run additional commands
##### 6.  Run PHIX/Clinician apps playbooks
##### 7.  Bootstrap apps with test users/data
```
ansible-playbook -i hosts.ini --verbose mean.yml
```

For both servers, login via ssh and execute following commands:
```
mkdir repos

cd repos

git clone git@github.com:amida-tech/PHIX.git

cd PHIX

npm install

#update app.js with proper configuration parameters

#update public/js/app.js with proper configuration parameters

#update watch.js with proper configuration parameters


```

```
sh ./run.sh

```


```
PATH=/home/ubuntu/local/bin:/home/ubuntu/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:~/repos/PHIX/node_modules/.bin

cd test/bootstrap/

#execute one of the bootstrap scripts depending on server role
mocha -R spec demoPHIX.js -t 10000

mocha -R spec demoClinicians.js -t 10000


```


### Config files
There are two short files you'll need to edit:

---

##### `nginx1/2.conf`

Update domain names to your setup
---

##### `hosts`
Update with hosts' IP addresses and path to your SSH keys.

---


## Configuring external DNS

In your domain's DNS, add entries for PHIX and Clinician Front-end apps (if different from DIRECT setup):

* `phix.amida-demo.com` (record type: `A`, value: `your first EC2 IP`)
* `clinician.amida-demo.com` (record type: `A`, value: `your second EC2 IP`)

With those two entries, you should be up and running!



#### Viewing logs
Your server's logs are at:
* `/var/log/upstart/phix.log` PHIX app log
* `/var/log/upstart/clinician.log` Clinician app log
* `/var/log/upstart/watcher-phix.log` PHIX watcher log
* `/var/log/upstart/watcher-clinician.log` Clinician watcher log

