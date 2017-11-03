# tomcat-redis-session-manager

搬迁的
https://github.com/jcoleman/tomcat-redis-session-manager
感谢原作者

这里只是记录使用方式，和编译好的jar包，方便项目急需使用的情况。


实现tomcat的session缓存到redis中


1 将tomcat-redis-session、jedis.jar、commons-pool2.jar 三个jar包分别放在tomcat实例下的lib目录下。

1 配置Tomcat的conf目录下的context.xml文件：
单点Reids配置

<!-- 
    Jedis save session
    -->
    <Valve className="com.radiadesign.catalina.session.RedisSessionHandlerValve" />        
    <Manager className="com.radiadesign.catalina.session.RedisSessionManager" 
        host="localhost" 
        port="6379" 
        database="0" 
		password="redispassword" 
        maxInactiveInterval="60"/>
		
		
Sentinel集群配置：

 <!-- Sentinel 配置 -->
     <Valve className="com.radiadesign.catalina.session.RedisSessionHandlerValve" />        
    <Manager className="com.radiadesign.catalina.session.RedisSessionManager" 
        maxInactiveInterval="60"
        sentinelMaster="mymaster"
		password="redispassword" 
        sentinels="127.0.0.1:26379,127.0.0.1:26380,127.0.0.1:26381,127.0.0.1:26382"
        />
		
		
重启tomcat服务
