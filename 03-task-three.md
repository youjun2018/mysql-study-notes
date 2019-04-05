# 【任务四】

## 4.1 MySQL 实战
### 学习内容

数据导入导出

将之前创建的任意一张MySQL表导出,且是CSV格式,再将CSV表导入数据库

### 作业

#### 项目七: 各部门工资最高的员工（难度：中等）

创建 Employee 表，包含所有员工信息，每个员工有其对应的 Id, salary 和 department Id。

```sql
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
```

创建 Department 表，包含公司所有部门的信息。

```sql
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```

编写一个 SQL 查询，找出每个部门工资最高的员工。例如，根据上述给定的表格，Max 在 IT 部门有最高工资，Henry 在 Sales 部门有最高工资。

```sql
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+
```


#### 项目八: 换座位（难度：中等）

小美是一所中学的信息科技老师，她有一张 seat 座位表，平时用来储存学生名字和与他们相对应的座位 id。其中纵列的 id 是连续递增的，小美想改变相邻俩学生的座位。
你能不能帮她写一个 SQL query 来输出小美想要的结果呢？
 
 请创建如下所示 seat 表：
 
示例：

```sql
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Abbot   |
|    2    | Doris   |
|    3    | Emerson |
|    4    | Green   |
|    5    | Jeames  |
+---------+---------+
```

假如数据输入的是上表，则输出结果如下：

```sql
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Doris   |
|    2    | Abbot   |
|    3    | Green   |
|    4    | Emerson |
|    5    | Jeames  |
+---------+---------+
```

注意：

如果学生人数是奇数，则不需要改变最后一个同学的座位。

#### 项目九: 分数排名（难度：中等）

编写一个 SQL 查询来实现分数排名。如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。

创建以下 score 表：

```sql
+----+-------+
| Id | Score |
+----+-------+
| 1 | 3.50 |
| 2 | 3.65 |
| 3 | 4.00 |
| 4 | 3.85 |
| 5 | 4.00 |
| 6 | 3.65 |
+----+-------+
```

例如，根据上述给定的 scores 表，你的查询应该返回（按分数从高到低排列）：

```sql
+-------+------+
| Score | Rank |
+-------+------+
| 4.00 | 1 |
| 4.00 | 1 |
| 3.85 | 2 |
| 3.65 | 3 |
| 3.65 | 3 |
| 3.50 | 4 |
+-------+------+
```



## 4.2 MySQL 实战 - 复杂项目
### 作业

#### 项目十：行程和用户（难度：困难）

Trips 表中存所有出租车的行程信息。每段行程有唯一键 Id，Client_Id 和 Driver_Id 是 Users 表中 Users_Id 的外键。Status 是枚举类型，枚举成员为 (‘completed’, ‘cancelled_by_driver’, ‘cancelled_by_client’)。

```sql
+----+-----------+-----------+---------+--------------------+----------+
| Id | Client_Id | Driver_Id | City_Id |        Status      |Request_at|
+----+-----------+-----------+---------+--------------------+----------+
| 1  |     1     |    10     |    1    |     completed      |2013-10-01|
| 2  |     2     |    11     |    1    | cancelled_by_driver|2013-10-01|
| 3  |     3     |    12     |    6    |     completed      |2013-10-01|
| 4  |     4     |    13     |    6    | cancelled_by_client|2013-10-01|
| 5  |     1     |    10     |    1    |     completed      |2013-10-02|
| 6  |     2     |    11     |    6    |     completed      |2013-10-02|
| 7  |     3     |    12     |    6    |     completed      |2013-10-02|
| 8  |     2     |    12     |    12   |     completed      |2013-10-03|
| 9  |     3     |    10     |    12   |     completed      |2013-10-03| 
| 10 |     4     |    13     |    12   | cancelled_by_driver|2013-10-03|
+----+-----------+-----------+---------+--------------------+----------+
```

Users 表存所有用户。每个用户有唯一键 Users_Id。Banned 表示这个用户是否被禁止，Role 则是一个表示（‘client’, ‘driver’, ‘partner’）的枚举类型。

```sql
+----------+--------+--------+
| Users_Id | Banned |  Role  |
+----------+--------+--------+
|    1     |   No   | client |
|    2     |   Yes  | client |
|    3     |   No   | client |
|    4     |   No   | client |
|    10    |   No   | driver |
|    11    |   No   | driver |
|    12    |   No   | driver |
|    13    |   No   | driver |
+----------+--------+--------+
```

写一段 SQL 语句查出 2013年10月1日 至 2013年10月3日 期间非禁止用户的取消率。基于上表，你的 SQL 语句应返回如下结果，取消率（Cancellation Rate）保留两位小数。

