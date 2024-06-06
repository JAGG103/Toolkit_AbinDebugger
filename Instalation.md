# Instalation

# Install Python 3.7 

```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository ppa:deadsnakes/ppa
sudo apt install python3.7
python3.7 --version
```

# Create environment

```
sudo apt install python3.7-venv
python3.7 -m venv abindebugger_venv
source abindebugger_venv/bin/activate
pip install --upgrade pip
```

# Clone repository

```
sudo apt install git
git clone http://github.com/jbcamacho/AbinDebugger.git
```

# Install dependencies

```
pip install -r AbinDebugger/requirements.txt
deactivate
sudo apt-get install libxcb-randr0-dev libxcb-xtest0-dev libxcb-xinerama0-dev libxcb-shape0-dev libxcb-xkb-dev
sudo apt update
```

# Install MongoDB (20.04 LTS ("Focal"))

## Import the public key

```
sudo apt-get install gnupg curl
```

```
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
```

## Create a list file for mongoDB

```
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

## Reload local package database

```
sudo apt-get update
```

## Install the mongoDB packages

```
sudo apt-get install -y mongodb-org
```

# Download the bug patterns collections

[Download patterns](https://drive.google.com/file/d/1NPZYI4ykUyap1PdUKrZPR4hCIJAlRCle/.)

# Start mongoDB and import patterns

## Start mongodb

```
systemctl start mongod
sudo systemctl enable mongod
mongoimport --db Bugfixes --collection BugPatterns --file <filepath> --jsonArray
```

# Solve mongodb error (Result: core-dump)

Al consultar el status de mongodb `sudo systemctl status mongod`

Si se obtiene la salida: Active: failed (Result: core-dump)
Se debe a la incompatibilidad con la arquitectura del computador donde estamos trabajando.

## Instalando una versión mas antigua version 4.0.4

- Stop mongodb

```
sudo service mongod stop
```

- Remove packages

```
sudo apt-get purge mongodb-org*
```

- Remove database

```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

- Then reinstall mangodb 4.4.8

- Import public key

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
```

- For 20.04 LTS ("Focal")

```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
```

- Update

```
sudo apt-get update
```

- Install mongo

```
sudo apt-get install mongodb-org=4.4.8 mongodb-org-server=4.4.8 mongodb-org-shell=4.4.8 mongodb-org-mongos=4.4.8 mongodb-org-tools=4.4.8
```

- check status mongodb with `sudo systemctl status mongod`

## Error with mongodb 4.4.8

Restart mongodb

```
sudo systemctl restart mongod
sudo systemctl enable mongod
sudo systemctl status mongod
```

# Start mongoDB and import patterns

## Start mongodb

```
systemctl start mongod
sudo systemctl enable mongod
mongoimport --db Bugfixes --collection BugPatterns --file Descargas/Toolkit_AbinDebugger-main/BugPatterns.json --jsonArray
```

# activate environment and open abindebugger

```
source abindebugger_venv/bin/activate
cd AbinDebugger
python AbinDriver.py
```

# Create script to open abindebugger

```
#!/bin/bash

source ~/abindebugger_venv/bin/activate
cd ~/AbinDebugger
python AbinDriver.py
```






