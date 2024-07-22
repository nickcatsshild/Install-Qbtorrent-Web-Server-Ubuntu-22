# install-Qbtorrent-Web-Server-Ubuntu-22
Instalação do Qb Torrent no servidor Ubuntu Server 22

Installation

sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt update
sudo apt install qbittorrent-nox

qBittorrent-nox (without X) is meant to be controlled via its Web UI which is accessible as a default at http://localhost:8080. The Web UI access is secured and the default account username is admin with adminadmin as default password…
Systemd service

Create a systemd service file for qBittorrent-nox that restart it automatically on system reboot:

sudo nano /etc/systemd/system/qbittorrent-nox.service

[Unit]
Description=qBittorrent-nox
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080
Restart=on-failure

[Install]
WantedBy=multi-user.target

If there’s another service running on port 8080, just change to another available port and set the -d --web-port=xxxx accordingly.

Then run following commands to enable and start this service:

sudo systemctl daemon-reload
sudo systemctl enable qbittorrent-nox
sudo systemctl start qbittorrent-nox

Check its running status by;

sudo systemctl status qbittorrent-nox

Nginx proxy

Following location directive should enough;

location / {
    proxy_redirect     off;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection "upgrade";
    proxy_set_header   Host $host;
    proxy_set_header   X-Real-IP $remote_addr;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass         http://localhost:8080; # qBittorrent-nox running port
}

You can proxy it to sub locations as well.

Now you can access qBittorrent-nox Web UI with your settings, don’t forget to change the default password in the Web UI… 😎
