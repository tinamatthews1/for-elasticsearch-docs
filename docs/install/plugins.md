---
layout: default
title: Standalone Elasticsearch Plugin Install
parent: Install and Configure
nav_order: 90
---

# Standalone Elasticsearch plugin installation

If you don't want to use the all-in-one Open Distro for Elasticsearch installation options, you can install the individual plugins on a compatible Elasticsearch cluster, just like any other Elasticsearch plugins.


---

#### Table of contents
1. TOC
{:toc}


---

## Plugin compatibility

<table>
  <thead style="text-align: left">
    <tr>
      <th>Elasticsearch version</th>
      <th>Plugin versions</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>7.9.1</td>
    <td>
      <pre>opendistro-anomaly-detection    1.10.1.0, 1.11.0.0
opendistro-job-scheduler        1.10.1.0, 1.11.0.0
opendistro-knn                  1.10.1.0, 1.11.0.0
opendistro_alerting             1.10.1.2, 1.11.0.1
opendistro_index_management     1.10.1.1, 1.11.0.0
opendistro_performance_analyzer 1.10.1.0, 1.11.0.0
opendistro_security             1.10.1.0, 1.11.0.0
opendistro_sql                  1.10.1.1, 1.11.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.8.0</td>
    <td>
      <pre>opendistro-anomaly-detection    1.9.0.0
opendistro-job-scheduler        1.9.0.0
opendistro-knn                  1.9.0.0
opendistro_alerting             1.9.0.0
opendistro_index_management     1.9.0.0
opendistro_performance_analyzer 1.9.0.1
opendistro_security             1.9.0.0
opendistro_sql                  1.9.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.7.0</td>
    <td>
      <pre>opendistro-anomaly-detection    1.8.0.0
opendistro-job-scheduler        1.8.0.0
opendistro-knn                  1.8.0.0
opendistro_alerting             1.8.0.0
opendistro_index_management     1.8.0.0
opendistro_performance_analyzer 1.8.0.0
opendistro_security             1.8.0.0
opendistro_sql                  1.8.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.6.1</td>
    <td>
      <pre>opendistro-anomaly-detection    1.7.0.0
opendistro-job-scheduler        1.7.0.0
opendistro-knn                  1.7.0.0
opendistro_alerting             1.7.0.0
opendistro_index_management     1.7.0.0
opendistro_performance_analyzer 1.7.0.0
opendistro_security             1.7.0.0
opendistro_sql                  1.7.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.4.2</td>
    <td>
      <pre>opendistro-job-scheduler        1.4.0.0
opendistro-knn                  1.4.0.0
opendistro_alerting             1.4.0.0
opendistro_index_management     1.4.0.0
opendistro_performance_analyzer 1.4.0.0
opendistro_security             1.4.0.0
opendistro_sql                  1.4.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.3.2</td>
    <td>
      <pre>opendistro-job-scheduler        1.3.0.0
opendistro_alerting             1.3.0.1
opendistro_index_management     1.3.0.1
opendistro_performance_analyzer 1.3.0.0
opendistro_security             1.3.0.0
opendistro_sql                  1.3.0.0
</pre>
    </td>
  </tr>
  <tr>
    <td>7.2.1</td>
    <td>
      <pre>opendistro-job-scheduler        1.2.1
opendistro_alerting             1.2.1.0
opendistro_performance_analyzer 1.2.1.0
opendistro_security             1.2.1.0
opendistro_sql                  1.2.1.0</pre>
    </td>
  </tr>
    <tr>
      <td>7.2.0</td>
      <td>
        <pre>opendistro-job-scheduler        1.2.0
opendistro_alerting             1.2.0.0
opendistro_performance_analyzer 1.2.0.0
opendistro_security             1.2.0.0
opendistro_sql                  1.2.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>7.1.1</td>
      <td>
        <pre>opendistro-job-scheduler        1.1.0
