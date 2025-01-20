### 一、部署
- cd nacos1/nacos-docker/cluster-mode/
- docker-compose -f cluster-hostname.yaml up 
- docker logs container_id(nacos1/nacos2/nacos3)

#Error creating bean with name 'externalDumpService': Invocation of init method failed; nested exception is ErrCode:500, ErrMsg:Nacos Server did not start because dumpservice bean construction failure :
org.springframework.jdbc.BadSqlGrammarException: PreparedStatementCallback; bad SQL grammar [SELECT DISTINCT data_id, group_id, tenant_id FROM config_info_aggr]; nested exception is java.sql.SQLSyntaxErrorException: Table 'nacos_devtest.config_info_aggr' doesn't exist
缺少表格那就添加表格

docker exec -it mysql bash
mysql> use nacos_devtest
Database changed
mysql> create table nacos_devtest.config_info_aggr(
    -> data_id VARCHAR(255) NOT NULL,
    -> group_id VARCHAR(255) NOT NULL,
    -> tenant_id VARCHAR(255) NOT NULL);
docker logs container_id(nacos1/nacos2/nacos3)
如果看到如下日志，说明服务启动成功。
INFO Nacos started successfully in cluster mode. use external storage
控制台页面：link：http://127.0.0.1:8848/nacos/
二、
1、开启鉴权
在nacos-hostname.env中新增一行NACOS_AUTH_ENABLE=true即可。
docker-compose -f cluster-hostname.yaml up -d
2、修改密码
只需修改env目录中的mysql.env  nacos-hostname.env
MYSQL_USER=nacos
MYSQL_PASSWORD=nacos

NACOS_AUTH_IDENTITY_KEY=2222
NACOS_AUTH_IDENTITY_VALUE=2xxx
NACOS_AUTH_TOKEN=SecretKey012345678901234567890123456789012345678901234567890123456789
自行修改密码
docker-compose -f cluster-hostname.yaml up -d
#进入容器查看配置是否更改成功
docker exec -it container bash
printenv | grep AUTH


git命令
echo "# nacos1" >> README>md
git init 
git add README.md(指定内容) / .（全部内容）
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/melody888888/nacos1.git
git push -u origin main
or
git remote add origin https://github.com/melody888888/nacos1.git
git branch -M main
git push -u origin main
