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

對DB操作{

    查詢DB: SHOW DATABASES;

    查詢當前DB: SELECT DATABASE();

    創建DB: CREATE DATABASE [name] [charset] [collate排序規則];

    刪除DB: DROP DATABASE [name];

    使用DB: USE [name];
}

對table操作{

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

修改表數據(add): alter table [table name] add [字段名] [type(長度)] [comment "注釋"][約束];

modify(修改數據類型): alter table [table name] modify [字段名] [新數據長度][comment];

change(修改數據類型和字段名):alter table [table name] change [舊字段名] [新字段名] [類型(長度)] [comment];

drop(修改數據類型和字段名):alter table [table name] drop [字段名] [comment];

rename to(重命名): alter table [old table name] rename to  [new table name] [comment];

}

DB數據類型: 
- 數值類型, float int,tinyint(無符號整數)等

- 字符串類型: carchar(變長字串),text(長文本)

- 日期類型: date, time, year, datetime,



DML: DDL是對表或DB修改, DML是對表中數據頁做增刪改, 其數據操作語言, 有以下三種方法
1. 插入, insert:
    - 給指定字段加數據 insert into 表名(字段1,字段2...) value(值1,2,...) ;
    - 給全部字段加數據 insert into [表名] [值];
2. 修改, update
    - update [table name] set [字段1=值1,字段2=值2,字段3=值3...] [where條件];
3. 刪除, delete
   - delete from [table] {where}

DQL: 查詢DB記錄, 用來查詢數據庫中的表, 有以下7種查詢方法, 執行順序為
1. select, 查詢字段列表
   - 去重查詢 select distinct 字段列表 from 表名; 
2. from, 查詢表名列表   
3. where, 查詢條件列表 
4. group by, 查詢分組字段列表
5. having, 查詢分組後條件列表
6. order by, 查詢排序字段列表
7. limit, 分頁參數(把N個數據分成K個數據頁展示, 其中K<N)

example.
1. 查詢所有年齡在20~23歳的女性員工信息
   selece * from emp where gender='女' and age in(20,21,22,23);
2. 查詢性別為男, 且年齡在20~40歲(含)內的姓名為三字的員工
   select * from emp where gender='男' and age between 20 and 40 and name like '___';
3. 統計員工表中, 年齡小於60歲的男性員工和女性員工人數
   select gender,count(*) from emp where age < 60 group by gender;
4. 查詢所有年齡小於35歲員工的姓名和年齡, 井對查詢結果按年齡升序排序, 如果年齡相同則按入職時間降序排序。
   select name, age from emp where age<35 order by age asc, entrydate desc;
5. 查詢性別為男, 且年齡在20-40歲(含)內的5位員工信息, 對結果按年齡升序排序, 年齡相同對入職時間排序
   select * from emp where gender = '男' and age between 20 and 40 order by age asc, entryage asc limit 5;


DCL:控制用戶權限, 增刪查改用戶
1. 查用戶
    ```mqsql
    use mtsql;
    select * from user;
    ```
2. 加用戶
   ```mqsql
    create user [username]@[hostname] inentified by [password];
    ```
3. 改用戶
    ```mqsql
    alter user [username]@[hostname] inentified with [原password] BY [新password];
    ```
4. 刪用戶
   ```mqsql
    drop user [username]@[hostname];
    ```
還有一些權限的特定字眼 grant, revoke等

## function
介紹常見內建函數
### 字符串函數
1. concat(s1,s2) 拼接
2. lower(str) 全部轉小寫
3. upper(str) 全部轉大寫
4. lpad(str,n,pad) 用字串pad對str左邊填充, 直到n位
5. rpad(str,n,pad) 用字串pad對str右邊填充, 直到n位
6. trim(str) 去除字串首部和尾部的空格
7. substring(str,start,len) 返回從字串str從start數起len位長度的字串
### 數值函數
1. ceil(X) 向上取整
2. floor(X) 向下取整
3. mod(X) 取模
4. rand() 0,1隨機數
5. round(X,y) 對X四舍五入, 保留y位小數

example: 通過DB function, 生成一個六位數驗證碼
```mqsql
select lpad(round(1000000*rand(),0),6,'0');
```

### 日期函數
1. curdate() 當前日期
2. curtime() 當前時間
3. now() 當前年月日時間
4. date_add(date,interval exp type) 返回一個日期/時間值加上一個時間間隔exp後的數間值
5. datediff(date1,date2) 兩天間相差的天數
   
example 查詢所有員工的入職天數, 並根據入職天數倒序排序
select name, datediff(curdate(),entryday) as 'entrydays' from emp order by entrydays desc; 
### 流程函數
1. if(value, t, f) 若value為真返回t,否則返回f
2. ifnull(value1,value2) 傳兩者間不為空的一個
3. case [語句] when '值A' then '返回值'; (必然等於)
4. case when [語句]>或<'值A' then '返回值';

## constraint
## 多表查詢
## 事務
```mqsql

```