opendistro_alerting             1.1.0.0
opendistro_performance_analyzer 1.1.0.0
opendistro_security             1.1.0.0
opendistro_sql                  1.1.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>7.0.1</td>
      <td>
        <pre>opendistro-job-scheduler        1.0.0
opendistro_alerting             1.0.0.0
opendistro_performance_analyzer 1.0.0.0
opendistro_security             1.0.0.2
opendistro_sql                  1.0.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>6.8.1</td>
      <td>
        <pre>opendistro_alerting             0.10.0.0
opendistro_performance_analyzer 0.10.0.0
opendistro_security             0.10.0.0
opendistro_sql                  0.10.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>6.7.1</td>
      <td>
        <pre>opendistro_alerting             0.9.0.0
opendistro_performance_analyzer 0.9.0.0
opendistro_security             0.9.0.0
opendistro_sql                  0.9.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>6.6.2</td>
      <td>
        <pre>opendistro_alerting             0.8.0.0
opendistro_performance_analyzer 0.8.0.0
opendistro_security             0.8.0.0
opendistro_sql                  0.8.0.0</pre>
      </td>
    </tr>
    <tr>
      <td>6.5.4</td>
      <td>
        <pre>opendistro_alerting             0.7.0.0
opendistro_performance_analyzer 0.7.0.0
opendistro_security             0.7.0.1
opendistro_sql                  0.7.0.0</pre>
      </td>
    </tr>
  </tbody>
</table>

To install plugins manually, you must have the exact OSS version of Elasticsearch installed (for example, 6.6.2 and not 6.6.1). To get a list of available Elasticsearch versions on CentOS 7 and Amazon Linux 2, run the following command:

```bash
sudo yum list elasticsearch-oss --showduplicates
```

Then you can specify the version that you need:

```bash
sudo yum install elasticsearch-oss-6.7.1
```


## Install plugins

Navigate to the Elasticsearch home directory (most likely, it is `/usr/share/elasticsearch`), and run the install command for each plugin.


### Security

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-security/opendistro_security-{{site.odfe_version}}.0.zip
```

After installing the security plugin, you can run `sudo sh /usr/share/elasticsearch/plugins/opendistro_security/tools/install_demo_configuration.sh` to quickly get started with demo certificates. Otherwise, you must configure it manually and run [securityadmin.sh](../../security/configuration/security-admin/).

The security plugin has a corresponding [Kibana plugin](../../kibana/plugins) that you probably want to install as well.


### Job Scheduler

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-job-scheduler/opendistro-job-scheduler-{{site.odfe_version}}.0.zip
```


### Alerting

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-alerting/opendistro_alerting-{{site.odfe_version}}.1.zip
```

To install Alerting, you must first install the Job Scheduler plugin. Alerting has a corresponding [Kibana plugin](../../kibana/plugins) that you probably want to install as well.


### SQL

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-sql/opendistro_sql-{{site.odfe_version}}.0.zip
```


### Index State Management

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-index-management/opendistro_index_management-{{site.odfe_version}}.0.zip
```

To install Index State Management, you must first install the Job Scheduler plugin. ISM has a corresponding [Kibana plugin](../../kibana/plugins) that you probably want to install as well.


### KNN

KNN is only available as part of the all-in-one installs: Docker, RPM, and Debian.


### Anomaly Detection

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/opendistro-anomaly-detection/opendistro-anomaly-detection-{{site.odfe_version}}.0.zip
```


### Performance Analyzer

```bash
sudo bin/elasticsearch-plugin install https://d3g5vo6xdbdb9a.cloudfront.net/downloads/elasticsearch-plugins/performance-analyzer/opendistro_performance_analyzer-{{site.odfe_version}}.0.zip
```

Performance Analyzer requires some manual configuration after installing the plugin:

