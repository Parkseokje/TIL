# Setting Elaticsearch and Kibana

## Install Elasticsearch

  I followed the guide listed [here](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/rpm.html#rpm-repo)

## Install Kibana

  I followed the guide listed [here](https://www.elastic.co/guide/en/kibana/7.6/deb.html#deb-repo)

  ```bash
  $ sudo vi /etc/kibana/kibana.yml

    # Modify these lines
    server.port: 5601
    server.host: "0.0.0.0"
  ```

## <span id="secure">Secure Elasticsearch & Kibana</span>

  For Security, [here](https://www.elastic.co/kr/blog/getting-started-with-elasticsearch-security)

  ```bash
  $ sudo /usr/share/elasticsearch/bin/elasticsearch-certutil cert -out /etc/elasticsearch/config/elastic-certificates.p12 -pass ""

  # If you meed "failed to initialize SSL TrustManager - access to read truststore file"
  $ chmod -R 770 /etc/elasticsearch/config
  ```

  `/etc/elasticsearch/elasticsearch.yml` should look like this:

  ```bash
  xpack.security.enabled: true
  xpack.security.transport.ssl.enabled: true
  xpack.security.transport.ssl.verification_mode: certificate
  xpack.security.transport.ssl.keystore.path: /etc/elasticsearch/config/elastic-certificates.p12
  xpack.security.transport.ssl.truststore.path: /etc/elasticsearch/config/elastic-certificates.p12
  ```

  Start elasticsearch

  ```bash
  $ sudo service elasticsearch start
  $ sudo /usr/share/elasticsearch/bin/elasticsearch-setup-passwords auto # It generates password for kibana
  ```

  Open `/etc/kibana/kibana.yml`

  ```bash
  elasticsearch.username: "kibana"
  elasticsearch.password: "{elasticsearch-setup-passwords generated kibana password}"
  ```

  And finally start/restart kibana

  ```bash
  $ sudo service kibana start
  ```

  Browse `http://{ES_URL}:5601`

  If you see Kibana login you have made it well.
  But when you don't clear your browser cache and try again.

### 참고
- [elasticsearch installation](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/rpm.html#rpm-repo)
- [kibana installation](https://www.elastic.co/guide/en/kibana/7.6/deb.html#deb-repo)
- [elasticsearch-security](https://www.elastic.co/kr/blog/getting-started-with-elasticsearch-security)