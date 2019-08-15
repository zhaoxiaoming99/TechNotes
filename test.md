# datamodel API设计

## 集成要求
数据库迁移到SQL Server

## 部署方式
1、将 datamanger.war 放到 Tomcat webapps 目录下；
2、启动 tomcat 后，tomcat 自动解压 datamanager.war 包；
3、war包解压完成后，关掉tomcat；
4、修改 jdbc.properties  文件。在 datamanager/WEB-INF/classes/spring/dal/ 目录中，DatabaseName设置成registry
```
jdbc.connection.driver_class = com.microsoft.sqlserver.jdbc.SQLServerDriver
jdbc.connection.url = jdbc:sqlserver://ip地址:1433;DatabaseName=registry
jdbc.connection.username = root
jdbc.connection.password =  root

### sql server Properties2
information.jdbc.connection.url = jdbc:sqlserver://ip地址:1433;DatabaseName=registry
information.jdbc.connection.username =  root
information.jdbc.connection.password =  root
```
5、重启 tomcat


## 调用接口

采用 RESTful web service 调用如下接口，http method 采用 POST 方式。
```
http://<url:8088>/datamanager/service/registry/form-save

```

## JSON 中的关键字段
**registryName:** ddeditor 中新建registry时填写的name值。字符串类型，必填

**registryLevel:** registry | patient 两个选项值，如果修改病人```demographics```信息填写patient（非病人信息不做修改）；如果修改registry信息请填写registry（病人级别信息不做修改）

**action：** 101 表示新增registry表单数据；102 表示修改registry表单数据；103 表示删除registry物理信息。字符串类型，必填

**indexids：** 是这些（NCDRPatientID，HospPatientID，InPatientID，OutPatientID，EncounterID，InPatientSeqID，EmergencySeqID，OutPatientSeqID，ProcedureSeqID ）的组合，要来识别唯一记录。这些 XxxID 并不是所有都需要的，要根据section所对应的物理表用到了哪些。通过 table_level 视图表可以知道对应物理表的 XxxIDs。比如 **select * from table_level where table_name = 'p_pci';**  字符串类型，必填

## 双中心新建encounter参考 [创建双中心直报](/Team2-Area/datamodel-API设计/创建双中心直报)

## 101新增registry Sample
JSON 中的 action 设置为 101 字符串，表示新增模式，前端需要提供所有section字段信息（section不再区分级别，拉平成一个平铺数组）：


```JSON
{
   "registryName":"CathPCI",
   "registryLevel":"registry",
   "action":"101",
   "sections":[
       sectionA,
       sectionB,
       section....,
       {
         "code":"PROCINFO",
         "indexIds":{
            "NCDRPatientID":"0000000001",
            "HospPatientID":"0000000001",
            "ProcedureSeqID":"0000000001",
            "EncounterID":"0000000001",
            "InPatientSeqID":"0000000001",
            "registryID":"0000000001"
         },
         "fields":[
            {
               "name":"DiagCorAngio",
               "value":false
            },
            {
               "name":"AccessSite",
               "value":"0000000002222-动脉入路"
            },
            {
               "name":"CAInHosp",
               "value":false
            },
            {
               "name":"FluoroscopyTime",
               "value":"2019-05-01 08:31:45"
            },
            {
               "name":"ContrastVol",
               "value":345345
            },
            {
               "name":"FluoroDoseDAP",
               "value":45345345
            }
         ]
      }
   ]
}
```

## 102编辑registry sample
JSON 中的 action 设置为 102 字符串，表示编辑，前端需要提供当前界面所有section字段的信息（不需要提供老信息）：
```JSON
{
   "registryName":"CathPCI",
   "registryLevel":"registry",
   "action":"102",
   "sections":[
      {
         "code":"PROCINFO",
         "indexIds":{
            "NCDRPatientID":"0000000001",
            "HospPatientID":"0000000001",
            "ProcedureSeqID":"0000000001",
            "EncounterID":"0000000001",
            "InPatientSeqID":"0000000001",
            "registryID":"0000000001"
         },
         "fields":[
            {
               "name":"DiagCorAngio",
               "value":true
            },
            {
               "name":"AccessSite",
               "value":"0000000002222-动脉入路"
            },
            {
               "name":"CAInHosp",
               "value":true
            },
            {
               "name":"FluoroscopyTime",
               "value":"2019-05-01 08:31:45"
            },
            {
               "name":"ContrastVol",
               "value":345345
            },
            {
               "name":"FluoroDoseDAP",
               "value":45345345
            }
         ]
      }
   ]
}
```







## 删除registry Sample
JSON 中的 action 设置为 103 字符串，表示删除，前端需要提供所有待删除的section节点主索引信息：
```JSON
{
   "registryName":"CathPCI",
   "registryLevel":"registry",
   "action":"103",
   "sections":[
      {
         "code":"PROCINFO",
         "indexIds":{
            "NCDRPatientID":"0000000001",
            "HospPatientID":"0000000001",
            "ProcedureSeqID":"0000000001",
            "EncounterID":"0000000001",
            "InPatientSeqID":"0000000001"
         }
      }
   ]
}

```

###流程图
![Datamanager API 流程图.png](.attachments/Datamanager-API-流程图-f3a34941-ad16-402e-930b-0dc509e32bd7.png)