1. Create `/usr/lib/systemd/system/opendistro-performance-analyzer.service` based on [this file](https://github.com/opendistro-for-elasticsearch/performance-analyzer/blob/master/packaging/opendistro-performance-analyzer.service).

1. Make the CLI executable:

   ```bash
   sudo chmod +x /usr/share/elasticsearch/bin/performance-analyzer-agent-cli
   ```

1. Run the appropriate `postinst` script for your Linux distribution:

   ```bash
   # Debian-based distros
   sudo sh /usr/share/elasticsearch/plugins/opendistro_performance_analyzer/install/deb/postinst.sh 1

   # RPM distros
   sudo sh /usr/share/elasticsearch/plugins/opendistro_performance_analyzer/install/rpm/postinst.sh 1
   ```

1. Make Performance Analyzer accessible outside of the host machine

   ```bash
   cd /usr/share/elasticsearch # navigate to the Elasticsearch home directory
   cd plugins/opendistro_performance_analyzer/pa_config/
   vi performance-analyzer.properties
   ```

   Uncomment the line `#webservice-bind-host` and set it to `0.0.0.0`:

   ```bash
   # ======================== Elasticsearch performance analyzer plugin config =========================

   # NOTE: this is an example for Linux. Please modify the config accordingly if you are using it under other OS.

   # WebService bind host; default to all interfaces
   webservice-bind-host = 0.0.0.0

   # Metrics data location
   metrics-location = /dev/shm/performanceanalyzer/

   # Metrics deletion interval (minutes) for metrics data.
   # Interval should be between 1 to 60.
   metrics-deletion-interval = 1

   # If set to true, the system cleans up the files behind it. So at any point, we should expect only 2
   # metrics-db-file-prefix-path files. If set to false, no files are cleaned up. This  can be useful, if you are archiving
   # the files and wouldn't like for them to be cleaned up.
   cleanup-metrics-db-files = true

   # WebService exposed by App's port
   webservice-listener-port = 9600

   # Metric DB File Prefix Path location
   metrics-db-file-prefix-path = /tmp/metricsdb_

   https-enabled = false

   #Setup the correct path for certificates
   certificate-file-path = specify_path

   private-key-file-path = specify_path

   # Plugin Stats Metadata file name, expected to be in the same location
   plugin-stats-metadata = plugin-stats-metadata

   # Agent Stats Metadata file name, expected to be in the same location
   agent-stats-metadata = agent-stats-metadata
   ```

1. Start the Elasticsearch service:

   ```bash
   sudo systemctl start elasticsearch.service
   ```

1. Send a test request:

   ```bash
   curl -XGET "localhost:9600/_opendistro/_performanceanalyzer/metrics?metrics=Latency,CPU_Utilization&agg=avg,max&dim=ShardID&nodes=all"
   ```


## List installed plugins

To check your installed plugins:

```bash
sudo bin/elasticsearch-plugin list
```


## Remove plugins

If you are removing Performance Analyzer, see below. Otherwise, you can remove the plugin with a single command:

```bash
sudo bin/elasticsearch-plugin remove <plugin-name>
```

Then restart Elasticsearch on the node:

```bash
sudo systemctl restart elasticsearch.service
```


### (Optional) Clean up Performance Analyzer files

Performance Analyzer requires certain configuration files to run. If you want to delete these files, run one of the scripts we provide based on your Linux distribution *before* performing the normal plugin removal process.

1. Make the removal scripts executable:

   ```bash
   sudo chmod +x plugins/opendistro_performance_analyer/install/deb/postrm sudo sh plugins/opendistro_performance_analyer/install/rpm/postrm
   ```

1. Run the appropriate removal script for your distribution:

   ```bash
   # Debian-based distros
   sudo --preserve-env=ES_HOME ./plugins/opendistro_performance_analyer/install/deb/postrm

   # RPM distros
   sudo --preserve-env=ES_HOME ./plugins/opendistro_performance_analyer/install/rpm/postrm
   ```

Then proceed with the normal removal procedure.


## Update plugins

Elasticsearch doesn't update plugins. Instead, you have to remove and reinstall them:

```bash
sudo bin/elasticsearch-plugin remove <plugin-name>
sudo bin/elasticsearch-plugin install <plugin-name>
```
