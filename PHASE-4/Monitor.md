# Highly recomended to follow the steps shown in video

### Links to download Prometheus, Node_Exporter & black Box exporter https://prometheus.io/download/
### Links to download Grafana https://grafana.com/grafana/download
### Other link from video https://github.com/prometheus/blackbox_exporter



##prometheus.yml 
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: 'node_exporter'
    static_configs:
      - targets: ['13.201.87.28:9100']

  - job_name: 'jenkins'
    metrics_path: '/prometheus'
    static_configs:
      - targets: ['13.201.87.28:8080']

  - job_name: 'blackbox'
    metrics_path: /probe
    params:
      module: [http_2xx]  # Look for a HTTP 200 response.
    static_configs:
      - targets:
        - http://prometheus.io    # Target to probe with http
        - http://15.207.254.100:31372
        - http://3.109.213.19:31372
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 35.154.10.118:9115  # The blackbox exporter's real hostname:port.
                                                                                        
