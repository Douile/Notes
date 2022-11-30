# Find up hosts (fast)
```shell
sudo nmap -sn -PP -T5 192.168.0.0/24
```
[Explanation](https://explainshell.com/explain?cmd=sudo+nmap+-sn+-PP+-T5+192.168.0.0%2F24)
- -sn = ping scan only
- -PP = ? do I actually need icr why I added

# Find local ssh servers
```shell
sudo nmap -Pn -p 22 -sS -sV -T5 --open 192.168.0.0/24
```
[Explanation](https://explainshell.com/explain?cmd=sudo+nmap+-Pn+-p+22+-sS+-sV+-T+--open+192.168.0.0%2F24)
- sudo required for -sS
- 192.168.0.0/24 - Ip range to scan
- -Pn don't ping to check hosts up

# Rootless TCP scan
```shell
nmap -sT -sV -T5 -p 22,80,443 192.168.0.1
```
[Explanation](https://explainshell.com/explain?cmd=nmap+-sT+-sV+-T5+-p+22%2C80%2C443+192.168.0.1)
