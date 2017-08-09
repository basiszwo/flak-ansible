# GeoServer Installation

Installation guide for GeoServer can be found at http://docs.geoserver.org/stable/en/user/installation/linux.html


Additional information for GeoServer and Geomesa: http://www.geomesa.org/documentation/user/architecture.html#geomesa-and-geoserver


Installing GeoMesa Accumulo in GeoServer
http://www.geomesa.org/documentation/user/accumulo/install.html#installing-geomesa-accumulo-in-geoserver


## Install Geomesa Accumulo GeoServer plugins

```
./geomesa-accumulo_2.11-1.3.2/bin/manage-geoserver-plugins.sh --lib-dir /home/accumulo/geoserver-2.11.2/webapps/geoserver/WEB-INF/lib --install
```


## Download JARs for correct accumulo and hadoop versions


Edit install script: geomesa-accumulo_2.11-1.3.2/bin/install-hadoop-accumulo.sh

Accumulo Version is 1.8.1

Then run with

```
./geomesa-accumulo_2.11-1.3.2/bin/install-hadoop-accumulo.sh /home/accumulo/geoserver-2.11.2/webapps/geoserver/WEB-INF/lib
```


## Start GeoServer

Use an Ubuntu init script. See http://docs.geoserver.org/stable/en/user/production/linuxscript.html#debian-ubuntu

This should be backed into ansible!

For now use `screen` to run GeoServer.

Run `./geoserver-2.11.2/bin/startup.sh`


Then visit http://accumulo-1.flak.one:8080/geoserver
