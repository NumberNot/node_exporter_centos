# The Prometheus node_exporter install procedure. Clean and simple. :rocket:

OS CentOS7/8.
Original article by Darshana at [fosslinux.com](https://www.fosslinux.com/10398/how-to-install-and-configure-prometheus-on-centos-7.htm) .

```bash
wget -O node_exporter.tar.gz wget https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz
tar xvzf node_exporter.tar.gz
useradd -rs /bin/false node-exp
mv node_exporter/node_exporter /usr/local/bin/
nano /etc/systemd/system/node_exporter.service
```
## The systemd unit file
```bash
  [Unit]
  Description=Node Exporter
  After=network.target

  [Service]
  User=node-exp
  Group=node-exp
  Type=simple
  ExecStart=/usr/local/bin/node_exporter

  [Install]
  WantedBy=multi-user.target
```
Again bash
```bash
systemctl daemon-reload
systemctl start node_exporter
systemctl status node_exporter
systemctl enable node_exporter
firewall-cmd --zone=internal --add-port=9100/tcp --permanent
firewall-cmd --reload
http://IP-Address:9100/metrics
```
