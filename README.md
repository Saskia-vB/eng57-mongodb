# Mongodb

## Provision

A script is provisioned by specifying a working directory, a log directory into which output from the script is recorded and a command to execute the script.


## Tests

Be sure to look at the vagrant up output as well as the tests to understand what is missing in your provision file.

## How to run tests?
```bash

cd starter-code
vagrant up
vagrant provision
cd tests
rake spec
```

This will identify the tests that you need to pass, in this case there are for tests:
1. install mangodb 3.2.20
2. start mangod
3. enable mangod
4. post 0.0.0.0


It is sometimes necessary to vagrant destroy before re doing the process above to start from a clean state and pass the tests.

```bash
vagrant destroy
```

## Provision

To pass the tests changes are made to the provision file.

1. Look at mongodb documentation online on how to install

```shell

wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -

echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update


sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections

```

2. make sure you look at specific requirement of test, i.e. mongod not mongodb
```shell
sudo systemctl start mongod
sudo systemctl status mongod
```

3.

```shell
sudo systemctl enable mongod
```


4.

```shell
sudo sed -i "s,\\(^[[:blank:]]*bindIp:\\) .*,\\1 0.0.0.0," /etc/mongod.conf
sudo service mongod restart
sudo systemctl enable mongod
```
