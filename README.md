# dynamicDrools
动态配置drools规则引擎和定时器,本文只提供了一个解决思路，后续会从项目中把代码摘取出来
##动态规则
  思路如下：
      MQ数据-》从数据库中获取rule->执行规则->满足条件->执行操作
##定时器
  思路如下：
      由于drools自带的定时器太过于鸡肋，无法控制定时器的开启，关闭，在执行过程中无法修改when 条件数据。
      
      所以我们可以考虑引入任务调用框架quartz,注：在微服务中，可能需要注意，quartz的重复执行问题。而分布式任务调度平台
      
      xxl-job也可以实现此功能，但是当我们想动态获取规则和规则对应cron表达式时，貌似xxl-job满足提供的bean模式，class/method满足不了我们的需求，
      
      所以本人使用quartz解决了这个问题。
      
      新建规则->开启规则状态->存储规则到quartz中->启动quartz对应的任务
      
      quartz 规则引擎定时器任务执行过程
      
      quzrtz启动任务 ->执行任务->获取任务信息（数据库中存储了对应的规则id）->获取规则->执行规则
      
      其实这个地方，就是把规则引擎的定时器功能转移到了quartz来管理->然后去执行drools.
      
      980938480@qq.com
      需要帮助可以致邮
      
      
      
      
      
      
      
      
  
