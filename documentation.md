---
title: Documentation
excerpt: "Category index"
aside: false
---

<ol>
	<li><a href="#introduction">Introduction.</a></li>
	<li><a href="#requirements">Requirements.</a></li>
	<li><a href="#installation">Installation.</a></li>
	<li><a href="#configuration">Configuration.</a>
<ul>
	<li><a href="#configuration-file">Configuration File.</a></li>
	<li><a href="#configuration-servlet-context">Servlet Context Configurations.</a></li>
	<li><a href="#configuration-spring">Spring Configurations.</a></li>
</ul>
</li>
	<li><a href="#sending_events">Sending Audit Events.</a>
<ol>
	<li><a href="#sending_events_call">Calling Audit Manager.</a></li>
	<li><a href="#annotations">Using Annotations.</a>
<ol>
	<li><a href="#annotations">@Audit</a></li>
	<li><a href="#annotations">@AuditField</a></li>
	<li><a href="#annotations">@DeIdentify</a></li>
	<li><a href="#annotations">@IgnoreAudit</a></li>
</ol>
</li>
</ol>
</li> 
	<li><a href="#metadata">Implementing Meta Data class.</a></li>
	<li><a href="#layouts">Using Layouts.</a>
<ol>
	<li><a href="#layout-simple">Simple Layout.</a></li>
	<li><a href="#layout-secure">Secure Layout.</a></li>
        <li><a href="#layout-customizable">Customizable Layout.</a></li>
</ol>
</li>
	<li><a href="#deidentification">Data de-identification.</a></li>
	<li><a href="#plugins">Plugins.</a>
<ol>
	<li><a href="#database_handler">Database Handler.</a>
<ol>
	<li><a href="#configure_database_handler">Configure Database Handler.</a></li>
	<li><a href="#configure_external_databases">Configure External Databases.</a></li>
	<li><a href="#configure_jndi">Configure jndi Data Sources.</a></li>
        <li><a href="#configure_datasource">External Data Sources.</a></li>
        <li><a href="#configure_pool">Configure Connection Pool.</a></li>
        <li><a href="#configure_multipletables">Multiple tables.</a></li>
</ol>
</li>
	<li><a href="#file_handler">File Handler.</a>
<ol>
	<li><a href="#file_auto_archive">Auto Archive.</a></li>
</ol>
</li>
	<li><a href="#spring_integration">Spring Integration.</a>
<ol>
	<li><a href="#spring_integration_configurations">Configurations.</a></li>
	<li><a href="#spring_audit4j_configurations">Audit4j Configuration with spring.</a></li>
</ol>
</li>
	<li><a href="#weld_integration">Audit4j for CDI spec implementations (Jboss Weld).</a>
<ol>
	<li><a href="#weld_integration_configurations">Configurations.</a></li>
</ol>
</li>
	<li><a href="#http_integration">HTTP Integration.</a>
<ol>
	<li><a href="#http_integration_configurations">Configurations.</a></li>
</ol>
</li>
	<li><a href="#catalina_plugin">Catalina Plugin for Tomcat, JBoss and Wildfly.</a>
<ol>
	<li><a href="#catalina_plugin_configurations">Configurations.</a></li>
</ol>
</li>
	<li><a href="#glassfish_plugin">Glassfish Plugin.</a>
<ol>
	<li><a href="#jetty_integration_configurations">Configurations.</a></li>
</ol>
</li>
	<li><a href="#jetty_plugin">Jetty Plugin.</a>
<ol>
	<li><a href="#jetty_integration_configurations">Configurations.</a></li>
</ol>
</li>
</ol>
</li>
	<li><a href="#event_filters">Custom Event Filters.</a></li>
    <li><a href="#monitoring">Monitoring And Management.</a></li>
	<li><a href="#unit_testing">Unit testing with Audit4j.</a></li>
    <li><a href="#performance_tuning">Performance Tuning.</a></li>
	<li><a href="#plugin_development">Plugin developments.</a></li>
