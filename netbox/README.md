# Netbox Installation
# Postgres installation
```
sudo apt-get install postgresql postgresql-contrib -y
```
```
systemctl status postgresql
```
```
sudo -u postgres psql
CREATE DATABASE netbox;
CREATE USER netbox WITH PASSWORD 'Pruthvi@12s360';
GRANT ALL PRIVILEGES ON DATABASE netbox TO netbox;
\q
```
```
psql --username netbox --password --host localhost netbox
password: Pruthvi@12s360
\q
```

```
sudo apt-get install wget ca-certificates nginx supervisor git gcc python3 python3-dev python3-pip python3-setuptools build-essential libxml2-dev libxslt1-dev libffi-dev graphviz libpq-dev libssl-dev zlib1g-dev unzip redis-server -y
```
```
sudo mkdir -p /opt/netbox/ && cd /opt/netbox/
cd ../
rm -rf /opt/netbox
sudo apt-get install -y python3.10.12 python3-pip python3-venv python3-dev build-essential libxml2-dev libffi-dev libpq-dev libssl-dev zlib1g-dev
pip3 install --upgrade pip
wget https://codeload.github.com/netbox-community/netbox/tar.gz/v3.4.1
tar -xzf v3.4.1 -C /opt
ln -s /opt/netbox-3.4.1/ /opt/netbox
ls -l /opt | grep netbox
cd /opt/netbox/netbox/netbox/
```
```
python3 ../generate_secret_key.py
ahflhaoighiajhfoj2994hgilahglajgaf
cp configuration_example.py configuration.py
nano configuration.py
```
```
ALLOWED_IP = ['*']
DATABASE = {
USER = netbox
PASSWORD = Pruthvi@12s360
}

SECRET = "ahflhaoighiajhfoj2994hgilahglajgaf"
```
```
cd ..
/opt/netbox/upgrade.sh
python3 manage.py migrate
python3 manage.py createsuperuser
```
