=============
Configuration
=============

Splunk
------
- Configure a new index (e.g. storage) for the new logs

Receiving syslogs on Splunk
~~~~~~~~~~~~~~~~~~~~~~~~~~~
NOTE: Its recommended to use a separate and dedicated syslog solution (e.g. rsyslog, syslog-ng, etc)
- Configure new TCP port (e.g. 514) pointing to the new index using the "ibm:datapower:syslog" sourcetype

Monitoring log files
~~~~~~~~~~~~~~~~~~~~
- Configure a new file monitor input pointing to the new index using the "ibm:datapower:syslog" sourcetype

IBM DataPower
-------------
- Configure syslog outputs
For more information please refer to the `IBM DataPower documentation`_.



.. _IBM DataPower documentation: https://www.ibm.com/support/knowledgecenter/SS9H2Y_7.5.0/com.ibm.dp.doc/logtarget_configuring.html