</ol>
&nbsp;
<h2><a name="introduction"></a>1. Introduction</h2>
Audit4j is an open source auditing framework which is a full stack application auditing solution for java enterprise projects. Refer the FAQ (frequently asked question) section for an overview of the application and the audit4j framework.

Audit4j is Open Source and available under the Apache 2 License.

Download from <a href="http://audit4j.org/downloads">http://audit4j.org/downloads</a>.

Code examples are prepared, which are included in a set of demo projects in order to demonstrate the usage of Audit4j and its plugins. For further information, please refer the following URL in order to access the project on Github.

<a href="http://github.com/audit4j/audit4j-demo">http://github.com/audit4j/audit4j-demo</a>

This documentation undergoes constant modifications (i.e.: added features, improvements, etc).

This document serves as the guide to the Audit4j framework. It explains the integration of the application, its configuration, optimization, security and usage of the plugin.

&nbsp;
<h2><a name="requirements"></a>2. requirements</h2>
Audit4j has been tested on a common distributions of Linux, Windows and Mac OS. Even though Audit4j is entirely built on Java, it will run on any operating system where the JVM (Java Virtual Machine) is installed. The Audit4j Core 2.x.x binaries require the JDK (Java Development Kit) version 7.0 or above.

&nbsp;
<h2><a name="installation"></a>3. Installation</h2>
You can download the latest version of Audit4j from the download page, or you can add the repository for Maven, Ant or Gradle. Please refer the download page for more information.

&nbsp;
<h2><a name="configuration"></a>4. Configuration</h2>
Even though Audit4j is designed to run with minimum configurations, it still provides various options for customization. Currently, YAML and XML are file formats that are supported.

The Audit4j configuration module uses a set of predefined instructions to load the config file. This allows the user to externalize the configurations from various locations including the environment variable, system variable, classpath lookup, as well as simple file or directory path. Hence, you can work with the same application code in
different environments as per the requirement.

The Audit4j configuration lookup algorithm is in the following order;

<ul>
	<li>1. Check whether configurations that are directly injected are available in the Context. If available; proceed with the injected configuration. If not, jump to step 7.</li>
</ul>
<ul>
	<li>2. Check if the configuration file or directory path is injected to the context. If available, it scans for a YAML (audit4j.conf.yml/audit4j.conf.yaml) or XML (audit4j.conf.xml) configuration file.</li>
</ul>
<ul>
	<li>3. Scans for the environment variable called "AUDIT4J_CONF_FILE_PATH" in order to locate the configuration file.</li>
</ul>
<ul>
	<li>4. Locate the Java system property variable called “audit4j.conf.file.path” to retrieve the configuration file.</li>
</ul>
<ul>
	<li>5. Searches for the application classpath in order to load the YAML or XML configuration file.</li>
</ul>
<ul>
	<li>6. Check for the user directory (user-dir) for the configuration file. If the file is not available, proceed to step 7.</li>
</ul>
<ul>
	<li>7. If config file is not available in the predefined or detected directory, a YAML configuration file with the default options is automatically created.</li>
</ul>
Users do not have to create the initial configuration file. If the configuration file is not found, audit4j will automatically create a new configuration file with the default settings in the relevant path, using the above algorithm. It will be easier to make changes around a newly created configuration file.

&nbsp;
<h3><a name="configuration-file"></a>4.1 Configuration File</h3>
Audit4j uses a <a href="http://yaml.org">YAML </a>like markup language in the main configuration file, which will make it easier to read and understand the syntax when compared with a traditional approach (i.e.: XML, JSON, etc). When initializing audt4j, a scan will commence for a configuration file; "audit4j.conf.yml".

