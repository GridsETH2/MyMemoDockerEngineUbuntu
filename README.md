# MyMemo Docker Basic on ubuntu

แหล่งที่มา : https://docs.docker.com/engine/install/

ข้อมูลการติดตั้ง : [ติดตั้ง Docker Engine บน Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

**ข้อกำหนดเบื้องต้น**

ความต้องการของระบบปฏิบัติการ

ในการติดตั้ง Docker Engine คุณต้องมี Ubuntu 64 Bit ต่อไปนี้ :

- Ubuntu Hirsute 21.04
- Ubuntu Focal 20.04 (LTS)
- Ubuntu Bionic 18.04 (LTS)
- Docker Engine is supported on x86_64 (or amd64), armhf, arm64, and s390x

_**Note** : กรณีผมใช้ Ubuntu Focal 20.04 (LTS)_

ถอนการติดตั้งเวอร์ชันเก่า (ถ้ามี)
~~~
$ sudo apt-get remove docker docker-engine docker.io containerd runc
~~~

## Set up the repository

คุณสามารถติดตั้ง Docker Engine ได้หลายวิธี ขึ้นอยู่กับความต้องการของคุณ แต่สำหรับผมในขั้นตอนนี้ผมจะติดตั้งโดยใช้ที่เก็บเนื่องจากอนาคตอาจมีการเปลี่ยนแปลงสถานที่ทำงาน

**ติดตั้งโดยใช้ที่เก็บ** ก่อนที่คุณจะติดตั้ง Docker Engine เป็นครั้งแรกบนเครื่องโฮสต์ใหม่ คุณต้องตั้งค่าที่เก็บ Docker ก่อน หลังจากนั้นคุณจึงจะสามารถติดตั้งและอัปเดต Docker จากที่เก็บได้

**ตั้งค่าที่เก็บ**

1. อัพเดตaptดัชนีแพ็คเกจและติดตั้งแพ็คเกจเพื่ออนุญาตให้aptใช้ที่เก็บผ่าน HTTPS :
~~~
$ sudo apt-get update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
~~~
2. เพิ่มคีย์ GPG อย่างเป็นทางการของ Docker :
~~~
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
~~~
3. ใช้คำสั่งต่อไปนี้เพื่อตั้งค่าพื้นที่เก็บข้อมูลที่มีเสถียรภาพ หากต้องการเพิ่มพื้นที่เก็บข้อมูลทุกคืน หรือ ทดสอบ ให้เพิ่มคำ nightly หรือ test (หรือทั้งสองอย่าง) หลังคำ stable ในคำสั่งด้านล่าง 

หมายเหตุ : lsb_release -cs คำสั่งย่อยด้านล่าง จะส่งคืนชื่อการแจกจ่าย Ubuntu ของคุณ เช่น xenial. 

บางครั้ง ในการแจกจ่ายเช่น Linux Mint คุณอาจต้องเปลี่ยน $(lsb_release -cs) เป็นการแจกจ่าย Ubuntu Master ของคุณ ตัวอย่างเช่น หากคุณใช้ Linux Mint Tessa คุณสามารถใช้ bionic. 

docker ไม่ได้ให้การรับประกันใดๆ เกี่ยวกับการแจกแจงของ Ubuntu ที่ยังไม่ทดสอบและไม่รองรับ
~~~
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable nightly test" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
~~~
## Install Docker Engine
~~~
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
~~~
ตรวจสอบเวอร์ชั่น Docker
~~~
$ sudo docker version
~~~
Report : 
~~~
$ sudo docker version

Client: Docker Engine - Community
 Version:           20.10.14
 API version:       1.41
 Go version:        go1.16.15
 Git commit:        a224086
 Built:             Thu Mar 24 01:48:02 2022
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.14
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.15
  Git commit:       87a90dc
  Built:            Thu Mar 24 01:45:53 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.5.11
  GitCommit:        3df54a852345ae127d1fa3092b95168e4a88e2f8
 runc:
  Version:          1.0.3
  GitCommit:        v1.0.3-0-gf46b6ba
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
~~~
ทดสอบ `run hello-world`
~~~
$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:10d7d58d5ebd2a652f4d93fdd86da8f265f5318c6a73cc5b6a9798ff6d2b2e67
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
~~~

## เพิ่มเติม

คุณสามารถแชร์ images, automate workflows และอื่นๆ ด้วย Docker ID : สมัคร Docker ID ที่ https://hub.docker.com/ (มันฟรี)

_**Note** : gridseth2 Password มากกว่า 9 characters._

_**Note** : สำหรับตัวอย่างและแนวคิดเพิ่มเติมโปรดไปที่ : https://docs.docker.com/get-started/_

_**Note** : หากคุณที่เก็บ Docker ที่เปิดใช้งานอยู่มากว่า 1 การติดตั้งหรืออัปเดตโดยไม่ระบุเวอร์ชันในคำสั่ง apt-get install หรือ apt-get update จะติดตั้งเวอร์ชันสูงสุดที่เป็นไปได้เสมอ ซึ่งอาจไม่เหมาะสมสำหรับความต้องการด้านความเสถียรของคุณ_

_**Note** : หากต้องการติดตั้งเวอร์ชันเฉพาะของ Docker Engine ให้ระบุเวอร์ชันที่มีใน repo จากนั้นเลือกและติดตั้ง :_

- คำสั่งนี้จะแสดงรายการเวอร์ชันที่เราสามารถใช้งานได้ :
~~~
$ apt-cache madison docker-ce
~~~
ผลลัพธในปัจจุบัน
~~~
 docker-ce | 5:20.10.10~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.10~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.10~2.1.rc1-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.9~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.9~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.8~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.8~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.7~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.7~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.6~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.6~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.5~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.5~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.4~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.4~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.3~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.3~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.2~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.2~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.1~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.1~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.0~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:20.10.0~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.0~2.2.rc2-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.0~2.1.rc1-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:20.10.0~1.1.beta1-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.15~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.15~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.14~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.14~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.13~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.13~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.13~1.2.beta2-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.12~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.12~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.11~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.11~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.10~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.10~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
 docker-ce | 5:19.03.9~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
 docker-ce | 5:19.03.9~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/test amd64 Packages
~~~
ติดตั้งเวอร์ชันเฉพาะโดยใช้สตริงเวอร์ชันจากคอลัมน์ที่สอง เช่น 5:18.09.1-3-0-ubuntu-xenial

ผมจะใช้เวอร์ชันล่าสุดที่มีอยู่ตอนนี้ที่ผมสามารถใช้ได้ `5:20.10.10~3-0~ubuntu-focal` 

รูปแบบคำสั่ง
~~~
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
~~~
ตัวอย่าง
~~~
sudo apt-get install docker-ce=5:20.10.10~3-0~ubuntu-focal docker-ce-cli=5:20.10.10~3-0~ubuntu-focal containerd.io
~~~

ตรวจสอบอีกครั้งว่า Docker Engine ได้รับการติดตั้งอย่างถูกต้องโดยเรียกใช้ hello-world ด้วยคำสั่ง `sudo docker run hello-world`

ถ้าไม่มีข้อผิดพลาดใดๆ และผลที่ได้เหมือนกับการทดสอบในครั้งแรก เราก็จะเสร็จสิ้นกระบวนการ การติดตั้งที่เก็บ Docker Engine บน Ubuntu
#
## ถอนการติดตั้ง Docker Engine
1. ถอนการติดตั้งแพ็คเกจ Docker Engine, CLI และ Containerd :
~~~
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io
~~~
2. ลบ images คอนเทนเนอร์ และวอลุ่มทั้งหมด
~~~
$ sudo rm -rf /var/lib/docker
$ sudo rm -rf /var/lib/containerd
~~~
#
## Error
Error เมื่อ update ubuntu
~~~
Err:1 https://download.docker.com/linux/ubuntu focal InRelease The following signatures couldn't be verified because the public key is not av
~~~
แก้ด้วย
~~~
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
~~~
