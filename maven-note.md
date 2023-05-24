### The order of Maven basic phases is:
- Validate
- Compile
- Test
- Package
- Verify
- Install
- Deploy

### Generate JUnit Test Report
- add in &lt;build&gt;
- Run `mvn surefire-report:report`
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-report-plugin</artifactId>
    <version>3.0.0</version>
    <configuration>
        <outputDirectory>${basedir}/</outputDirectory>
        <linkXRef>false</linkXRef>
    </configuration>
</plugin>
```
- 直接跑 `mvn site` 會有 error: `java.lang.NoClassDefFoundError: org/apache/maven/doxia/siterenderer/DocumentContent`
- 需添加以下 Repository
- 執行後會跑出整個 Project 的 Repository
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-project-info-reports-plugin</artifactId>
    <version>3.4.1</version>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-site-plugin</artifactId>
    <version>3.12.0</version>
</plugin>
```