```sql
+------------+-------------------+
|     Day    | Cancellation Rate |
+------------+-------------------+
| 2013-10-01 |       0.33        |
| 2013-10-02 |       0.00        |
| 2013-10-03 |       0.50        |
+------------+-------------------+
```

#### 项目十一：各部门前3高工资的员工（难度：中等）

将项目7中的 employee 表清空，重新插入以下数据（其实是多插入5,6两行）：

```sql
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
+----+-------+--------+--------------+
```

编写一个 SQL 查询，找出每个部门工资前三高的员工。例如，根据上述给定的表格，查询结果应返回：

```sql
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
| IT         | Joe      | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |
+------------+----------+--------+
```

此外，请考虑实现各部门前N高工资的员工功能。

#### 项目十二  分数排名 - （难度：中等）

依然是昨天的分数表，实现排名功能，但是排名是非连续的，如下：

```sql
+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 3    |
| 3.65  | 4    |
| 3.65  | 4    |
| 3.50  | 6    |
+-------+------+
```

### 【任务说明】
这是本次集训最后一次任务啦，大家再坚持一下。之前的任务中项目是不是觉得水水的？本次任务都是较为复杂的实战了。建议有能力的小伙伴可以在项目本身的基础上拓展，看能不能将问题设置的更复杂点或实现方式更灵活点。举个栗子：各部门工资最高，是不是可以实现工资第二高的甚至是第N高的？ 自由发挥~
祝大家学习开心。:-)

======================================================================================

以下是实战

### 项目七
1. 创建 Employee 表

```sql
create table Employee(

Id int auto_increment primary key,

Name varchar not null,

Salary int not null,

DepartmentId int not null

);

insert into Emploee (Name,Salary,DepartmentId) values(Joe,70000,1);

insert into Emploee(Name,Salary,DepartmentId) values(Henry,80000,2);

insert into Emploee(Name,Salary,DepartmentId) values(Sam,60000,2);

insert into Emploee(Name,Salary,DepartmentId) values(Max,90000,1);
```

2. 创建 Department 表

```sql
create table Department(

Id int primary key auto_increment,

Name varchar not null

);

insert into Department(Name) values (IT);

insert into Department(Name) values (Sales);
```

3. 找出每个部门工资最高的员工
```sql
select Department.Name as Department,Emploe.Name as Emploee,max(Emploee.Salary) as Salary from Emploee,Department where Employee.Id=Department.Id group by Emploee.DepartmentId;
```

### 项目八：换座位

1. 创建 seat 表

```sql
create table seat(

id int primary key auto_increment,

student varchar not null

);

insert into seat(student) values(Abbot);

insert into seat(student) values(Doris);

insert into seat(student) values(Emerson);

insert into seat(student) values(Green);

insert into seat(student) values(Jeames);
```

2. 输出结果

```sql
UPDATE seat s1
JOIN seat s2
ON (s1.id % 2 = 1 AND s2.id = s1.id+1)
SET s1.student=s2.student,s2.student=s1.student

WHERE s1.id+1 <> null;
```

### 项目九：分数排名

1. 创建 score 表

```sql
create table score(

Id int auto_increment primary key,

Score float not null

);
```

2. 查询结果

```sql
SELECT Score,
CASE 
WHEN @prevRank = Score THEN @curRank 
WHEN @prevRank := Score THEN @curRank := @curRank + 1
END AS Rank
FROM scores,
(SELECT @curRank :=0, @prevRank := NULL) 
ORDER BY Score desc;
```

### 项目十：行程和用户

```sql
select t1.Request_at,t1.c1/t2.c2 as Cancellation Rate from

(select count(Status) as c1 Request_at from Trips where Client_Id in (select Users_id from Users where Role=client && Banned=No;) and Status <> completed group by Request_at;) t1,

(select count(Status) as c2 Request_at from Trips where Client_Id in (select Users_id from Users where Role=client && Banned=No;) group by Request_at;) t2

where

t1.Request_at=t2.Request_at;
```

### 项目十一：各部分前 3 高的工资的员工

```sql
select Department.Name as Department,EmployeeName as Employee,Employee.Salary from

Department join Employee on 

order by Employee.salary

desc

limit 3

group by

Department.name

where

Employee.Department_Id=Department.Id;
```


### 项目十二：分数排名

```sql
SELECT Score Rank FROM
(SELECT Score,
@curRank := IF(@prevRank = Score, @curRank, @incRank) AS Rank,
@incRank := @incRank + 1, 
@prevRank := Score
FROM scores,(
SELECT @curRank :=0, @prevRank := NULL, @incRank := 1
) 
ORDER BY Score desc;
```















