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

---

### 3.测试一个水杯

寻找水杯是否有说明书，如果有需要充分阅读并理解水杯说明书，按说明书描述，测试到所有需求点  
按测试关注点划分主要分为以下几个方面：

1.功能测试：  
主要关注水杯基本功能  
1.1 水杯是否可以正常装水  
1.2 水杯是否可以正常喝水  
1.3 水杯是否有盖子，盖子是否可以正常盖住  
1.4 水杯是否有保温功能，保温功能是否正常保温  
1.5 水杯是否会漏水，盖住盖子拧紧后是否会漏水  

2.界面测试：  
主要关注水杯外观、颜色、设计等方面  
2.1 外观是否完整  
2.2 外观是否舒适  
2.3 颜色搭配及使用是否让人感到舒适  
2.2 杯子外观大小是否适中  
2.3 杯子是否有图案，图案是否易磨损

3.易用性测试：  
主要关注水杯使用是否方便  
3.1 水杯喝水时否方便  
3.2 水杯拿起放下是否方便，这里会衍生到水杯形状的测试  
3.3 水杯装水是否方便  
3.4 水杯携带是否方方便  
3.5 水杯是否有防滑功能  
3.6 水杯装有低温或者高温水时，是否会让手感到不适

4.性能测试：  
4.1 水杯装满水时，是否会露出来  
4.2 水杯最大使用次数  
4.3 水杯的保温性是否达到要求  
4.4 水杯的耐寒性是否达到要求  
4.5 水杯的耐热性是否达到要求  
4.6 水杯掉落时时，是否可以正常使用  
4.7 水杯长时间放置时，是否会发生泄露

5.兼容性测试： 
主要关注水杯是否可以装其他液体，如果汁、汽油、酒精等

6.可移植性测试： 
主要关注水杯放置环境等  
6.1 将水杯放在常温环境中，使用是否正常  
6.2 将水杯放在零下的环境中，使用是否正常  
6.3 将水杯放在高于正常温度的环境中，使用是否正常

7.安全性测试：  
主要关注水杯外观和各种异常条件下是否释放有毒物质等  
7.1 当水杯装满热水时，水杯是否会烫手  
7.2 当水杯装上水后，是否会产生有毒物质  
7.3 把水杯放在零下环境时，是否会产生有毒物质  
7.4 把水杯放在高温环境时，是否会产生有毒物质
