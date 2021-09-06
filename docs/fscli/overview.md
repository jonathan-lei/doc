# FSCLI

FSCLI is a module that simplifies starting, stopping & deleting servers based on server_id and email. It directly interacts with the console's API, which then delegates the action to the specific provider. 

**This should be the preferred way to manage machines, as it changes the Airtable records for you. However, if the Airtable record is not correct, manually manage the system and don't use FSCLI.**

## Installation

You can install the FSCLI package using pip3. If there are any errors or issues with pip3, then you can install it using Git (down below).

### Installing FSCLI via pip3

`pip3 install --upgrade fscli`

### Installation From Source

Cloning the Repository

If you are installing from source, be sure to have git installed on your machine.

`git clone https://github.com/fluidstackio/fscli.git`

**Installing the packages**

You can use pip3 to install the packages required to run the package.

`cd FSCLI && sudo pip3 install -r requirements.txt`


## Usage

These are different commands that you can run, replace the word inside the <> with the replacement value.

* `python3 -m fscli --start --email <email> --server_id <server id>`
* `python3 -m fscli --stop_all --email <email>`
* `python3 -m fscli --stop --email <email> --server_id <server id>`
* `python3 -m fscli --destroy_all --email <email>`
* `python3 -m fscli --destroy --email <email> --server_id <server_id>`
* `python3 -m fscli --fraud_set --email <email>`