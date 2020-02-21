# Filebeat

_Created by Seokje Park at 2020.02.21_

keyword

- `centralized logging`
- `log shipper`

## What is Beats ?

- Beats are collection of lightweight and open source log shipper
- Beats are built on top of a Go framework called libbeat.
- It acts as agents installed on the different servers for collecting lgos or metrics
- Filebeat : Collects log files
- Packetbeat : Collects network data
- Metricbeat : Collects server metrics
- Once collected, the data is sent to either directly into Elasticsearch or to Logstash.

## Quick start

Described on AWS Linux(AMI) basis.

- Download and install the public signing key:

  ```bash
  $ sudo rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch
  ```

- Create `elastic.repo` and add the following lines in your /etc/yum.repos.d/ directory:
  ```bash
  [elastic-7.x]
  name=Elastic repository for 7.x packages
  baseurl=https://artifacts.elastic.co/packages/7.x/yum
  gpgcheck=1
  gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
  enabled=1
  autorefresh=1
  type=rpm-md
  ```
- Modify `filebeat.yml` in /etc/filebeat/filebeat.yml:

  ```yml
  filebeat.inputs:
    - type: log
      enabled: true
      paths:
        - /home/ec2-user/.pm2/[APPNAME]*.log
  output.elasticsearch:
    hosts: ["<es_url>"]
  username: "elastic"
  password: "<password>"
  setup.kibana:
    host: "<kibana_url>"
  ```

- Add the following line `/etc/filebeat/modules.d/system.yml.disabled`: (Optional)

  This way you send log events in Elasticsearch with a UTC timestamp. Kibana can simply convert from UTC to whatever timezone you browser
  is in at request time.

  ```bash
  var.convert_timezone: true
  ```

- Enable logstash module

  ```bash
  $ sudo filebeat modules enable logstash
  ```

- Setup and start Filebeat

  ```bash
  $ sudo filebeat setup # A new index will be created in Elasticsearch which you can define in Kibana
  $ sudo service filebeat start
  $ sudo chkconfig --add filebeat # Start filebeat automatically during boot
  ```

- Kibana Management > Index Patterns create index pattern `filebeat-*`
- In Kibana Discover, change current index pattern to `filebeat-*` and set date filters.
- Click Refresh. if you see data, you made it. Congratulation!

## 참고

- [A Beats Tutorial](https://logz.io/blog/beats-tutorial/)
- [Filebeat and AWS Elasticsearch](https://www.partiallydisassembled.net/posts/filebeat-kibana-aws.html)
- [Repositories for APT and YUM](https://www.elastic.co/guide/en/beats/filebeat/current/setup-repositories.html)
- [System Log Aggregation with the Elastic Stack](https://linuxacademy.com/blog/certifications/system-log-aggregation-with-the-elastic-stack/)