The sample configuration file will look like;
```js
!Configuration # Mandetory

# Configure handlers, One or more handlers must be configured.

handlers:
- !org.audit4j.core.handler.ConsoleAuditHandler {}
- !org.audit4j.core.handler.file.FileAuditHandler {}

# Configure layouts, Either one handler must be configured.

layout: !org.audit4j.core.SecureLayout {}

# Configure meta data.

metaData: !org.audit4j.core.DummyMetaData {}

# Configure additional properties.
properties:
log.file.location: user.dir
```
<h3><a name="configuration-servlet-context"></a>4.2 Servlet Context Configurations</h3>
For Java web applications, Audit4j supports the loading of configurations from the web application classpath. Optionally it supports the customization of configuration attributes as context-params in a web.xml file.

Servlet context configurations support for Servlet-2.x specification as well as Servlet-3 specification.

1. For Servlet spec 2.x
   ```xml
   <listener>
   <listener-class>org.audit4j.core.web.AuditContextListener</listener-class>
   </listener>
   ```

For servlet 3 spec you don't want to configure in web.xml.


<h3><a name="configuration-spring"></a>4.3 Spring Configurations</h3>
Audit4j supports configurations in the spring application context. Please refer the <a href="#spring_audit4j_configurations">Spring Integration</a> section under Plugins for more information.

<h2><a name="sending_events"></a>5. Sending audit events</h2>
<h3><a name="sending_events_call"></a>5.1 Calling Audit Manager</h3>
The easiest way to integrate Audit4j with your application is by adding the Audit4j core module. Download the instructions here. To send audit records you need to call the Audit Manager.

#### Java
```java
public void myMethod(String myParam1, Object myParam2) {
String actor = MyApplicationContext.getAuthanticatedUser();
AuditManager manager = AuditManager.getInstance();
manager.audit(new AuditEvent(actor, "myMethod", new Field("myParam1Name", myParam1),
new Field("myParam2Name", myParam2)));
}
```

#### Scala
```scala
def myMethod(myParam1: String, myParam2: AnyRef) {
val actor = MyApplicationContext.getAuthanticatedUser
val manager = AuditManager.getInstance
manager.audit(new AuditEvent(actor, "myMethod", new Field("myParam1Name", myParam1), new Field("myParam2Name",
myParam2)))
}
```


Or using Event Builder
#### Java

```java
String actor = MyApplicationContext.getAuthanticatedUser();
EventBuilder builder = new EventBuilder();
builder.addActor(actor).addAction("myMethod").addField("myParam1Name", myParam1).addField("myParam2Name", myParam2);
AuditManager manager = AuditManager.getInstance();
manager.audit(builder.build());
```


#### Scala

```scala
val actor = MyApplicationContext.getAuthanticatedUser
val builder = new EventBuilder()
builder.addActor(actor).addAction("myMethod").addField("myParam1Name", myParam1)
.addField("myParam2Name", myParam2)
val manager = AuditManager.getInstance
manager.audit(builder.build())
```


#### groovy


&nbsp;
<h3><a name="annotations"></a>5.2 Using annotations</h3>
Without writing codes inside the method, audit records can be sent using annotations.

Before using annotation please refer <em><a href="#metadata">Meta DataSpring</a> section for more details.</em>

Annotations can be used through below plugins.
1. "<a href="/audit4j/integration-spring/"></a>"
2. "<a href="/audit4j/integration-weld">Weld</a>"

The annotations given below are available with Audit4j.

<h4>5.2.1 @Audit</h4>
@Audit annotation can be used either in class level or method level. The following options are available in Audit annotation

Example:
```java
@Audit
public void foo(Integer bar){
```

&nbsp;

[su_table]
<table style="height: 54px;">
<tbody>
<tr>
<th style="width: 100px;">@Audit Attribute</th>
<th style="width: 700px;">Description</th>
<th style="width: 700px;">Default</th>
</tr>
<tr>
<td>action</td>
<td>Custom action name.</td>
<td>Method name</td>
</tr>
<tr>
<td>repository</td>
<td>Used to route audit record into different repositories. As an example, for a different audit table. repository is given by the table name.</td>
<td>default</td>
</tr>
</tbody>
</table>
[/su_table]

