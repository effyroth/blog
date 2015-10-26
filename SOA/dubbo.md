本来准备用dubbo和thrift搭建一套跨语言SOA架构的基础框架,结果中间遇到的问题不少,做个记录总结

    os              : mac os
    ide             : Intellij idea
    build tool      : gradle
    java version    : 1.8
    thrift version  : 0.9.1 and 0.8.0
    webserver       : gradle jetty plugin
    log             : slf4j->log4j
    
    总的来说最大的麻烦其根本来自java的依赖冲突(部分exclude解决)
    gradle 不引入idea插件会造成ide依赖混乱
    idea 的 gradle runner plugin 有logback和log4j冲突报错,
    shell里执行gradle jettyrunwar则没问题,
    所以猜测是gradle runner plugin本身依赖了有logback的classpath
    java8会由于版本过高导致log报错,还会出现optional反射调用失败问题,建议改用java7
    
    dubbo自身扩展了thrift0.8.0的protocol,
    所以thrift0.9.1没法用(但brew只能装0.9.1,
    这里找thrift0.8.0的执行文件又遇到麻烦,
    mac ox下编译0.8比较麻烦,
    最后找了一个win的执行文件在win上完成gen)
    
    搞定thrift0.8以后测试provider和consumer,
    这里遇到了一个"commons-lang:commons-lang:2.6"的依赖问题,
    因为是反射loader,
    运行时才报classnotfound,真是防不胜防
    简单参数和简单返回值的method invoke success,
    但method返回值(参数没试)里有序列化对象的时候consumer显示provider timeout,
    provider不容易debug,猜测可能是对象序列化出了问题

    很失望,都到这一步了,改用dubbo原生协议做了一套demo,好歹是跑通了
    
    TODO:dubbo monitor搭建
