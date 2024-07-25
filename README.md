# 🐳 Docker 🐳

### Docker Oracle 연동 하기 전 Test

1. **Docker 설치 후 로그인(docker hub의 id/pw)**
    1. 사용자를 Docker 그룹에 포함(sudo 생략 가능)
    2. sudo apt install -y(모든질문 yes) docker.io
    
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
    docker pull 이미지이름
    ```
    
7. **다운로드 이미지 검색**
    
    ```bash
    docker images
    ```
    
8. **이미지로 사용 가능한 서버 구축(컨테이너 생성)**
    
    ```bash
    docker run --name 고유한이름 -d -p 포트포워딩 이미지명
    ```
    
9. **tomcat run 명령어로 다운로드 및 설치, 실행**
    
    ```bash
    $docker run --name 고유한이름 -d -p 포트포워딩 이미지명
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
$docker exec -it 컨테이너id bash
```

## Oracle ver.xe-11g 설치 및 실행 💻

- **oracle 8버전은 유료라서 진행이 안됨 따라서, 교육용 11버전을 다운 받아야 한다**
- **docker search oracle-xe-11g로 xe11버전을 찾는다**

![docker써치.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/docker%25EC%258D%25A8%25EC%25B9%2598.png)

- **docker pull oracleinanutshell/oracle-xe-11g로 image를 다운로드 받는다**

- **docker run** --**name oracle -d(백그라운드실행) -p(포트설정) 1521:1521 oracleinanutshell/oracle-xe-11g**

![docker런.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/docker%25EB%259F%25B0.png)

- **docker exec -it <container_id> bash 로 oracle bash 설정으로 이동**
    
    ![dock배쉬.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/dock%25EB%25B0%25B0%25EC%2589%25AC.png)
    

- **sqlplus 입력 후 ip/pw: system/oracle 입력 후 connected 뜨면 성공**

![plus접속.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/plus%25EC%25A0%2591%25EC%2586%258D.png)

- system 계정 사용하면 안되서 계정을 생성을 해야 함

```bash
-- 일반 계정 생성 : id scott / pw tiger
SQL> create user scott identified by tiger;
User created.

-- scott 계정 관리 권한
SQL> grant connect, resource, dba to scott;
Grant succeeded.

-- 현 로그인 계정에서 scott 계정으로 명령창에서 바로 갈아타기
SQL> connect scott/tiger
Connected.
```

![계정생성.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/%25EA%25B3%2584%25EC%25A0%2595%25EC%2583%259D%25EC%2584%25B1.png)

## Ubuntu 🐧내의 Docker 🐋 와 Dbeaver 🦫 연동🔗🔗

- **Dbeaver의 navigator 창에 우클릭 후 connection 생성 후 oracle 선택**
    
    ![디비버커넥.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/%25EB%2594%2594%25EB%25B9%2584%25EB%25B2%2584%25EC%25BB%25A4%25EB%2584%25A5.png)
    

- **SSH 설정** ⚙️
    
    
    | Host/IP | 127.0.0.1 |
    | --- | --- |
    | User Name | username |
    | Password | ubuntu |
    | Test tunnel configuration |  |
    
    ![ssh디비버.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/ssh%25EB%2594%2594%25EB%25B9%2584%25EB%25B2%2584.png)
    

- 🪢**Main 포트포워딩 설정**🪢
    
    
    | Database | xe |
    | --- | --- |
    | Username | scott |
    | Password | tiger |

![오라클메인.png](%F0%9F%90%B3%20Docker%20%F0%9F%90%B3%2067b5f3946c0349fbbc56f177c804f8c9/%25EC%2598%25A4%25EB%259D%25BC%25ED%2581%25B4%25EB%25A9%2594%25EC%259D%25B8.png)

- **virtualbox 용량 부족 이슈 해결 방법** 📒
    
    ```bash
    sudo lvextend -L +10G /dev/mapper/ubuntu--vg-ubuntu--lv
    //논리볼륨 10GB 추가
    sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
    //ext파일 시스템 크기 확장
    ```