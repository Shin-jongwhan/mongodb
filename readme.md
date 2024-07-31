### 240731
## MongoDB
### <br/><br/><br/>

# 참고
### 아래 블로그들을 참고하였다.
- [몽고db 정말 잘 정리된 블로그](https://pycoding.tistory.com/entry/%EB%AA%BD%EA%B3%A0db-%EC%A0%95%EB%A7%90-%EC%9E%98-%EC%A0%95%EB%A6%AC%EB%90%9C-%EB%B8%94%EB%A1%9C%EA%B7%B8])
- [Ubuntu MongoDB GPG 오류 해결](https://whackur.tistory.com/152)
### <br/><br/><br/>

# 설치
### 나는 리눅스 기반으로 진행하였다.
### 우분투 Ubuntu 18.04.6 LTS 버전
### 
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 68818C72E52529D4
sudo apt update -y
sudo apt-get install -y mongodb-org
```
### <br/>

### 설치 확인
#### ![image](https://github.com/user-attachments/assets/1b544216-9320-4206-a813-49207e01ef0c)
### <br/>

### service start
```
sudo service mongod start
```
### <br/>

### service start 확인
```
cat /var/log/mongodb/mongod.log
```
### <br/>

### mongodb 접속
```
mongo
```
#### ![image](https://github.com/user-attachments/assets/00325306-6c71-412d-b233-b7084380f539)
### <br/><br/><br/>

# 데이터베이스 사용하기
### mongodb에 접속한 다음 먼저 데이터베이스를 생성한다.
```
use tutorial
```
#### ![image](https://github.com/user-attachments/assets/cb286ce8-003d-49aa-9a49-90baaf7ca3ea)

### <br/>

### 데이터베이스 리스트 확인
### 그런데 아직 데이터베이스가 보이지 않는다. 왜냐하면 ducument(key, value pair로 이루어진 하나의 단위)가 없기 때문이다.
```
show dbs
```
#### ![image](https://github.com/user-attachments/assets/b53feb7e-d207-4f59-960c-a9e002b36692)
### <br/>

### ducument를 하나 생성해준다.
```
db.book.insert({"name": "MongoDB Tutorial", "author": "jhshin"});
```
#### ![image](https://github.com/user-attachments/assets/ac7e4bc7-9adb-4f98-97a1-91c2e0adfc71)
### <br/>

### 데이터베이스 제거
### use를 먼저 쓰고 써야 한다.
```
use tutorial
db.dropDatabase();
```
#### ![image](https://github.com/user-attachments/assets/b4c58c37-b1ee-425b-ad77-794835984ead)
### <br/>

### collection 생성
### db.createCollection(name, \[options\])
```
db.createCollection("books")
```
### 옵션에는 다음과 같은 값들이 들어갈 수 있다.
| Field     | Type    | 설명                                                                                                                                                                                                                                        |   |   |   |   |
|-----------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|---|---|---|
| capped    | Boolean | 이 값을 true 로 설정하면 capped collection 을 활성화 시킵니다. Capped collection 이란, 고정된 크기(fixed size) 를 가진 컬렉션으로서, size 가 초과되면 가장 오래된 데이터를 덮어씁니다. 이 값을 true로 설정하면 size 값을 꼭 설정해야합니다. |   |   |   |   |
| autoIndex | Boolean | 이 값을 true로 설정하면, _id 필드에 index를 자동으로 생성합니다. 기본값은 false 입니다.                                                                                                                                                     |   |   |   |   |
| size      | number  | Capped collection 을 위해 해당 컬렉션의 최대 사이즈(maximum size)를 ~ bytes로 지정합니다.                                                                                                                                                   |   |   |   |   |
| max       | number  | 해당 컬렉션에 추가 할 수 있는 최대 갯수를 설정합니다.                                                                                                                                                                                       |   |   |   |   |
| max       | number  | 해당 컬렉션에 추가 할 수 있는 최대 갯수를 설정합니다.    

