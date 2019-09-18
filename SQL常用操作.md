# 修改表的schema，修改列字段类型
```SQL
ALTER SCHEMA dbo TRANSFER [fun].[value_set_master]
GO  
ALTER SCHEMA dbo TRANSFER [fun].[column_display_name]
GO  

alter table demographics alter column [create_timestamp] datetime
alter table demographics alter column [update_timestamp] datetime
```

# 删除数据库下面的所有表

```SQL
declare @sql varchar(8000)
declare @name varchar(64)
while (select count(*) from sysobjects where type='U' and category=0)>0
begin
select top 1 @name=name from sysobjects where type='U' and category=0
SELECT @sql='drop table [dbo].[' + @name + ']'
exec(@sql)
print @sql
end
```
