# FILEBEAT OUTPUT LOGTASH MULTIPLE LOGS INDEX
- copy file filebat-kubernetes.conf to server logtash on folder`/etc/logstash/conf.d/`

### Filter logs with spesific message
```
output {
  if "kube-system" in [message] and [kubernetes][namespace] == "ingress-nginx" {
    elasticsearch {
        hosts => ["https://localhost:9200"]
        #define index name send to ElasticSearch
        index => "filebeat-data-kube-system-%{+YYYY.MM.dd}"
	    user => "elastic"
        password => "mypass"
	    #ssl_certificate_verification => false
	    cacert => "/etc/logstash/elasticsearch-ca.pem"
    }
  }
  if "default" in [message] and [kubernetes][namespace] == "ingress-nginx" {
    elasticsearch {
        hosts => ["https://localhost:9200"]
        #define index name send to ElasticSearch
        index => "filebeat-data-default-%{+YYYY.MM.dd}"
	    user => "user"
        password => "mypass"
	    #ssl_certificate_verification => false
	    cacert => "/etc/logstash/elasticsearch-ca.pem"
    }
  }
}
```