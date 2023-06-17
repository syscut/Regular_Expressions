### list all container
```
docker container ls
```
### check composoe settings
```
docker inspect <container id> | grep com.docker.compose
```
### run command in gitlab container
```
docker exec -it <container id> <your command>
```
## GitLab mvn deploy
- 如果 gitlab group name 為 `com.example` project name 為 `myRepository` 對應 pom.xml
  ```
  <groupId>com.example</groupId>
  <artifactId>myRepository</artifactId>
  ```
- pom.xml 內加入
  ```
  <distributionManagement>
    <repository>
      <id>gitlab-maven</id>
      <url>http(s)://<your_host_name>/api/v4/projects/<project_id>/packages/maven</url>
    </repository>
    <snapshotRepository>
      <id>gitlab-maven</id>
      <url>http(s)://<your_host_name>/api/v4/projects/<project_id>/packages/maven</url>
    </snapshotRepository>
  </distributionManagement>
  ```
- 在其他 project 內使用此 repository 需添加 [endpoint-urls](https://docs.gitlab.com/ee/user/packages/maven_repository/#endpoint-urls)
- 此處才分為 group 或 project 或 instance 前面 deploy 沒有分

### Personal access token
- 需要在個人頁面的 Access Tokens 新增一個 Token 並名為 Private-Token
- 修改 server 端 Maven Home 底下的 settings.xml
  ```
  <settings>
    <servers>
      <server>
        <id>gitlab-maven</id>
        <configuration>
          <httpHeaders>
            <property>
              <name>REPLACE_WITH_NAME</name>
              <value>REPLACE_WITH_TOKEN</value>
            </property>
          </httpHeaders>
        </configuration>
      </server>
    </servers>
  </settings>
  ```
### ci/cd
- server 端 setting.xml 不用改
- 至 project setting -> ci/cd -> Token Access -> Limit CI_JOB_TOKEN access 打開(預設會加入本project 或是可以另外加入別的 project 上限100組)
- 在自己的 Maven Repository 底下新增 `ci_settings.xml`
  ```
  <settings xmlns="http://maven.apache.org/SETTINGS/1.1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
    <servers>
      <server>
        <id>gitlab-maven</id>
        <configuration>
          <httpHeaders>
            <property>
              <name>Job-Token</name>
              <value>${CI_JOB_TOKEN}</value>
            </property>
          </httpHeaders>
        </configuration>
      </server>
    </servers>
  </settings>
  ```
- 會自動吃到 GitLab 自動產生的 CI_JOB_TOKEN 此 token 為單次性,每次都不同
- .gitlab-ci-yml
  ```
  mvn deploy -s ci_settings.xml
  ```
