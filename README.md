# mybatis-plus 读写分离+分库分表

项目基于： https://gitee.com/baomidou/mybatisplus-sharding-jdbc

因为原项目中提到的  sharding-jdbc-mybatis-plus-spring-boot-starter 没有再更新，所以产生了此项目

### dependencies
- com.baomidou:mybatis-plus:2.2.0
- sharding-jdbc-core-spring-boot-starter:2.0.3
- spring-boot-starter:1.5.10.RELEASE

尽量保持以上依赖跟官方最近稳定版同步


### 声明

项目 使用了 mybatis-plus 的 groupId,如果觉得不妥 可以联系我修改


### 使用

```yaml
sharding.jdbc:
  datasource:
    names: ds_master_0,ds_master_0_slave_0
    ds_master_0:
      type: com.zaxxer.hikari.HikariDataSource
      driverClassName: com.mysql.jdbc.Driver
      jdbcUrl: jdbc:mysql://192.168.1.1:3306/demo?useSSL=false&useUnicode=true&characterEncoding=utf8&autoReconnect=true
      username: root
      password: 111111
      maxPoolSize: 20
    ds_master_0_slave_0:
      type: com.zaxxer.hikari.HikariDataSource
      driverClassName: com.mysql.jdbc.Driver
      jdbcUrl: jdbc:mysql://192.168.1.2:3306/demo?useSSL=false&useUnicode=true&characterEncoding=utf8&autoReconnect=true
      username: xxx
      password: 111111
      maxPoolSize: 20
  config:
    masterslave:
      name: ds_ms
      master-data-source-name: ds_master_0
      slave-data-source-names: ds_master_0_slave_0
```

这里数据源根据自己需求定，详细的配置见 [Sharding-Jdbc](http://shardingjdbc.io/docs_cn/02-guide/configuration/)


