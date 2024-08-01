### 240801
## 외부 접속 허용 방법
### mongosh라는 프로그램으로 접속 가능하며, mongodb에서 공식적으로 지원하는 프로그램이다.
### <br/><br/><br/>

## 설정
### 아래 파일을 열고 접속 ip 범위를 수정한다.
### 접속 ip, port에 대한 것은 방화벽에서 처리한다.
```
vi /etc/mongod.conf
```
#### ![image](https://github.com/user-attachments/assets/ab1e680c-5cf3-4493-a7d3-d3f36d7e1e29)
### <br/><br/><br/>

## 설치
### 아래 공식 웹사이트에 있는 걸 그대로 따라하면 설치된다.
### [mongosh 설치 방법](https://www.mongodb.com/ko-kr/docs/mongodb-shell/install/)
### <br/><br/><br/>

## 접속
### mongodb의 기본 포트는 27017이다.
```
mongosh mongodb://[ip_address]
```
### <br/>

### 외부 서버에서 접속을 확인한다.
#### ![image](https://github.com/user-attachments/assets/f8a8db72-e072-41de-8e1a-fb3e50cae4af)
