# fluentd-config
Ruby and Fluentd and Google Cloud Storage Plugin Setup

## Upgrade Ruby on CentOS
[source](http://ask.xmodulo.com/upgrade-ruby-centos.html)
```
sudo yum remove ruby ruby-devel
sudo yum groupinstall -y "Development Tools"
sudo yum install -y openssl-devel
cd /tmp
wget http://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz
tar xvfvz ruby-2.4.1.tar.gz
cd ruby-2.4.1
./configure && make
sudo make install
sudo /usr/local/bin/gem update --system
sudo /usr/local/bin/gem install bundler
sudo /usr/local/bin/gem update
```

## Install fluentd on CentOS 
[source](https://docs.fluentd.org/v0.12/articles/install-by-rpm)
```
curl -L https://toolbelt.treasuredata.com/sh/install-redhat-td-agent2.sh | sh
chkconfig td-agent on
sudo service td-agent start
```

## Install Fluentd Plugin for Google Cloud Storage
[source](https://rubygems.org/gems/fluent-plugin-google-cloud-storage)
```
sudo td-agent-gem install fluent-plugin-google-cloud-storage
sudo service td-agent restart
```

## Install Fluentd Plugin for ElasticSearch
[source](https://www.fluentd.org/guides/recipes/elasticsearch-and-s3)
```
sudo td-agent-gem install fluent-plugin-elasticsearch
sudo service td-agent restart
```

## Notes on Fluentd
* To setup HA for Fluentd, refer to [here](https://docs.fluentd.org/v0.12/articles/high-availability)
* Need to add `localtime true` at the `/etc/td-agent/td-agent.conf` file since default may run into UTC time issue
