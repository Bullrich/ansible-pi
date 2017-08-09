# Watchman

### Playbook for installing watchman for use with React

This playbook does the same as this script:
```bash
#!/bin/bash
if [ "$EUID" -ne 0 ]
  then echo "Please run as root"
  exit
fi

cd ~
apt-get install openssl libtool npm git livssl-dev
git clone https://github.com/facebook/watchman.git
cd watchman/
apt-get install -y autoconf automake build-essential python-dev
./autogen.sh
./configure
make
make install

watchman --version

echo 999999 | sudo tee -a /proc/sys/fs/inotify/max_user_watches  && echo 999999 | sudo tee -a  /proc/sys/fs/inotify/max_queued_events && echo 999999 | sudo tee  -a /proc/sys/fs/inotify/max_user_instances && watchman  shutdown-server
```
