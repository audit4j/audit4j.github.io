---
title: Documentation
excerpt: "Category index"
aside: false
---
<h3><a name="Audit4j"></a>What is Audit4j?</h3>
Audit4j is comprehensive auditing framework which can be used to track any kind of audit log including server, application and database. Audit4j is entirely annotation driven, hence you can adopt to your application using minimum configurations.
<h3><a name="TraceAndLog"></a>What is different between Audit trace and Log?</h3>
A log is often unpreserved whereas; an audit trace is <strong><em>secure</em> </strong>and <strong><em>preservable</em></strong>. As a result, recording sensitive information, or data which will be required at a later time will not be handled by a log. Other issue is usually logs are not recording actor(Who did),  action(What did) and origin(Comes from), but audit log should contains those information. However, an audit trail addresses these issues.
<h3><a name="features"></a>What are the main features of Audit4j?</h3>
1. Can be Asynchronous/Synchronous, according to the requirement.
2. Scalable.
3. Fully customizable annotations.
4. In-built plugins (File and Console).
5. Minimum configurations.
6. Rich extendible API - Custom/third party plugins can be used by via the API.
   
<h3><a name="performance"></a>How is the performance after integrating the Audit4J with my application?</h3>
   Audit4J supports asynchronous events (and synchronous events – depends on the requirement).  Since the architecture is based on asynchronous event mechanisms, application will not be added additional latency (or less than 10 micro second.) after integrating the audit4j and its plugins.

<h3>How does the Audit4j architecture work?</h3>
   Audit4J is entirely based on a modular architecture. There are three different types of plugins that support connecting various types of external tools with the core module.

1. Caller Plugins - Sending audit events from various sources.
2. Layout Plugins - Format and organize audit events.
3. Handler Plugins - Process and save audit information.

The <a href="/audit4j/javadoc/"><i>javadoc</i> </a> can be referred in order to obtain further information regarding this.
<h3><a name="integrations"></a>Currently, what are the available integrations for Audit4j?</h3>
1.Audit4j-Spring Integration.
2.Audit4j-Weld Integration.
3.Audit4j-Guice Integration.
4.Audit4j-database Integration.
5.Audit4j-http.
