# MyMemoDockerEngineUbuntu

แหล่งที่มา : https://docs.docker.com/engine/install/

ข้อมูลการติดตั้ง : [ติดตั้ง Docker Engine บน Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

**ข้อกำหนดเบื้องต้น**

ความต้องการของระบบปฏิบัติการ

ในการติดตั้ง Docker Engine คุณต้องมี Ubuntu 64 Bit ต่อไปนี้ :

- Ubuntu Hirsute 21.04
- Ubuntu Focal 20.04 (LTS)
- Ubuntu Bionic 18.04 (LTS)
- Docker Engine is supported on x86_64 (or amd64), armhf, arm64, and s390x

ถอนการติดตั้งเวอร์ชันเก่า (ถ้ามี)
~~~
$ sudo apt-get remove docker docker-engine docker.io containerd runc
~~~

**วิธีการติดตั้ง**

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

File '/usr/share/keyrings/docker-archive-keyring.gpg' exists. Overwrite? (y/N) y
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
ตรวจสอบว่า Docker Engine ได้รับการติดตั้งอย่างถูกต้องโดยเรียกใช้ hello-world
~~~
$ sudo docker run hello-world

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
หมายเหตุ : ในกรณี ตรวจสอบ version docker แล้วระบบแจ้งว่า
~~~
docker --v

Command 'docker' not found, but can be installed with:

sudo snap install docker     # version 20.10.8, or
sudo apt  install docker.io  # version 20.10.7-0ubuntu1~20.04.2

See 'snap info docker' for additional versions.
~~~
ผมใช้คำสั่ง `sudo snap install docker` รอซักครู่
~~~
docker 20.10.8 from Canonical✓ installed
~~~
จากนั้นผมใช้คำสั่ง `sudo docker run hello-world`
~~~
sudo docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:37a0b92b08d4919615c3ee023f7ddb068d12b8387475d64c622ac30f45c29c51
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

หลังจากเสร็จสิ้นกระบวนการทำงาน Docker จะแสดงสถานะและแจ้งถึงสิ่งได้กระทำและคำแนะนำเบื้องต้น

ในการสร้างข้อความนี้ Docker ได้ทำตามขั้นตอนต่อไปนี้ :
 1. ไคลเอ็นต์ Docker ติดต่อกับ Docker daemon
 2. Docker daemon ดึงอิมเมจ "hello-world" จาก Docker Hub
    (amd64)
 3. Docker daemon สร้างคอนเทนเนอร์ใหม่จากอิมเมจนั้นซึ่งเรียกใช้
    ไฟล์เรียกทำงานที่สร้างเอาต์พุตที่คุณกำลังอ่านอยู่
 4. Docker daemon สตรีมเอาต์พุตนั้นไปยังไคลเอ็นต์ Docker ซึ่งส่งไป
    ไปยังเทอร์มินัลของคุณ

หากต้องการลองสิ่งที่มากกว่านี้ คุณสามารถเรียกใช้คอนเทนเนอร์ Ubuntu ด้วย : `docker run -it ubuntu bash`

คุณสามารถแชร์ images, automate workflows และอื่นๆ ด้วย Docker ID : สมัคร Docker ID ที่ https://hub.docker.com/ (มันฟรี)

_Note :_ gridseth2 Password มากกว่า 9 characters.

สำหรับตัวอย่างและแนวคิดเพิ่มเติมโปรดไปที่ : https://docs.docker.com/get-started/

**ติดตั้ง Docker Engine**

1. อัปเดต apt ดัชนีแพ็คเกจ : 
~~~
$ sudo apt-get update
~~~
ติดตั้ง Docker Engine เวอร์ชันล่าสุด และ คอนเทนเนอร์ :
~~~
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
~~~
_**หมายเหตุ :** หากคุณที่เก็บ Docker ที่เปิดใช้งานอยู่มากว่า 1 การติดตั้งหรืออัปเดตโดยไม่ระบุเวอร์ชันในคำสั่ง apt-get install หรือ apt-get update จะติดตั้งเวอร์ชันสูงสุดที่เป็นไปได้เสมอ ซึ่งอาจไม่เหมาะสมสำหรับความต้องการด้านความเสถียรของคุณ_

2. หากต้องการติดตั้งเวอร์ชันเฉพาะของ Docker Engine ให้ระบุเวอร์ชันที่มีใน repo จากนั้นเลือกและติดตั้ง :

คำสั่งนี้จะแสดงรายการเวอร์ชันที่เราสามารถใช้งานได้ :
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
ติดตั้งเวอร์ชันเฉพาะโดยใช้สตริงเวอร์ชันจากคอลัมน์ที่สอง เช่น 5:18.09.1~3-0~ubuntu-xenial

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
