# IBatisNet
IBatisNet  fork from https://github.com/yYang365/IBatisNet

##### 测试及编译流程: 

**项目 "IBatisNet.DataMapper.Test"** 

> 新建文件database.config, 具体模板参考文件 DataBase-Template.config

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<settings>
	<!--   User application and configured property settings go here.-->
	<!-- To run tests, create a file named DataBase.config 
		 with your own value for datasource.
		 (don't included it in the solution and don't commit it in SVN)
	-->
	<add key="userid" value="IBatisNet" />
	<add key="password" value="test" />
	<add key="database" value="IBatisNet" />
	<add key="datasource" value="(local)\NetSDK" />
	<add key="useridHibernate" value="NHibernate" />
	<add key="databaseHibernate" value="NHibernate" />
    <!--下面这行暂时不知有什么用-->
	<add key="connectionStringOdbc" value="Driver={SQL Server};Server=(local)\NetSDK;Database=IBatisNet;Uid=IBatisNet;Pwd=test;" />
	<add key="datasourceMySql" value="localhost" />
	<add key="selectKey" value="select @@IDENTITY as value" />
	<add key="MyCategoryName" value="'Film'" />
	<add key="accountName" value="'Joe'" />
	<add key="datasourcePostgreSQL" value="localhost"/>
	<add key="directory" value="Maps" />
	<add key="useStatementNamespaces" value="true" />
</settings>
```



IbatisNet启用事务的方案有两个:

1. 使用SqlMapper默认的 BeginTransaction 方法

   ```csharp
   sqlMap.BeginTransaction(); //SqlMap需要设置为静态成员变量
   //TODO: 其他业务逻辑
   sqlMap.CommitTransaction();
       
   ```

2. 同样使用SqlMapper.BeginTransaction() 方法, 但用法稍微不同

   ```csharp
    using (IDalSession session = sqlMap.BeginTransaction())
    {
        //TODO: 其他业务逻辑
       session.Complete(); // Commit
    }
   ```

   