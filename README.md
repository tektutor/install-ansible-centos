# Installing Ansible in CentOS 7.9.2009

```
sudo yum -y install epel-release
sudo yum -y update
sudo yum install zlib-devel
sudo yum -y groupinstall "Development Tools"
sudo yum -y install openssl-devel bzip2-devel libffi-devel xz-devel
sudo yum -y install wget
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz
tar xvf Python-3.8.12.tgz
cd Python-3.8*/
./configure --enable-optimizations
sudo make altinstall
python3.8 --version
sudo ln -sf /usr/local/bin/python3.8 /usr/bin/python3
sudo yum install -y python3-pip
pip --version
pip3 --version

python3 -m pip install ansible
ansible --version
```


## Troubleshooting

In case of the below error
<pre>
cryptographydeprecationwarning-python-3-6-is-no-longer-supported-by-the-python
</pre>

Edit the file
```
sudo vim /usr/local/lib/python3.6/site-packages/ansible/parsing/vault/__init__.py
```

Add the below before importing crypto package
<pre>
warnings.filterwarnings(action='ignore',message='Python 3.6 is no longer supported')
</pre>
