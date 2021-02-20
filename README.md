
# Docker-Nagios

This is a fork of [jasonrivers/nagios](https://hub.docker.com/r/jasonrivers/nagios/) Docker image. The original version was over two years old, on Ubuntu 16.04 and Nagios 4.4.5. This version is Ubuntu 20.05 and Nagios 4.4.6, as well as all updated NRPE and Nagios Plugin versions.

This fork also includes some additional plugins that were helpful to my own requirements. Those are listed below.

### Configurations
Nagios Configuration lives in /opt/nagios/etc
NagiosGraph configuration lives in /opt/nagiosgraph/etc

### Install

```sh
docker pull aaronmweiss/nagios:latest
```

### Running

Run with the example configuration with the following:

```sh
docker run --name nagios -p 0.0.0.0:8080:80 aaronmweiss/nagios:latest
```

alternatively you can use external Nagios configuration & log data with the following:

```sh
docker run --name nagios  \
  -v /path-to-nagios/etc/:/opt/nagios/etc/ \
  -v /path-to-nagios/var:/opt/nagios/var/ \
  -v /path-to-custom-plugins:/opt/Custom-Nagios-Plugins \
  -v /path-to-nagiosgraph-var:/opt/nagiosgraph/var \
  -v /path-to-nagiosgraph-etc:/opt/nagiosgraph/etc \
  -p 0.0.0.0:8080:80 aaronmweiss/nagios2004:4.4.6
```

Note: The path for the custom plugins will be /opt/Custom-Nagios-Plugins, you will need to reference this directory in your configuration scripts.

There are a number of environment variables that you can use to adjust the behaviour of the container:

| Environamne Variable | Description |
|--------|--------|
| MAIL_RELAY_HOST | Set Postfix relayhost |
| MAIL_INET_PROTOCOLS | set the inet_protocols in postfix |
| NAGIOS_FQDN | set the server Fully Qualified Domain Name in postfix |
| NAGIOS_TIMEZONE | set the timezone of the server |

For best results your Nagios image should have access to both IPv4 & IPv6 networks

#### Credentials

The default credentials for the web interface is `nagiosadmin` / `nagios`

### Extra Plugins

* Nagios nrpe [<http://exchange.nagios.org/directory/Addons/Monitoring-Agents/NRPE--2D-Nagios-Remote-Plugin-Executor/details>]
* Nagiosgraph [<http://exchange.nagios.org/directory/Addons/Graphing-and-Trending/nagiosgraph/details>]
* JR-Nagios-Plugins -  custom plugins I've created [<https://github.com/JasonRivers/nagios-plugins>]
* WL-Nagios-Plugins -  custom plugins from William Leibzon [<https://github.com/willixix/WL-NagiosPlugins>]
* JE-Nagios-Plugins -  custom plugins from Justin Ellison [<https://github.com/justintime/nagios-plugins>]
* check_ipmi_sensor - Thomas-Kreen [<https://github.com/thomas-krenn/check_ipmi_sensor_v3>]
* Nagios-Wordpress-Update - check WordPress core, theme, and plugin verison [<https://github.com/jinjie/Nagios-WordPress-Update>]
* TrueNAS/FreeNAS - Checks alerts, zpool, and replications [<https://github.com/StewLG/check_truenas_extended_play>]
