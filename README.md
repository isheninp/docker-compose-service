# How to make docker-compose running as service (Centos 7)

1. create file /etc/systemd/system/docker-compose.service

[Unit]
Description=docker-compose
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes

User=root
Group=root

WorkingDirectory=/home/data
PIDFile=/var/run/docker-compose/docker-compose.pid

ExecStart=/usr/local/bin/docker-compose -f /home/data/docker-compose.yml up -d.
ExecStop=/usr/local/bin/docker-compose down

TimeoutStartSec=0

[Install]
WantedBy=multi-user.target


2. create file /usr/lib/tmpfiles.d/docker-compose.conf

d /var/run/docker-compose 0755 root root -

3. Make directory /var/run/docker-compose

4. Set up systemctl 

systemctl status docker-compose
systemctl enable docker-compose
systemctl -l status docker-compose
systemctl start docker-compose 

