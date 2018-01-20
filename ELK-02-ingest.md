
**logstash-apple**

```javascript
input {  
  file {
    path => "~/github/ELK-Stack/Logstash/logstash-apple.conf"
    start_position => "beginning"    
  }
}
filter {  
  csv {
      separator => ","
      columns => ["Date","Open","High","Low","Close","Volume","Adj Close"]
  }
  mutate {convert =&gt; ["High", "float"]}
  mutate {convert =&gt; ["Open", "float"]}
  mutate {convert =&gt; ["Low", "float"]}
  mutate {convert =&gt; ["Close", "float"]}
  mutate {convert =&gt; ["Volume", "float"]}
}
output {  
    elasticsearch {
        action => "index"
        host => "localhost"
        index => "stock"
        workers => 1
    }
    stdout {}
}
```


# Run Logstash


/opt/logstash/bin/logstash -f ~/github/ELK-Stack/logstash-apple.conf