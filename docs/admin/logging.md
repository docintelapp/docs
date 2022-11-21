---
layout: default
title: Logging
parent: Administration Guide
---

# Logging

Logging is a crucial part of software development. It helps us track what the
software is doing and makes sure that it is running correctly. Without logging,
we would be flying blind, and it would be very difficult to debug any issues
that might arise. Logging also provides valuable insights into how the software
is being used. We can use this data to improve the user experience or to make
performance tweaks. In short, logging is an essential tool for any software
development team.

Sometimes, too much logging can be a problem. This is because it can make the
software slow down or fill your disk. It's important to make sure that you only
log the information that you need, and that you filter out any unnecessary
data. Otherwise, you might end up with a lot of logs that are difficult to read
and understand.

To configure the logging in DocIntel, you need to edit the file `nlog.config`
You can read about the detailled options in the [documentation of
NLog](https://nlog-project.org/config/).

For example, the following will only display the logs that have a level above
Warning. 

```
<?xml version="1.0" encoding="utf-8" ?>
<!-- XSD manual extracted from package NLog.Schema: https://www.nuget.org/packages/NLog.Schema-->
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" xsi:schemaLocation="NLog NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      autoReload="true">

  <!-- the targets to write to -->
  <targets>
    <target name="coloredConsole" xsi:type="ColoredConsole" useDefaultRowHighlightingRules="false"
      layout="${longdate} [${level:uppercase=true}] [${logger}] ${message}" >
        <highlight-row condition="level == LogLevel.Debug" foregroundColor="DarkGray" />
        <highlight-row condition="level == LogLevel.Info" foregroundColor="Gray" />
        <highlight-row condition="level == LogLevel.Warn" foregroundColor="Yellow" />
        <highlight-row condition="level == LogLevel.Error" foregroundColor="Red" />
        <highlight-row condition="level == LogLevel.Fatal" foregroundColor="Red" backgroundColor="White" />
    </target>
  </targets>

  <!-- rules to map from logger name to target -->
  <rules>
    <logger name="*" minlevel="Warn" writeTo="coloredConsole" />
  </rules>
</nlog>
```