&nbsp;
<h4>5.2.2 @AuditField</h4>
@AuditField Annotation is used to mark parameters which will include in the audit event.

[su_table]
<table style="height: 54px;">
<tbody>
<tr>
<th style="width: 100px;">@AuditField
Attributes</th>
<th style="width: 700px;">Description</th>
</tr>
<tr>
<td>field</td>
<td>Marked field name.</td>
</tr>
</tbody>
</table>
[/su_table]


&nbsp;

<h4>5.2.3 @IgnoreAudit</h4>
This annotation can be used in below scenarios.

1. When The particular class marked for audit using @Audit annotation but specific method should not be audited, This annotation can be added.

Example:
```java
@Audit
public class UserService {
@IgnoreAudit
public void changePassword(String oldPassword, String newPassword) {
// This method will not be audited.
}
}
```

2. Mark method field which should not be audited.

```java
public class UserService {
@Audit
public void login(String username, @IgnoreAudit String password) {
// password parameter will not be audited.
}
}
```


3. Skip auditing method object field.

```java
public class UserService {
@Audit
public void saveUser(User user) {
// password parameter in user object will not be audited.
}
}


public class User {

private String username;
@IgnoreAudit
private String password;

//Getters and Setters
}
```


&nbsp;
<h4>5.2.4 @DeIdentify</h4>
@DeIdentify can be used to deidentify certain fields. This applies a mask for certain characters with '*'. Please read <a href="#deidentification">Data De-identification</a> section for more information.

Example:

```java
@Audit
public void saveCreditCardId(@DeIdentify(left=5) int cardId){
```

Sample input card id: 123456789
Audited record: *****6789

[su_table]
<table style="height: 54px;">
<tbody>
<tr>
<th style="width: 100px;">@DeIdentify
Attributes</th>
<th style="width: 700px;">Description</th>
</tr>
<tr>
<td>left</td>
<td>De identify left characters. Ex: @DeIdentify(left=3) -&gt; ***456789</td>
</tr>
<tr>
<td>right</td>
<td>De identify rightcharacters. Ex: @DeIdentify(right=3) -&gt; 123456***</td>
</tr>
<tr>
<td>fromLeft</td>
<td>De identify all characters from the position left. Ex: @DeIdentify(fromLeft=3) -&gt; 123******</td>
</tr>
<tr>
<td>fromRight</td>
<td>De identify all characters from the position right. Ex: @DeIdentify(fromRight=3) -&gt; ******789</td>
</tr>
</tbody>
</table>
[/su_table]

&nbsp;
<h2><a name="metadata"></a>6 Meta Data Implementation</h2>
If you are using annotations to capture audit records, a custom meta-data class should be implemented. Audit4j will not receive certain information using annotations (i.e.: information regarding the logged in user and origin). In such a scenario, Audit4j will add some dummy data into your audit record. This can be carried out easily by implementing org.audit4j.core.MetaData class.

Example for the custom metadata implementation:

```java
import org.audit4j.core.MetaData;
public class MyMetaData implements MetaData{
@Override
public String getActor() {
return MyContext.getAuthanticatedUSer();
}

    @Override
    public String getOrigin() {
        return MyContext.getRemoteAddress();
    }
}
```

Configurations:

[js]
!Configuration
...
# Configure meta data.
metaData: !com.myapp.meta.MyMetaData {}
...
[/js]

&nbsp;
<h2><a name="layouts"></a>7 Using layouts</h2>
Layouts allow you to format individual audit events when it is being stored in the file or console. This will provide out-of-the-box support to encrypt, encode, organize, separate and filter audit information.

Here is an example of a formatted audit event;
<blockquote>08/16/2014 13:52:09|Audit4j User|Origin3|myMethod3==&gt;myParam1Name03 java.lang.String:param103,</blockquote>
&nbsp;
<h3><a name="layout-simple"></a>7.1 Simple Layout</h3>
Simple layout will format audit information by applying special characters (pipe-|,space, comma, arrow - =&gt;&gt; and colon - : ).

