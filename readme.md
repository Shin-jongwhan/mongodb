### 240731
## MongoDB
### <br/><br/><br/>

# 참고
### 아래 블로그들을 참고하였다.
- [몽고db 정말 잘 정리된 블로그](https://pycoding.tistory.com/entry/%EB%AA%BD%EA%B3%A0db-%EC%A0%95%EB%A7%90-%EC%9E%98-%EC%A0%95%EB%A6%AC%EB%90%9C-%EB%B8%94%EB%A1%9C%EA%B7%B8)
- [Ubuntu MongoDB GPG 오류 해결](https://whackur.tistory.com/152)
### <br/>

### mongodb 공식 문서
- remove
  - https://www.mongodb.com/ko-kr/docs/manual/reference/method/db.collection.remove/
- collation
  - https://www.mongodb.com/ko-kr/docs/manual/reference/collation/
  - https://www.mongodb.com/ko-kr/docs/manual/reference/collation-locales-defaults/
- where query(javascript expression)
  - https://www.mongodb.com/ko-kr/docs/manual/reference/operator/query/where/
- elemMatch
  - https://www.mongodb.com/ko-kr/docs/manual/reference/operator/query/elemMatch/
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

-------------------------------------------------------------

# 데이터베이스 사용하기
### mongodb에 접속한 다음 먼저 데이터베이스를 생성한다.
```
use tutorial
```
#### ![image](https://github.com/user-attachments/assets/cb286ce8-003d-49aa-9a49-90baaf7ca3ea)

### <br/><br/><br/>

## 데이터베이스 리스트 확인
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
### <br/><br/><br/>

## 데이터베이스 제거
### use를 먼저 쓰고 써야 한다.
```
use tutorial
db.dropDatabase();
```
#### ![image](https://github.com/user-attachments/assets/b4c58c37-b1ee-425b-ad77-794835984ead)
### <br/><br/>

## collection 생성
### db.createCollection(name, \[options\])
### ex)
```
db.createCollection("books")
db.createCollection("articles", { capped: true, size: 6142800, max: 10000 })
```
#### ![image](https://github.com/user-attachments/assets/71917096-763f-419d-8e58-67297926b289)
### <br/>

### 옵션에는 다음과 같은 값들이 들어갈 수 있다.
#### * 참고로 autoIndex 옵션은 deprecated 되었다.
| Field     | Type    | 설명                                                                                                                                                                                                                                        |
|-----------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| capped    | Boolean | 이 값을 true 로 설정하면 capped collection 을 활성화 시킵니다. Capped collection 이란, 고정된 크기(fixed size) 를 가진 컬렉션으로서, size 가 초과되면 가장 오래된 데이터를 덮어씁니다. 이 값을 true로 설정하면 size 값을 꼭 설정해야합니다. |
| size      | number  | Capped collection 을 위해 해당 컬렉션의 최대 사이즈(maximum size)를 ~ bytes로 지정합니다.                                                                                                                                                   |
| max       | number  | 해당 컬렉션에 추가 할 수 있는 최대 갯수를 설정합니다.                                                                                                                                                                                       |
| max       | number  | 해당 컬렉션에 추가 할 수 있는 최대 갯수를 설정합니다.                                                                                                                                                                                       |
### <br/><br/><br/>

## collection 제거
### db.\[collection_name\].drop()
### 있으면 true, 없거나 실패하면 false를 출력한다.
```
db.articles.drop()
```
#### ![image](https://github.com/user-attachments/assets/64bd67a3-c643-4b4f-86d7-8c4dde924097)
### <br/><br/><br/>

## document 추가
### 한 row 추가하는 방법
```
db.books.insert({"name": "mongoDB tutorial", "author": "jhshin"})
```
### <br/>

### 여러 줄 추가하는 방법
```
db.books.insert(
  [
    {"name": "mongoDB tutorial", "author": "jhshin"},
    {"name": "mongoDB tutorial 2", "author": "jhshin"}
  ]
)
```
#### ![image](https://github.com/user-attachments/assets/13e471eb-1808-477c-b08f-e2f76bdad4a2)
### <br/><br/><br/>


## collection에서 특정 document 찾기(데이터 조회하기)
### db.\[collection_name\].find()로 찾는다.
### 전체를 찾고 싶다면 find() 안에 아무 것도 넣지 않으면 되고, 특정 조건으로 찾고 싶다면 json 형식으로 넣어주면 된다.
```
db.books.find();
db.books.find({"name":"mongoDB tutorial"});
```
#### ![image](https://github.com/user-attachments/assets/9727e5c6-8106-4c3e-a7fa-682f3bc60a9a)
### <br/><br/>

### 정렬 후 조회
### db.\[collection\].find().sort()를 사용한다.
### -1은 내림차순 정렬이다.
```
db.books.find().sort({"_id" : -1})
```
#### ![image](https://github.com/user-attachments/assets/e5bd129f-64e0-481e-8e31-e2386cfb402c)
### <br/><br/>

### 보기 좋게 출력하기
### db.\[collection\].find().pretty()
```
db.books.find().pretty()
```
#### ![image](https://github.com/user-attachments/assets/02ab2992-4698-49b4-9186-13270c0df901)
### <br/><br/>

### 출력할 때 사용하는 비교 연산자
| operator | 설명                                                   |
|----------|--------------------------------------------------------|
| $eq      | (equals) 주어진 값과 일치하는 값                       |
| $gt      | (greater than) 주어진 값보다 큰 값                     |
| $gte     | (greather than or equals) 주어진 값보다 크거나 같은 값 |
| $lt      | (less than) 주어진 값보다 작은 값                      |
| $lte     | (less than or equals) 주어진 값보다 작거나 같은 값     |
| $ne      | (not equal) 주어진 값과 일치하지 않는 값               |
| $in      | 주어진 배열 안에 속하는 값                             |
| $nin     | 주어빈 배열 안에 속하지 않는 값                        |
### <br/><br/>

### 비교 연산자 사용하여 출력하기 예시
### 다음의 예시 데이터를 insert 한다.
```
db.books.insert(
  [
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 1},
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 2}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 3}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 4}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 5}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 6}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 7}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 8}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 9}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 10}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 11}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 12}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 13}, 
  ]
)
```
### <br/>

### 아래와 같이 find 한다.
```
db.books.find({"num" : {$lte : 10}})
```
#### ![image](https://github.com/user-attachments/assets/d5769522-bc3d-41ea-af0a-65e3ae4cc183)
### <br/><br/>

### 논리 연산자
| operator | 설명                                   |
|----------|----------------------------------------|
| $or      | 주어진 조건중 하나라도 true 일 때 true |
| $and     | 주어진 모든 조건이 true 일 때 true     |
| $not     | 주어진 조건이 false 일 때 true         |
| $nor     | 주어진 모든 조건이 false 일때 true     |
### <br/>

### 논리 연산자를 사용할 때는 리스트 형태로 묶는다.
### 다음의 예시는 5 <= num <= 10인 조건을 찾는다.
```
db.books.find({$and : [{"num" : {$gte : 5}}, {"num" : {$lte : 10}}]})
```
#### ![image](https://github.com/user-attachments/assets/3f300893-5c73-443f-b825-7232798ad4b1)
### <br/>

### 특정 key만 조회(projection)
### 조건절 뒤에 {}로 조회할 key를 아래와 같이 작성한다.
```
db.books.find({}, {"num": true})
```
#### ![image](https://github.com/user-attachments/assets/09806d28-e92c-489c-bb9d-bef399d7e785)
### <br/><br/>

### 정규식 사용
### db.\[collection\].find({field : {$regex: '정규표현식'}})
### 숫자에는 적용이 안 되는 듯 하다. 아무래도 정규식이 문자열을 인식하는 거라서..
### 정규식 관련해서는 여러 참고자료가 있으니 다른 자료를 참고하도록 한다 !
```
db.books.find({"author" : {$regex:'^j'}})
db.books.find({"author" : {$regex:'[a-z]'}})
```
#### ![image](https://github.com/user-attachments/assets/ee26b1ae-4356-4233-8b0d-0b43c381a6d3)
### <br/><br/>

### where query
### javascript expression을 사용하여 검색하는 방법이다.
### elemMatch와 같이 쓸 수 없다.
### 특별한 경우 말고는 mongodb에서 지원하는 다른 문법(기능)들이 있으니 그런 것들을 쓸 것 같다.
### 그리고 javascript expression을 처리하기 위해서 별도의 인식과 프로세스가 들어간다고 공식 문서에 나와 있다. 아마 나중에는 deprecated 될 듯 하다.
#### ![image](https://github.com/user-attachments/assets/83f45212-719d-4f06-bc4d-31df4dd8cb66)
#### ![image](https://github.com/user-attachments/assets/a1f84646-3b20-41a1-9987-ec4766c15b11)
```
db.books.find({$where : "this.num === 1"})
db.books.find({$where : "this.author == \"jhshin\""})
```
#### ![image](https://github.com/user-attachments/assets/372e277c-6c7e-4e3c-b44c-b4cb7aeee90b)
### <br/><br/>

### elemMatch query
### 배열로 이루어진 것에 대한 검색이다.
### where과 같이 쓸 수 없다.
### <br/>

### 예제 collection
```
db.books.insert(
  [
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 1, "arr" : [1, 2, 3]},
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 2, "arr" : [3, 5, 9]}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 3, "arr" : [19, 20, 25]}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 4, "arr" : [1, 5, 10]}, 
    {"name": "mongoDB tutorial", "author": "jhshin", "num" : 5, "arr" : [10, 5, 3]}
  ]
)
```
#### ![image](https://github.com/user-attachments/assets/485cc9c0-26a4-45bd-b278-730432bfe84c)
### <br/>

### 배열에서 10 이상, 15이하인 항목이 하나나로 포함 되어 있으면 출력한다.
```
db.books.find({ arr : { $elemMatch : {$gte : 10, $lte : 15} } })
```
#### ![image](https://github.com/user-attachments/assets/795d9d53-0726-470c-8733-87fa7769bd18)
### <br/><br/>

### elemMatch를 projection에 사용해보기
### projection에 사용하면 배열에 존재하는 모든 element를 출력하지 않고, 해당하는 것만 출력해준다.
```
db.books.find({ arr : { $elemMatch : {$gte : 10, $lte : 15} } }, { arr : { $elemMatch : {$gte : 10, $lte : 15} } })
```
#### ![image](https://github.com/user-attachments/assets/26cb402f-dd6c-45ff-87a0-ff152d598584)
### <br/><br/>

### sort
### find 이후 데이터를 특정 기준으로 sort할 때 사용한다.
### db.\[collection\].find({condition}).sort({condition})와 같이 쓴다.
### <br/>

### id 기준으로 역순 ex) 
```
db.books.find().sort({"_id" : -1})
```
#### ![image](https://github.com/user-attachments/assets/60dbdf8a-ced3-4c39-870d-6c031185ba93)
### <br/><br/>

### limit
### RDBMS의 limit과 같다.
### db.\[collection\].find({condition}).limit(n)으로 사용한다.
### ex)
```
db.books.find().sort({"_id" : -1}).limit(1)
```
#### ![image](https://github.com/user-attachments/assets/e159bc10-4e81-47ff-ac14-6767115de84f)


### <br/><br/><br/>


## document 삭제
### db.\[collection_name\].remove(criteria, justOne)
### 전체 삭제
```
db.books.remove({})
```
#### ![image](https://github.com/user-attachments/assets/191ec02a-0c8d-4e7c-8725-4a5aa9eff85c)
### <br/>

### 일부 조건으로 삭제
```
db.books.remove({"name" : "mongoDB tutorial"})
```
#### ![image](https://github.com/user-attachments/assets/78528c3d-0d03-44c8-ae2e-1617984f2c45)
### <br/>

### 일부 조건, 맨 처음에 추가된 document 삭제
```
db.books.remove({"name" : "mongoDB tutorial"}, {justOne: true})
```
#### ![image](https://github.com/user-attachments/assets/a0458103-0673-4ab8-9d53-2451e9691677)
### <br/>

### 다른 옵션들도 있다.
```
db.collection.remove(
    <query>,
    {
      justOne: <boolean>,
      writeConcern: <document>,
      collation: <document>,
      let: <document> // Added in MongoDB 5.0
    }
)
```
#### ![image](https://github.com/user-attachments/assets/23b3d4f0-4ae4-48f2-9323-55c8ad4f031e)
### <br/>

### collation
### 데이터 정렬을 할 때 사용하며 locale은 필수로 사용해야 한다고 한다.
```
{
   locale: <string>,
   caseLevel: <boolean>,
   caseFirst: <string>,
   strength: <int>,
   numericOrdering: <boolean>,
   alternate: <string>,
   maxVariable: <string>,
   backwards: <boolean>
}
```
### collation locale 정보는 mongodb 공식 문서에 있다.
```
{ "locale" : "<locale code>@collation=<variant>" }
```
### 영어인 경우
```
{ "locale" : "en@collation=search" }
```
#### ![image](https://github.com/user-attachments/assets/6e2da9c7-e88b-48de-9d1a-a8873a61b06e)
#### ![image](https://github.com/user-attachments/assets/6dc9ebdc-e8a8-4207-b293-c70808248274)
### <br/>

### 맨 마지막에 추가된 document 삭제
### db.\[collection_name\].findOneAndDelete를 사용한다.
### 그리고 _id 기준으로 내림차순으로 정렬한 후 삭제한다.
```
db.books.findOneAndDelete({"name" : "mongoDB tutorial"}, {sort: { _id: -1 }})
```
#### ![image](https://github.com/user-attachments/assets/f7bd150d-d514-46ed-9ed5-aff8457a0d82)
#### ![image](https://github.com/user-attachments/assets/dbebac17-1311-4324-a097-d03d258f5d77)
### <br/><br/><br/>


## update
### mongodb의 update는 매우 좋은 것 같다. 여러가지 형식으로 document에 값을 수정, 추가, 삭제할 수 있다.
### <br/><br/>

### 여러 document에 key 추가하기
```
db.books.update({}, {$set : {arr : [1,2,3,4,5,6,7]}}, {multi : true})
```
#### ![image](https://github.com/user-attachments/assets/a98e789e-8a36-4972-b738-584c7e2ce46d)

