# MySQL學習筆記
## what is that?
database作用是存儲和管理數據的倉庫
## fundamental concep of MYSQL
### DB,DBMS, SQL
DB for store data, DBMS from control and manage, SOL是操作的方法, different DBMS use the same language(SQL) 
### how to use
在windows下使用管理員cmd進入mqsql的指令為
```mqsql
net start mysql以啟動
net stop mqsql 以關閉
```
連接客戶端
```mqsql
mqsql -u root -p
```
### 3.RDBMS
類似excel的表, 有一個統一格式(唯一標識)如id
### data model
user->DBMS(orcal,mysql and so on)->DB->RDBMS(二維表單)

## SQL
### SQL語法
SQL不分大小寫, 並以;結尾

單行注釋 --
多行注釋 /**/
### SQL分類 
DDL:數據定義, 如表,

查詢DB: SHOW DATABASES;

查詢當前DB: SELECT DATABASE();

創建DB: CREATE DATABASE [name] [charset] [collate排序規則];

刪除DB: DROP DATABASE [name];

使用DB: USE [name];

查詢表 show tables;

查詢表結構 desc [表名];

查詢指定表的建表語句: show create table [name];

創建表:
```mysql
create table [name](
    字段1 type[comment"名稱"],
    字段2 type[comment"名稱"],
    字段3 type[commen"名稱"],
)[comment "名稱"];
```

數據類型: 數值類型, float int,tinyint(無符號整數)等

字符串類型: carchar(變長字串),text(長文本)

日期類型: date, time, year, datetime,

修改表數據(add): alter table [table name] add [字段名] [type(長度)] [comment "注釋"][約束];

modify(修改數據類型): alter table [table name] modify [字段名] [新數據長度][comment];

change(修改數據類型和字段名):alter table [table name] change [舊字段名] [新字段名] [類型(長度)] [comment];

drop(修改數據類型和字段名):alter table [table name] drop [字段名] [comment];

rename to(重命名): alter table [old table name] rename to  [new table name] [comment];

DML: 對數據刪改,

DQL: 查詢DB記錄,

DCL:控制用戶權限

## function
## constraint
## 多表查詢
## 事務
```mqsql

```