Configurations:

[js]
!Configuration
...
# Configure layout
layout: !org.audit4j.core.SimpleLayout{}
dateFormat: MM-dd-yyyy HH:mm:ss # Optional. Default will use MM/dd/yyyy HH:mm:ss
...
[/js]

&nbsp;
<h3><a name="layout-secure"></a>7.2 Secure layout</h3>
Using the secure layout you will be able to encrypt sensitive audit information.
If you are using the secure layout you need to add a secure key and salt in the Audit4j configurations as below.

Configurations:

[js]
!Configuration
...
# Configure layout
layout: !org.audit4j.core.SecureLayout{}
dateFormat: MM-dd-yyyy HH:mm:ss # Optional. Default will use MM/dd/yyyy HH:mm:ss
...
[/js]

<h3><a name="layout-customizable"></a>7.3 Customizable Layout</h3>
By using a customizable layout, the output format can be modified using templates. The Audit4j event stream gives you the following variables to build a template for a customizable layout.

${eventDate} - Event created date time
${uuid} - Auto generated uuid
${actor} - Actor
${action} - Action
${origin} - Origin
${fields} - Audit Fields

The operations below can be used as a option
looping:
${foreach fields field}${field.name} ${field.type}:${field.value}, ${end}

Conditions:
${if fields == null} No Results ${end}

Example for a template.

${eventDate}|${uuid}|${actor}|${action}|${origin} =&gt; ${foreach fields field}${field.name} ${field.type}:${field.value}, ${end}

The Java Minimal Template Engine (JMTE) is the best template engine we found so far in terms of performance. Thus, all the syntax of JMTE can be applied to Customizable Layouts.

&nbsp;
<h2><a name="deidentification"></a>8 Data de-identification</h2>
On certain occasions, users will want to audit sensitive information (User email addresses, Credit card numbers, etc). This information should be unidentifiable to third parties, but still at some extent be identifiable to achieve our purposes. This can be achieved using the de-identify feature in the Audit4j platform.
De-identification currently supports annotations called “@DeIdentify” which can be used in fields level.

Please see @DeIdentify annotation for more information.

&nbsp;
<h2><a name="plugins"></a>9 Plugins</h2>
&nbsp;
<h3><a name="database_handler"></a>9.1 Database handler</h3>
Database audit handler supports the capturing of audit records with popular databases (MySQL, Oracle, SQL Server, etc.). HSQLDB is embedded in to the database audit handler, but we are not recommending to use it in production systems since sensitive audit records better to store in a different location managed by the user.

&nbsp;
<h4><a name="configure_database_handler"></a>9.1.1 Configure database handler</h4>
Before starting the configuration you should refer the configuration section in the audit4j documentation.

The following line should be added under the handler: section in the audit4j.conf.yml file.
<blockquote>- !org.audit4j.handler.db.DatabaseAuditHandler{}</blockquote>
After this configuration Audit4j will record any audit events in the embedded database. The database file will automatically be created in the class-path. If you want to configure any other database, please refer the Database Configuration section below.

&nbsp;
<h4><a name="configure_external_databases"></a>9.1.2 Configure external databases</h4>
If you want to configure any other database, you should disable the one already active. You then need to select the connection type; if it is a single connection, a connection pool or a jndi data source.

connection type parameters as below:
Single Connection - single
Connection Pool - pooled
Jndi Datasource - jndi

Other configurations are usual connection parameters.

[js]
- !org.audit4j.handler.db.DatabaseAuditHandler
  embeded: false
  db_connection_type: pooled
  db_driver: com.mysql.jdbc.Driver
  db_url: jdbc:mysql://localhost/audit4j
  db_user: username
  db_password: password
  [/js]

&nbsp;
<h4><a name="configure_jndi"></a>9.1.3 Configure jndi datasources</h4>
&nbsp;

[js]
- !org.audit4j.handler.db.DatabaseAuditHandler
  embeded: false
  db_connection_type: jndi
  db_jndi_datasource: java:comp/env/jdbc/database
  [/js]

