So **chkconfig**

chkconfig has five distinct functions: adding new services for  management,  removing  services  from management, listing the current startup information for services, changing the  startup  information  for  services, and checking the startup state of a particular service.

For example
```
$sudo chkconfig mysqld on
```
will start mysql server whenever system start up (or restart)

Some useful utilities:
```
// this will display a list of system services
$chkconfig --list

// this will enable/disable service
$chkconfig service_name on/off
```
