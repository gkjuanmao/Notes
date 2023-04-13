# 1. 报java runtime错

一般为Java版本不对，需要改java版本，如果改了Java版本还是报错，在构建中点击错误，会弹出项目结构，在里面修改Java版本

# 2. 报ClassNotFound

springboot各个组件不一定是同一版本，如果版本不对就会出现报错，将版本不对的组件在pom中加上dependency依赖

# 3. springboot启动后没有报错直接退出

多半是没加spring-boot-web组件