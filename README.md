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
/usr/local/lib/python3.6/site-packages/ansible/parsing/vault/__init__.py:44: CryptographyDeprecationWarning: Python 3.6 is no longer supported by the Python core team. Therefore, support for it is deprecated in cryptography and will be removed in a future release.
  from cryptography.exceptions import InvalidSignature</pre>

Edit the file
```
sudo vim /usr/local/lib/python3.6/site-packages/ansible/parsing/vault/__init__.py
```

Add the below before importing crypto package
<pre>
warnings.filterwarnings(action='ignore',message='Python 3.6 is no longer supported')
</pre>

## Final you should have an working ansible setup
<pre>
[jegan@tektutor.org windows-node]$ ansible --version
ansible [core 2.11.12] 
  config file = /home/jegan/.ansible.cfg
  configured module search path = ['/home/jegan/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.6/site-packages/ansible
  ansible collection location = /home/jegan/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.6.8 (default, Nov 16 2020, 16:55:22) [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)]
  jinja version = 3.0.3
  libyaml = True
</pre>
