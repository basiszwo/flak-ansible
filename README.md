# FLAK Stack - Ansible

## Why?

t.b.d


## Setup

### Requirements

You need a digitalocean access key.


### Commands

#### Provision all required droplets

```
ansible-playbook digitalocean.yml -i hosts --tags start --ask-become-pass
```

#### Provision example api droplets

```
ansible-playbook digitalocean.yml -i hosts --tags start --extra-vars "custom_host_group=api" --ask-become-pass
```

#### Provision kafka droplets

```
ansible-playbook digitalocean.yml -i hosts --tags start --extra-vars "custom_host_group=kafka" --ask-become-pass
```

#### Provision flink droplets

```
ansible-playbook digitalocean.yml -i hosts --tags start --extra-vars "custom_host_group=flink" --ask-become-pass
```

#### Provision Geomesa / Accumulo droplets

```
ansible-playbook digitalocean.yml -i hosts --tags start --extra-vars "custom_host_group=geomesa" --ask-become-pass
```

#### Wire up "network"

This is to update the `/etc/hosts` file on each droplet to know about the neighbors.

```
ansible-playbook -i hosts network.yml --tags setup
```


#### Install kafka brokers

```
ansible-playbook kafka.yml -i hosts --tags install
```


#### Install example api application

```
ansible-playbook api.yml -i hosts --tags install
```


#### Install flink brokers

```
ansible-playbook flink.yml -i hosts --tags install
```


#### Install geowave / accumulo

```
ansible-playbook geowave.yml -i hosts --tags install
```


#### Create kafka topic

```
ansible-playbook kafka.yml -i hosts --tags create-topic
```

## Verify Setup

### Show list of kafka topics

```
kafka/bin/kafka-topics.sh --list --zookeeper localhost:2181
```

### Show detailled information about kafka topic

```
kafka/bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic flak-example
```


#### Run flink job

```
flink/bin/flink run -c one.flak.flinkkafkaconsumer.Main ~/flinkkafkaconsumer-1.0-SNAPSHOT.jar --topic flak-example --bootstrap.servers kafka-1.flak.one:9092 --group.id flak-example
```


## Web pages

### HDFS

http://accumulo-1.flak.one:50070/


### Flink Master

http://flink-master.flak.one:8081/


### Accumulo Monitor

http://accumulo-1.flak.one:9995/


### GeoServer

http://accumulo-1.flak.one:8080/geoserver

Default username: `admin`
Default password: `geoserver`

For more information see GeoServer Quickstart Guide
http://docs.geoserver.org/latest/en/user/gettingstarted/web-admin-quickstart/index.html
