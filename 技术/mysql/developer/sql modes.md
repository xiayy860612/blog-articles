# SQL Models

`sql_mode`系统变量可用于**全局作用域和会话作用域**, 
可以在mysql启动时在命令行中设置, 或者是在mysql的配置文件my.cnf中设置.

```sql
-- 查询
SELECT @@GLOBAL.sql_mode;
SELECT @@session.sql_mode;

-- 设置
SET GLOBAL sql_mode = 'modes';
SET SESSION sql_mode = 'modes';
```

SQL Models会影响MySQL所支持的SQL语法以及数据的有效性验证.

`innodb_strict_mode`用于针对InnoDB存储的表进行额外的错误检查.

SQL mode的修改会对已存在的分区表造成很大的影响, 有可能会导致数据的丢失和破坏.
强烈建议在创建了用户自定义的分区表后不修改SQL mode; 保证主从节点的SQL mode一致.

所谓的strict mode指的是开启了**STRICT_TRANS_TABLES**或者**STRICT_ALL_TABLES**中的任一一个或者全部.

重要的模式:

- ERROR_FOR_DIVISION_BY_ZERO
- NO_AUTO_CREATE_USER
- NO_ZERO_IN_DATE
- ONLY_FULL_GROUP_BY
- STRICT_TRANS_TABLES

## strict sql mode

严格模式控制MySQL如何处理数据更改语句（例如INSERT或UPDATE）中的无效或缺失值.
如果严格模式无效，则MySQL会为无效或缺失的值**插入调整后的值并产生警告**.

对于SELECT 不更改数据的语句，无效值会在严格模式下生成警告，而不是错误。

对于事务表, 启用STRICT_ALL_TABLES或STRICT_TRANS_TABLES时, 数据更改语句中的无效值或缺失值会发生错误, 该语句被中止并回滚。

对于非事务表:
- 如果在要插入或更新的第一行中出现错误值, 语句中止且表保持不变
- 如果该语句插入或修改了多行，并且错误值出现在第二行或更高行中, 则结果取决于启用了哪种严格模式:
  - 对于STRICT_ALL_TABLES，MySQL返回错误，并忽略其余行。但是由于已插入或更新了较早的行，因此结果是部分更新。为避免这种情况，请使用单行语句。
  - 对于STRICT_TRANS_TABLES，MySQL将无效值转换为该列的最接近的有效值，并插入调整后的值。
  如果缺少值，MySQL将为列数据类型插入隐式默认值。无论哪种情况，MySQL都会生成警告而不是错误，并继续处理该语句。

## IGNORE关键字

- IGNORE关键字: 将错误降级为警告
- 严格模式: 将警告升级为错误

当IGNORE关键字和严格的SQL模式都有效时，IGNORE优先。

可用于以下语句:

- CREATE TABLE ... SELECT
- DELETE
- INSERT
- UPDATE

---
[Server SQL Modes]: https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html