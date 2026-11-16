## Monitoring Logs with Alloy, Loki and Grafana 


Below is the complete setup how to use Grafana/alloy, Grafana/loki and Grafana to collect, store, query,log files from host systems, containers, applications, cloud and infrastructures.  

To simplify the setup, I use Grafana, Alloy and Loki docker images to monitor/visualize containers' log files, host service log files and some other local log files.  

**Setup**  
Run the below commands to download the demo repository and run Grafana web UI.  
```bash
#Downloading the repository
git clone git@github.com:hiepdng/monitoring_alloy_loki_grafana_logs.git

#Creating volumes
cd monitoring_alloy_loki_grafana_logs
mkdir grafana_data
sudo chown -R 472:472 grafana_data
mkdir loki_data
sudo chown -R 10001:10001 loki_data
mkdir alloy_data
sudo chown -R 473:473 alloy_data

#Running containers
docker compose up -d
```
**Access Grafana web:**  
Go to http://localhost:3000/ to access your local Grafana webpage and view the host and containers metrics.  

To view specific container webpages:  
- Alloy: http://localhost:12345/
- Loki: http://localhost:9100/ready
 

**View Grafana Drilldown Logs:**  
In the Grafana webpage (http://localhost:3000/), by default the Drilldown Logs will display service label tab.  
Click `Add label tab` to add more tabs.  

**Note:**  
- Not all log files are collected because file size and permission. To fix these problems:  
  - Increate the `max_line_size` on the loki-config.yaml file.  
  - increase the `batch_size` in the config.alloy file.  
  - Add alloy user the group othe log file you try to monitor, for example:  
    `$ usermod -aG adm alloy`   

