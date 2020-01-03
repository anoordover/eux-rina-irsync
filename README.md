# eux-rina-irsync

Small app offering scheduled RINA IR SYNC (and a REST API with Swagger) using RINA SDK.

## main functionality

* sync IR

## quickstart

* you want this directory structure, including an empty logs directory
```
eux-rina-irsync/
├── config/
│   ├── application.yml
├── logs/
│  
└── eux-rina-irsync-0.9.4-SNAPSHOT.jar
```
* download the eux-rina-irsync-0.9.4-SNAPSHOT.jar
* download config/application.yml
* adopt config/application.yml to your environment
* run 
```bash
java -Djava.util.concurrent.ForkJoinPool.common.parallelism=16 -jar eux-rina-irsync-0.9.4-SNAPSHOT.jar
```
  
## known shortcomings

* this version assumes that it takes less than four minutes to request potentially new IR content from your AP, i.e. that your anti-
  malware does not take more than four minutes. If it does, don't worry, eux-rina-irsync will pick up the message on the next pass after
  20 minutes.
  
* The above mentioned four minutes cannot be configured, the 20 minutes can, see application.yml 
IRSYNC scheduling properties
cron:
  syncRate: 1200000
  
* eux-rina-irsync needs the RINA CPI SDK patches from ResourcesApi.path in order to work. They are included in the source here at
  eu.ec.dgempl.eessi... and compiled into the fat jar if you use e.g. maven install.

* this is a scaled down branch of NAV's EUX RINA ADMIN tools to administer several things in RINA, like users/password, roles, NIE, etc.
  The full functionality is rather customized to NAV, and honestly we don't have the spare time to generalize it.
  
* currently, only one RINA can be addressed. Full EUX RINA ADMIN supports many RINAs called "tenants" in application.yml.
  IR SYNC only supports one, because of how we use admin username and password in our TEST and ACCEPTANCE environments. 
  
## TODOs

* http://nssm.cc/ Windows service implementation (small configuration job, coming in early January 2020)
* Ubuntu service implementation
* Reintroduce support for multiple RINAs
* or
* remove the possibly complicated code and config for admin username and password.