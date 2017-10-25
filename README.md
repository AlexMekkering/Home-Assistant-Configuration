# Home-Assistant-Configuration
My main Home Assistant configuration

# Installation instructions

## Installation of required Arch Linux packages
```bash
sudo pacman -Syu --needed git python gcc sed grep autoconf automake make
```
## Creation of an unprivileged user

```bash
sudo useradd -m -r -G uucp homeassistant
```

##  Setting up Python virtualenv
```bash
sudo -iu homeassistant

python -m venv venv
. venv/bin/activate
pip install -U homeassistant
exit
```

## Start Home Assistant and enable at system startup

### Create a systemd service
```bash
sudo tee -a /etc/systemd/system/homeassistant.service > /dev/null <<EOF
[Unit]
Description=Home Assistant

[Service]
Type=simple
User=homeassistant
ExecStart=/home/homeassistant/venv/bin/hass -c "/home/homeassistant/.homeassistant"
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF
```

### Start and enable the service
```bash
sudo systemctl enable --now homeassistant
```
