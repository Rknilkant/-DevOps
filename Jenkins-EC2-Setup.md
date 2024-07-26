
# Installing Jenkins in EC2 

Steps To Install:



## Installing JDK

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```

## Installing LTS Version



```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
## Start Jenkins

```bash
sudo systemctl enable jenkins
```
```bash
sudo systemctl start jenkins
```
```bash
sudo systemctl status jenkins
```
## If Jenkins Is Not Starting Then:

```bash
sudo systemctl stop jenkins
```
## Step-by-Step Guide to Change Jenkins Port
```bash
sudo systemctl enable jenkins
```
## Edit Jenkins Configuration File:
```bash
sudo vi /etc/default/jenkins
```
### Change the line:

```bash
HTTP_PORT=7001
```
## Edit Jenkins Systemd Service File (if necessary):
```bash
sudo vi /lib/systemd/system/jenkins.service
```
## Reload systemd daemon
```bash
sudo systemctl daemon-reload
```
## Restart Jenkins Service:
```bash
sudo systemctl start jenkins
```
```bash
sudo systemctl status jenkins
```
## Open The Port In AWS Console

By editing inbound rule and adding 7001 to TCP
