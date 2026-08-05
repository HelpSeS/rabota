# rabota
# Мой проект
#!/bin/bash

sudo apt install libxcb-xinerama0
PACKAGE_1="bzsenagent"
if eval "sudo dpkg -s $PACKAGE_1>/dev/null 2>&1"
then 
echo "\033[37;1;42m Пакет '$PACKAGE_1' установлен в системе. \033[0m"
else
echo "Пакет '$PACKAGE_1' не установлен, идет процесс установки"
sudo dpkg -i bz_sensors_agent-sbautotech-32a0fb6e.soc.bi.zone-v2.23.2-plain-2025.10.09T21-09-3.deb
echo ""
fi

PACKAGE_2="klnagent64"
if eval "sudo dpkg -s $PACKAGE_2>/dev/null 2>&1"
then
echo "\033[37;1;42m Пакет '$PACKAGE_2' установлен в системе. \033[0m"
else
echo "Пакет '$PACKAGE_2' не установлен, идет процесс установки"
sudo dpkg -i klnagent64_15.4.0-8873_amd64.deb
sudo /opt/kaspersky/klnagent64/lib/bin/setup/postinstall.pl
echo ""
fi

PACKAGE_3="kesl11"
if eval "sudo dpkg -s $PACKAGE_3>/dev/null 2>&1"
then 
echo "\033[37;1;42m Пакет '$PACKAGE_3' установлен в системе. \033[0m"
else
echo "Пакет '$PACKAGE_3' не установлен, идет процесс установки"
sudo dpkg -i kesl_12.4.0-1225_amd64.deb
sudo /opt/kaspersky/kesl/bin/kesl-setup.pl
sudo dpkg -i kesl-gui_12.4.0-1225_amd64.deb
echo ""
fi

if [ "$SKIP_PACKAGES_UPDATE" != "true" ]; then
  sudo apt update -y || true
fi
sudo rm -f /tmp/rudesktop-amd64.deb
wget --no-check-certificate https://desk.navio.auto/download/rudesktop-amd64.deb -O /tmp/rudesktop-amd64.deb

if [ "$SKIP_SERVER_SETUP" = "true" ]; then
  sudo -H apt install -fy /tmp/rudesktop-amd64.deb
else
  sudo -H RUDESKTOP_DOMAIN=desk.navio.auto apt install -fy /tmp/rudesktop-amd64.deb
fi

pkill -xf "rudesktop|/usr/bin/rudesktop" || true

sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb

sudo dpkg -i cpyvpn-1.6.3.deb

#sudo dpkg -i AnyDesk_Custom_Client.deb

sudo dpkg -i google-chrome-stable_current_amd64.deb

sudo dpkg -i mattermost-desktop_5.12.0-1_amd64.deb

sudo dpkg -i ktalk3.3.0amd64.deb

sudo apt --fix-broken install

export AGENT_SERVER_HOSTS=https://10.100.127.200:4444
export SOFTWARE_CENTER_HOSTS=https://10.100.127.200:9400

sudo -E apt install /home/sargeras/Downloads/Linux_domain/linux-agent-4.6.0.96.ubuntu22.04.deb

sudo apt install curl

sudo lpadmin -p AT_Printum -L "Printer Location" -E -v ipp://10.100.127.7:1631/printers/Printum -m drv:///sample.drv/generic.ppd
