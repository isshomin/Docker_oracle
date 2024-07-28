# 🐳 Docker 🐳 
-------------------
&nbsp;
&nbsp;
<details>
  <summary>  <h2 style="font-size: 30px;"> Docker Oracle 연동 하기 전 Test❗❗ </h2> </summary>
&nbsp;
1. **Docker 설치 후 로그인(docker hub의 id/pw)**
   
        1-1. 사용자를 Docker 그룹에 포함(sudo 생략 가능)
    
        1-2. sudo apt install -y(모든질문 yes) docker.io
    
2. **Docker 설치 확인**
    ```bash
    docker --version
    ```
    
3. **Docker image 확인**
    ```bash
    docker images
    ```
    
4. **Docker container 확인**
    ```bash
    docker ps -a
    ```
    
5. **Docker hub에서 nginx 존재 여부 확인**
    
    
6. **nginx 명령어로 이미지 다운로드**
    ```bash
    docker pull <image_name>
    ```
    
7. **다운로드 이미지 검색**
    ```bash
    docker images
    ```
    
8. **이미지로 사용 가능한 서버 구축(컨테이너 생성)**
    ```bash

    docker run --name <name> -d -p <port_forwarding> <image_name>
    ```
    
9. **tomcat run 명령어로 다운로드 및 설치, 실행**
    
    ```bash
    $docker run --name <name> -d -p <port_forwarding> <image_name>
    ```
    
10. **Docker 실행 중인 컨테이너 확인**
    ```bash
    $docker ps
    ```
    
11. **컨테이너 리스트 확인**
    ```bash
    $docker ps -a
    ```
    
12. **이미지 확인**
    
    
13. **curl 명령어로 tomcat 서버에 접속**
    ```bash
    $curl http://127.0.0.1:8081
    ```
    
14. **tomcat과 nginx 컨테이너 자체의 os 접속 및 종류 확인**
```bash
$docker exec -it <container_id> bash
```

</details>
&nbsp;
&nbsp;

## Oracle ver.xe-11g 설치 및 실행 💻

- **oracle 8버전은 유료라서 진행이 안됨 따라서, 교육용 11버전을 다운 받아야 한다**
- **docker search oracle-xe-11g로 xe11버전을 찾는다**

<p align="left"><img src="https://github.com/user-attachments/assets/83d8b8b7-86fb-4ad1-9a30-6190d469c1ce"></p><br>

- **docker pull oracleinanutshell/oracle-xe-11g로 image를 다운로드 받는다**<br>

```bash
$docker run -- name oracle -d -p 1521:1521 oracleinanutshell/oracle-xe-11g
```
//-d demon실행, -p 포트포워딩
<p align="left"><img src="https://github.com/user-attachments/assets/30309ecc-bd4a-4d1d-a151-440e4fc4af88"></p><br>

- **docker exec -it <container_id> bash 로 oracle bash 설정으로 이동**<br>
```bash
$docker exec -it 96cca020aa30 bash
```
<p align="left"><img src="https://github.com/user-attachments/assets/d5c032a9-47f8-4993-9f23-69a844d8784e"></p><br>
    
- **sqlplus 입력 후 ip/pw: system/oracle 입력 후 connected 뜨면 성공**<br>
<p align="left"><img src="https://github.com/user-attachments/assets/9230c3f1-334d-4873-85d1-c46e3bd0883b"></p><br>

 __<h2 style="font-size: 30px;">system 계정 사용하면 안되서 계정을 생성을 해야 한다</h2><br>__

 + __일반 계정 생성 (id scott / pw tiger)__<br>
```bash
SQL> create user scott identified by tiger;
```

 + __scott 계정 관리 권한부여__<br>
```bash
SQL> grant connect, resource, dba to scott;
```

 + __현 로그인 계정에서 scott 계정으로 명령창에서 바로 갈아타기__<br>
```bash
SQL> connect scott/tiger
```
<br>
<p align="left"><img src="https://github.com/user-attachments/assets/ea1181be-9948-424e-952e-0b8370054503"></p><br>


## Ubuntu 🐧내의 Docker 🐋 와 Dbeaver 🦦 연동🔗🔗<br>

- **Dbeaver의 navigator 창에 우클릭 후 connection 생성 후 oracle 선택**<br>

<p align="left"><img src="https://github.com/user-attachments/assets/f6b6d8d7-8966-4f76-b589-a90ee9e490bb"></p><br>
    

- **SSH 설정** ⚙️
    
    
    | Host/IP | 127.0.0.1 |
    | --- | --- |
    | User Name | username |
    | Password | ubuntu |
    | Test tunnel configuration |  |
    
    <p align="left"><img src="https://github.com/user-attachments/assets/651927c1-13ff-4374-951b-2c76419f7f5b"></p><br>
    

- ➕**Main 포트포워딩 설정**➕
    
    
    | Database | xe |
    | --- | --- |
    | Username | scott |
    | Password | tiger |

<p align="left"><img src="https://github.com/user-attachments/assets/90d27e26-973f-4e55-8581-353524f16e23"></p><br>


__<h2 style="font-size: 30px;">virtualbox 용량 부족 이슈 해결 방법 📒</h2>__
  ```bash
  sudo lvextend -L +10G /dev/mapper/ubuntu--vg-ubuntu--lv
  #논리볼륨 10GB 추가
  sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
  #ext파일 시스템 크기 확장
  ```


  # [Notion Link](https://immediate-scarer-1a0.notion.site/Docker-67b5f3946c0349fbbc56f177c804f8c9)
