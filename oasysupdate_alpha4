#!/bin/bash
exists()
{
  command -v "$1" >/dev/null 2>&1
}
if exists curl; then
echo ''
else
  sudo apt update && sudo apt install curl -y < "/dev/null"
fi
bash_profile=$HOME/.bash_profile
if [ -f "$bash_profile" ]; then
    . $HOME/.bash_profile
fi
sleep 1 && curl -s https://raw.githubusercontent.com/exfeddix17/luckyteam/main/luckyteam.sh | bash && sleep 1

systemctl stop oasysd
sleep 3
cd $HOME
wget -O geth-v1.0.0-alpha4-linux-amd64.zip https://github.com/oasysgames/oasys-validator/releases/download/v1.0.0-alpha4/geth-v1.0.0-alpha4-linux-amd64.zip
unzip -o geth-v1.0.0-alpha4-linux-amd64.zip
sudo mv geth /usr/local/bin/geth
wget -O genesis.zip https://github.com/oasysgames/oasys-validator/releases/download/v1.0.0-alpha4/genesis.zip
unzip -o genesis.zip
mv genesis/testnet.json /home/geth/genesis.json
rm -rf /home/geth/.ethereum/geth
sudo -u geth geth init /home/geth/genesis.json
echo '[ "enode://4a85df39ec500acd31d4b9feeea1d024afee5e8df4bc29325c2abf2e0a02a34f6ece24aca06cb5027675c167ecf95a9fc23fb7a0f671f84edb07dafe6e729856@35.77.156.6:30303" ]' > /home/geth/.ethereum/geth/static-nodes.json
systemctl restart oasysd
sleep 3
echo "==================================================="
echo -e '\n\e[42mCheck node status\e[0m\n' && sleep 1
if [[ `service oasysd status | grep active` =~ "running" ]]; then
  echo -e "Your Oasys node \e[32mupdated and works\e[39m!"
  echo -e "You can check node status by the command \e[7mservice oasysd status\e[0m"
  echo -e "Press \e[7mQ\e[0m for exit from status menu"
else
  echo -e "Your Oasys node \e[31mwas not installed correctly\e[39m, please reinstall."
fi
