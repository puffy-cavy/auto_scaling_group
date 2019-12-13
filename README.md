# auto_scaling_group
我从12.6号写到12.13号，，终于把这个东西写完了
太多坑了😫

#### 1. 
aws cloudformation describe-stacks 可以查这个账户上所有的cf stack，这样就算query了半个string也可以查出来
aws cloudformation list-stack-resources 为了列出一个特定stack的所有resources
这些output都可以是text，table。。的形式，也可以用query 来filter， table最适合用来看从属关系
（本来除了describe-auto-scaling-groups，还看到一个describe-auto-scaling-groups by instanceID的，但后来怎么都找不到ASG的id在哪儿了）

#### 2.
写cloudformation template的时候，最外面是
```
{
"Resources":{}
}
```
auto scaling group一定要有一个launch config跟着。（虽然写的时候细节很多，但写完发现还是很make sense的）

#### 3.
为了查output结果有没有 contain某个关键词，aws cli有些command好像可以用contain，但cloudformation describe-stacks只能用grep

#### 4.
bash script 的 if statement 后要加；evaluate的语句外面是double bracket [[]]

#### 5.
bash script首行不加 #!/usr/bin/env bash 就会认不出所有的bash command，这个应该是定义一个bash script跑的环境

#### 6.
不加 export PATH=/usr/local/bin:$PATH 就会认不出aws的所有command， 可能是告诉Jenkins需要用的plug in在哪里找吧

#### 7.
关于怎么从Jenkinsfile/groovy 读input进bash script：虽然adolfo说在Jenkinsfile里 sh“source jenkins_bash.sh”不需要source，但没有source 的话，好像连echo这种bash command都执行不出来。所以还是需要source的。虽然刚开始不敢在variable前面加env， 会让这个variable跨很多环境（变成multi environment consistent，这样好像容易ruin 一个variable），但只有env.VARIABLE = "${}"，bash script才能读到，bitbucket上的代码也是这么写的。还有！！！因为赋给variable的值都是string，所以一定要在${}外面加双引号！不然会有Jenkins 的error
