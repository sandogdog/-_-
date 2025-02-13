# 新大陆软件_软件初级测试工程师_笔试+面试
唉，准备了两天面试的，但是自己一直在熟悉测试流程和测试工程师的工作，导致面试前的笔试直接寄……题目倒是不难，都怪自己捏。不过拿得起，放得下，想快点找工作，要总结经验。

---

### 1.(mysql)现有以下三张表结构：

学生表 (Student)  
StudentID (学生ID，主键)  
StudentName (学生姓名)

课程表 (Course)  
CourseID (课程ID，主键)  
CourseName (课程名称)

选课表 (Enrollment)  
EnrollmentID (选课记录ID，主键)  
StudentID (学生ID，外键关联学生表)  
CourseID (课程ID，外键关联课程表)

要求：  
编写一条 SQL 查询，返回所有选修了课程名为“语文”的学生信息（需包含去重逻辑）。

注意：  
若学生多次选修同一门课程，结果中不应重复。  
需显式说明表关联逻辑。

```SQL
-- 使用 INNER JOIN 实现多表关联
SELECT DISTINCT s.StudentID, s.StudentName
FROM Student s
INNER JOIN Enrollment e ON s.StudentID = e.StudentID
INNER JOIN Course c ON e.CourseID = c.CourseID
WHERE c.CourseName = '语文';

-- 或使用子查询实现
SELECT StudentID, StudentName
FROM Student
WHERE StudentID IN (
    SELECT DISTINCT e.StudentID
    FROM Enrollment e
    INNER JOIN Course c ON e.CourseID = c.CourseID
    WHERE c.CourseName = '语文'
);
```

---

### 2.(mysql)假设有一个购物表 `shopping`，表中包含以下字段：  
- `shopper_name`：购物人姓名    
- `product_name`：购买商品名称  
- `quantity`：商品数量  

以下是表格数据示例：  

| shopper_name | product_name | quantity |  
|--------------|--------------|----------|  
| Alice        | Apple        | 5        |  
| Alice        | Banana       | 3        |  
| Bob          | Apple        | 2        |  
| Bob          | Orange       | 4        |  
| Bob          | Banana       | 1        |  
| Charlie      | Apple        | 7        |  

现在，你需要查询购买商品种类在两种或两种以上的购物人信息，即查询那些至少购买了两种不同商品的购物人。

SQL 查询语句：

```sql
SELECT shopper_name
FROM shopping
GROUP BY shopper_name
HAVING COUNT(DISTINCT product_name) >= 2;
```

解释：  
1. **GROUP BY shopper_name**：按购物人姓名分组，将同一个人购买的所有商品记录聚集在一起。  
2. **COUNT(DISTINCT product_name)**：计算每个购物人购买的不同商品种类数。  
3. **HAVING COUNT(DISTINCT product_name) >= 2**：只筛选出购买了至少两种不同商品的购物人。

查询结果：

| shopper_name |  
|--------------|  
| Alice        |  
| Bob          |  

在这个例子中，Alice 购买了 Apple 和 Banana 两种商品，Bob 购买了 Apple、Orange 和 Banana 三种商品，因此他们符合条件。
