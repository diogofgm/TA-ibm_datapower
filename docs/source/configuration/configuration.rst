=============
Configuration
=============

Splunk
------
- Configure a new index (e.g. storage) for the new logs

The IBM Datapower Add-on contains two base sourcetypes:
- ibm:datapower:syslog - this should be used if you are sending data via UDP
- ibm:datapower:syslog:tcp - this should be used if you are sending data via TCP

The reason behind having multiple base sourcetypes is due to the fact that DataPower logs diferent timestamp formats  depending on how you are sending the logs.
- Sending data via UDP doesn't allow for much configuration and the timestamp will look something like "Jul 10 10:45:32".
- Sending data via TCP allows for extra time granularity since you can choose to include the microseconds and time zone. It will look something like "2019-07-10T10:45:32.123415+01:00". 

Receiving syslogs on Splunk
~~~~~~~~~~~~~~~~~~~~~~~~~~~
NOTE: Its recommended to use a separate and dedicated syslog solution (e.g. rsyslog, syslog-ng, etc)
- Configure new TCP port (e.g. 514) pointing to the new index using the "ibm:datapower:syslog:tcp" sourcetype

Monitoring log files
~~~~~~~~~~~~~~~~~~~~
- Configure a new file monitor input pointing to the new index using the "ibm:datapower:syslog:tcp" sourcetype

IBM DataPower
-------------
- Configure syslog outputs
For more information please refer to the `IBM DataPower documentation`_.



.. _IBM DataPower documentation: https://www.ibm.com/support/knowledgecenter/SS9H2Y_7.5.0/com.ibm.dp.doc/logtarget_configuring.html