&nbsp;
<h4><a name="configure_datasource"></a>9.1.4 External Data Sources.</h4>
External data sources can be directly injected into the audit4j configurations before starting the audit4j server. Noted below is an example for the spring configuration.

```java
@Bean
public DataSource dataSource() {
// Application Datasource configurations.
}

@Bean
public DatabaseAuditHandler databaseHandler() {
DatabaseAuditHandler dbHandler = new DatabaseAuditHandler();
dbHandler.setEmbedded("false");
dbHandler.setDataSource(dataSource());
return dbHandler;
}
```

&nbsp;
<h4><a name="configure_pool"></a>9.1.5 Configure Connection Pool.</h4>
The Audit4j Database plugin uses Hikari as its default connection pool. The Audit4j DB API exposes the additional configuration options in order to fine-tune the connection pool. The following parameters are supported as optional configuration options.

[su_table]
<table style="height: 54px;">
<tbody>
<tr>
<th style="width: 100px;">Property</th>
<th style="width: 700px;">Description</th>
<th style="width: 700px;">Default value</th>
</tr>
<tr>
<td>db_pool_autoCommit</td>
<td>This property controls the default auto-commit behavior of connections returned from the pool</td>
<td>true</td>
</tr>
<tr>
<td>db_pool_connectionTimeout</td>
<td>Controls the maximum number of milliseconds that a client (that's you) will wait for a connection from the pool</td>
<td>3000 (30 seconds)</td>
</tr>
<tr>
<td>db_pool_idleTimeout</td>
<td>controls the maximum amount of time that a connection is allowed to sit idle in the pool</td>
<td></td>
</tr>
<tr>
<td>db_pool_maxLifetime</td>
<td>controls the maximum lifetime of a connection in the pool.</td>
<td></td>
</tr>
<tr>
<td>db_pool_minimumIdle</td>
<td>This property controls the minimum number of idle connections that HikariCP tries to maintain in the pool.</td>
<td></td>
</tr>
<tr>
<td>db_pool_maximumPoolSize</td>
<td>This property controls the maximum size that the pool is allowed to reach, including both idle and in-use connections.</td>
<td>100</td>
</tr>
</tbody>
</table>
[/su_table]
<h4><a name="configure_multipletables"></a>9.1.6 Multiple tables.</h4>
An audit stream can be routed to multiple tables in a database handler. This feature can be activated by enabling separate table configurations as below.

[js]
- !org.audit4j.handler.db.DatabaseAuditHandler
  separate: true
  [/js]

if you are using annotations events can be tagged for the table name in @audit annotation or simply add tagged information to audit event..

```java
@Audit (tag=”login”)
```

<h3><a name="file_handler"></a>9.2 File handler</h3>
Audit4j in-built file handler will save audit events in files with various configuration options.
Configuration:

[js]
!Configuration

handlers:
- !org.audit4j.core.handler.file.FileAuditHandler {}
  [/js]

<h4><a name="file_auto_archive"></a>9.2.2 Auto Archive</h4>
&nbsp;
<h3><a name="spring_integration"></a>9.3 Spring Integration</h3>
Audit4j-Spring is a plugin for Audit4j for integration between Spring and Audit4j Core. It will enable the below features in addition to the core functionalities.
<ul>
	<li>Annotation driven auditing.</li>
	<li>Configurations in the Spring Application Context.</li>
</ul>
&nbsp;
<h4><a name="spring_integration_configurations"></a>9.3.1 Configurations</h4>
Spring integration extension enables the annotation processing using two ways. You can use either one method as you preferred.

1. Spring AOP configurations:

[xml]
<bean id="auditAspect" class="org.audit4j.integration.spring.AuditAspect" />

<aop:aspectj-autoproxy>
<aop:include name="auditAspect" />
</aop:aspectj-autoproxy>
[/xml]

2. Spring Advice configurations:
   The bean given below should be configured in the spring configuration file.

[xml]<bean id="auditAdvice" class="org.audit4j.integration.spring.AuditAdvice" />[/xml]

After initiating the bean, it should be injected in to the spring transaction proxy under the particular Service as follows;

[xml]
<bean id="serviceClassImpl" class="com.myproject.ServiceImpl">
<!-- properties here -->
</bean>

<bean id="serviceImplProxy"
class="org.springframework.aop.framework.ProxyFactoryBean">
<property name="target" ref="serviceClassImpl" />
<property name="interceptorNames">
<list>
<value>auditAdvice</value>
</list>
</property>
</bean>
[/xml]

&nbsp;
<h4><a name="spring_audit4j_configurations"></a>9.3.1 Audit4j Configuration with spring</h4>
The Audit4j-Spring plugin supports out-of-the-box configuration options with spring. The bean shown below should be configured in the spring application context.

[xml]
<bean id="layout" class="org.audit4j.core.SimpleLayout"></bean>
<bean id="metaData" class="com.myproject.util.AuditMetaData"></bean>
<bean id="consoleAuditHandler" class="org.audit4j.core.handler.ConsoleAuditHandler"></bean>
<bean id="databaseAuditHandler" class="org.audit4j.handler.db.DatabaseAuditHandler">
<property name="embedded" value="false"></property>
<property name="db_connection_type" value="jndi"></property>
<property name="db_jndi_datasource" value="java:comp/env/jdbc/database"></property>
</bean>
<bean id="auditconfig" class="org.audit4j.integration.spring.SpringAudit4jConfig">
<property name="layout" ref="layout"></property>
<property name="metaData" ref="metaData"></property>
<property name="handlers">
<list>
<ref bean="consoleAuditHandler"/>
<ref bean="databaseAuditHandler"/>
</list>
</property>
</bean>
[/xml]

&nbsp;
<h3><a name="cdi-integration"></a>9.4 Audit4j for CDI spec implementations (Jboss Weld)</h3>
[su_label type="warning"]beeta[/su_label]
<h4><a name="cdi-integration-configurations"></a>9.4.1 Configurations.</h4>
Configuration for Jboss Weld:

[xml]
<beans
...
<interceptors>
<class>org.audit4j.intregration.cdi.AuditInterceptor</class>
</interceptors>
</beans>
[/xml]

&nbsp;
<h3><a name="http-integration"></a>9.5 HTTP Integration.</h3>
<h4><a name="http-integration-configurations"></a>9.5.1 Configurations.</h4>
web.xml configuration.

[xml]
<filter>
<filter-name>auditFilter</filter-name>
<filter-class>org.audit4j.intregration.http.AuditFilter</filter-class>
</filter>

<filter-mapping>
   <filter-name>auditFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
[/xml]

&nbsp;
<h3><a name="catalina-integration"></a>9.6 Catalina Plugin for Tomcat, JBoss and Wildfly.</h3>
[su_label type="warning"]beeta[/su_label]
<h4><a name="catalina-integration-configurations"></a>9.6.1 Configurations.</h4>
Put audit4j-core-2.3.1-all.jar(or higher) and audit4j-tomcat-2.3.1.jar in the tomcat 'lib' directory.
Add the following Valve line to Tomcat's server.xml file. The 'Engine' line is used to show context.

[xml]
<Engine name="Catalina" defaultHost="localhost">
<Valve className="org.audit4j.intregration.tomcat.Audit4jTomcatValve"/>
[/xml]

&nbsp;
<h3><a name="glassfish-integration"></a>9.7 Glassfish Plugin</h3>
[su_label type="warning"]beeta[/su_label]
<h4><a name="glassfish-integration-configurations"></a>9.7.1 Configurations.</h4>
For glashfish 4.0+

[xml]
<sun-web-app ...>
...
<property name="auditValue" value="org.audit4j.intregration.glassfish.Audit4jGlashfishValue"/>
</sun-web-app>
[/xml]

&nbsp;
<h3><a name="jetty-integration"></a>9.8 Jetty Plugin</h3>
[su_label type="warning"]beeta[/su_label]
<h4><a name="jetty-integration-configurations"></a>9.8.1 Configurations.</h4>
For Jetty 8,9+
Server Mode:

[xml]
<Set name="handler">
...
<Item>
<New id="auditHandler" class="org.audit4j.intregration.jetty.Audit4jJettyHandler"/>
</Item>
</Set>
[/xml]

Embedded Mode:

```java
Server server=new Server(8080);
...
Audit4jJettyHandler wrapper =  new Audit4jJettyHandler();
server.setHandler(wrapper);
server.start();
}
```

For Jetty 6.1.5
Server Mode:
Put audit4j-core-2.3.1.jar(or higher) and audit4j-tomcat-2.3.1.jar in the jetty 'lib/etc' directory.

[xml]
<Set name="handler">
...
<Item>
<New id="auditHandler" class="org.audit4j.intregration.jetty.Audit4jJetty6Handler"/>
</Item>
</Set>
[/xml]

&nbsp;
<h2><a name="event_filters"></a>10 Custom Event Filters.</h2>
Custom filters are used to screen audit events. Custom filter should implement <a href="/apidocs/core/latest/org/audit4j/core/filter/AuditEventFilter.html">AuditEventFilter </a>interface.

Sample custom event filter implantation, This filter will not accepts the events with action "DummyAction".

```java
public class CustomFilter implements AuditEventFilter {
@Override
public boolean accepts(AuditEvent event) {
if (event.getAction().equals("DummyAction")) {
return false;
}
return true;
}
```

Optionally filters provides the filter query language to simplify the development. Below filter will filter events with action, "Action1" or "Action2".

```java
public class CustomFilterWithQuery implements AuditEventFilter{
@Override
public boolean accepts(AuditEvent event) {
if (query.from(event).with("action").eq("Action1").or().eq("Action2").evaluate()) {
return false;
}
return true;
}
```

&nbsp;
<h2><a name="monitoring"></a>11 Monitoring And Management</h2>
Audit4j can be monitored and managed using Java Management Extensions (JMX). In other words, JMX can be used to monitor the Audit4j server status and manage basic server operations including starting, stopping, enabling and disabling. JMX can be enabled via the configuration due to the fact that the JMX setting is disabled by default. Use below configurations to enable JMX.

[js]
jmx: !org.audit4j.core.jmx.JMXConfig {}
[/js]

&nbsp;
<h2><a name="unit_testing"></a>12 Unit testing with audit4j</h2>
Audit4j supports the use of different settings other than production settings for unit tests in Audit4j integrated applications. Different configurations for test scope will be supported by Audit4j. As an example, if you need to point to a different database for audit trails in your unit tests, Audit4j provides an API which enables the use of different configurations in unit test classes.

Configurations should be added to a setup method in your unit test class before initiating Audit4j.

```java
@Before
public void before() {
AuditManager.startWithConfiguration("/home/audit4j/audit4j-test.conf.yml");
}
```

Write your test cases as usual.

```java
@Test
public void test(){
......
}
```

&nbsp;

Make sure you shut down the Audit4j context in teardown method to clear the audit4j resources.

```java
@After
public void after() {
AuditManager.getInstance().shutdown();
}
```

&nbsp;
<h2><a name="performance_tuning"></a>13 Performance Tuning</h2>
Audit4j supports limited options to improve performance in your application. These options are not enabled by default because they are highly depend on your applications’ nature and the system environment.
<h3><a name="performance_tuning_metadata"></a>13.1 Metadata lookup in async mode</h3>
By default metadata lookup is setted to sync mode and this can be changed to async mode by using below configuration.

[js]
commands: -metadata=async
[/js]

Warning: The metadata lookup will not work if your application framework doesn’t allow invoking metadata information asynchronously.

&nbsp;
<h2><a name="plugin_development"></a>14 Plugin Development</h2>