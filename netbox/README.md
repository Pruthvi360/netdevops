# Netbox Installation
# Postgres installation
```
apt -y update
apt -y install postgresql postgresql-common
```
```
systemctl is-enabled postgresql
systemctl status postgresql
```
```
sudo -u postgres psql
CREATE DATABASE netbox;
CREATE USER netbox WITH PASSWORD '1996';
GRANT ALL PRIVILEGES ON DATABASE netbox TO netbox;
\conninfo
\q
```
```
psql --username netbox --password --host localhost netbox
password: 1996
\q
```
```
apt -y install redis-server
systemctl is-enabled redis-server
systemctl status redis-server
vi /etc/redis/redis.conf
 requirepass 1996
systemctl restart redis-server
redis-cli
AUTH 1996
Ctl+d
```
```
sudo mkdir -p /opt/netbox/ && cd /opt/netbox/
cd ../
rm -rf /opt/netbox
useradd -r -d /opt/netbox -s /usr/sbin/nologin netbox
sudo apt -y install -y git python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev
pip3 install --upgrade pip
wget https://codeload.github.com/netbox-community/netbox/tar.gz/v3.4.1
tar -xzf v3.4.1 -C /opt
ln -s /opt/netbox-3.4.1/ /opt/netbox
ls -l /opt | grep netbox
chown -R netbox:netbox /opt/netbox
cd /opt/netbox/netbox/netbox/
```
```
python3 ../generate_secret_key.py
ahflhaoighiajhfoj2994hgilahglajgaf
cp configuration_example.py configuration.py
nano configuration.py
```
```
ALLOWED_HOSTS = ['*']
DATABASE = {
USER = netbox
PASSWORD = Pruthvi@12s360
}
redi_server = {
USERNAME = ''
PASSWORD = '1996'
}
redis_server_cache = {
USERNAME = ''
PASSWORD = '1996'
}

SECRET = "ahflhaoighiajhfoj2994hgilahglajgaf"
```
```
cd /opt/netbox
pip3 install -r /opt/netbox/requirements.txt
/opt/netbox/upgrade.sh



systemctl daemon-reload
cd /opt/netbox/netbox
source /opt/netbox/venv/bin/activate
cd /opt/netbox/netbox
python3 manage.py createsuperuser
```
```
exit
sudo su
cd /opt/netbox
cp contrib/gunicorn.py /opt/netbox/gunicorn.py
cp contrib/*service /etc/systemd/system/
systemctl daemon-reload
systemctl enable netbox netbox-rq
systemctl start netbox netbox-rq
systemctl status netbox netbox-rq
```
```
cp /opt/netbox/contrib/nginx.conf /etc/nginx/sites-available/netbox
cd /etc/nginx/sites-enabled/
rm default
ln -s /etc/nginx/sites-available/netbox
service nginx restart
```
```
nano /opt/netbox/gunicorn.py
```
```
edit bind= '<public-ip>:8001'
```
```
systemctl daemon-reload
systemctl enable netbox netbox-rq
systemctl restart netbox netbox-rq
systemctl status netbox netbox-rq
```
