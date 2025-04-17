# Monitor System Resources Using Netdata

## 1. Launch an EC2 Instance
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/f8c7e80c12fa7bcff75ea7946c33a4222877baf3/images/1.JPG)

## 2. Connect the Instance and Update it
```bash
sudo apt-get update
```
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/f8c7e80c12fa7bcff75ea7946c33a4222877baf3/images/2.JPG)

## 3. Install Docker using `Shell` Script
```bash
nano docker.sh     # `ctrl+s` to save the file, `ctrl+x` to exit the nano editor mode
-------------------
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo apt-get install docker-compose -y
sudo usermod -aG docker ubuntu
sudo chmod 777 /var/run/docker.sock
newgrp docker
sudo systemctl status docker
-----------------------
bash docker.sh
docker --version
docker-compose --version
```
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/f8c7e80c12fa7bcff75ea7946c33a4222877baf3/images/3.JPG)

## 4. Launch `Netdata` as a Docker container
```bash
docker run -d \
  --name=netdata \
  -p 19999:19999 \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  --restart unless-stopped \
  netdata/netdata
docker ps  # To check running container 
```
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/f8c7e80c12fa7bcff75ea7946c33a4222877baf3/images/4.JPG)

## 5. Now access the `Netdata` dashboard using `Publi IP` of base machine on Port `19999`
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/8bfe6f187a0dd635f4a8ea5c65b6c0d409fb4ccd/Netdata_Screenshots/SS1.JPG)

## 6. Screenshots of the `Netdata` dashboard is given below ---

* Metrics = System
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/3efa9dfaa2c60f3ae3d9a12779978c6c28d553f7/Netdata_Screenshots/SS2.JPG)

* Metrics = CPU
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS3.JPG)


* Metrics = Memory
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS4.JPG)

* Metrics = RAM
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS5.JPG)

* Metrics = Hardware
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS6.JPG)

* Metrics = Disk(I/O)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS7.JPG)

* Metrics = Disk(IOPS)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS8.JPG)

* Metrics = Disk(Latency)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS9.JPG)

* Metrics = Disk(Utilization)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS10.JPG)

* Metrics = Mount Points
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS11.JPG)

* Metrics = Docker
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS12.JPG)

* Metrics = Docker(Summary)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS13.JPG)

* Metrics = Docker(Containers)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS14.JPG)

* Metrics = Docker(Health)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS15.JPG)

* Metrics = Docker(Images)
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS16.JPG)

* Alerts
![image alt](https://github.com/souravhajra123/ElevateLabsTask7/blob/b686183fc17918cf8b6ee678f43e0ce2fceeb086/Netdata_Screenshots/SS17.JPG)
