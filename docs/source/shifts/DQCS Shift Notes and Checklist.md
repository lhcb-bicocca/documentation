# DQCS Shift Notes and Checklist

## Documentation
* latest [training](https://indico.cern.ch/event/1139897/)
* [Shift DataBase](https://lbshiftdb.cern.ch/)
* [Bicocca Docs](https://lhcb-bicocca-docs.readthedocs.io/en/latest/shifts/dqcs.html)
* [Operation Meeting](https://indico.cern.ch/category/4206/) setup [instructions](https://lhcb-dqcs-docs.web.cern.ch/lhcb-dqcs-docs/operations-meetings.html) and [CodiMD](https://codimd.web.cern.ch/eeXrQ8C8QmeQwfDnGsgtSQ)
* [Simulation Meeting](https://indico.cern.ch/category/14788/) setup [instructions](https://lhcb-dqcs-docs.web.cern.ch/lhcb-dqcs-docs/mc-meetings.html) and [CodiMD](https://codimd.web.cern.ch/n0vdfaeRSQ-xBV2GYrdEvw)

## Prerequisites
- [ ] ELog access
- [ ] Subscribed to `lhcb-simulation`,`lhcb-distributed-analysis`,`lhcb-geoc` mailing lists
- [ ] Join `Simulation` and `Computing Operations` Mattermost Channels
- [ ] Get Grid Certificate
- [ ] `lhcb_shifter` role available on DIRAC portal
- [ ] test generation of DQCS report made from [this](https://github.com/mmazurekgda/nightly-status-checker) or  [this](https://github.com/alex-t-grecu/nightly-status-checker) repo

## MC Quality checks

Nightly Tests [docs](https://lhcb-dqcs-docs.web.cern.ch/lhcb-dqcs-docs/mc-monitoring-nightlies.html)
Gauss LHCbPR Tests [docs](https://lhcb-dqcs-docs.web.cern.ch/lhcb-dqcs-docs/mc-monitoring-lhcbpr.html)
Dirac portal [docs](https://lhcb-dqcs-docs.web.cern.ch/lhcb-dqcs-docs/monitoring.html)
### Every couple of hours
- [ ] Monitor [Dirac Portal](https://lhcb-portal-dirac.cern.ch/DIRAC/) plots for anomalies and report it on [Operation channel](https://mattermost.web.cern.ch/lhcb/channels/computing-operations) monitoring the plots on desktops (Concezio Bozzi's ones are OK). They appear going to "Settings->Group : lhcb_shifter". Then go to "Application->Administration->Public State Manager", select "Desktops->Shared Desktops" and choose the desktop with saved the plots to inspect. Report in Computing Operations

### Once a Day
- [ ]  Visit [LHCb Nightly builds reports](https://lhcb-nightlies.web.cern.ch/nightly) and update Simulation Data Quality [codimd](https://codimd.web.cern.ch/n0vdfaeRSQ-xBV2GYrdEvw)
*  - [ ] lhcb-sim10
*  - [ ] lhcb-sim10-dev
*  - [ ] lhcb-sim11
- [ ] Visit [LHCbPR Simulation dashboard](https://lblhcbpr.cern.ch/dashboards/simulation) for the following checks:
* - [ ] Gauss software performance check
* - [ ] Detailed check to commissioning future simulation campaign


### Once a Week
- [ ] Check [LHCb Nightly builds reports](https://lhcb-nightlies.web.cern.ch/nightly) 
*  - [ ] lhcb-sim11-g4
*  - [ ] lhcb-sim09-cmake
- [ ] Visit [LHCbPR Simulation dashboard](https://lblhcbpr.cern.ch/dashboards/simulation) for the following checks:
* - [ ] Run 2 detailed simulation check
* - [ ] Run 3 detailed simulation check


```
For each slot, check:

* the given slot builds for all platforms
* all merge requests were successfully merged in the given nightly slot
     * if there is an arrow next to the project name, click on the blue page icon and verify it in checkout log

* there are no new test failures that appeared for the x86_64_v2-centos7-gcc11-opt platform
    * compare to previous build (or few builds) using the [Compare with previous builds] button
    * compare the latest lhcb-sim10-dev slot with the latest lhcb-sim10 slot using the [Compare slots] button
```
:::warning
`lhcb-sim11` has more platform that needs to be monitored: `x86_64_v2-centos7-gcc11+detdesc-opt`, `x86_64_v2-centos7-gcc12-opt`, `x86_64_v2-centos7-gcc12+detdesc-opt` and `x86_64_v2-el9-gcc12-opt`
:::
:::info
The `*-dbg` tags are less important, especially as far as tests are concerned.
:::

# Week schedule

## Friday before
- [ ] [time=11:30] Attend [LHCb Computing Operations](https://indico.cern.ch/category/4206/) meeting to acknowledge the status of the system

## Monday
- [ ] [time=10:00] copy and update [LHCb Computing Operations](https://indico.cern.ch/category/4206/) meeting event and chair it asking news about the tiers and other topics
- [ ] do Once a day tasks
- [ ] check nightly report prepared by the previous shifter and update it using [this repo](https://github.com/alex-t-grecu/nightly-status-checker) and update Simulation Data Quality codimd
## Tuesday
- [ ] do Once a day tasks

- [ ] [time=16:30] attend [Simulation Meeting](https://indico.cern.ch/category/14788/) reporting information on previous week and upload a `.md` and a `.html` copy of this [codimd](https://codimd.web.cern.ch/n0vdfaeRSQ-xBV2GYrdEvw)
- [ ] clear out tables on codimd and start preparing the report for the next shifter

## Wednesday
- [ ] [time=10:00] copy and update [LHCb Computing Operations](https://indico.cern.ch/category/4206/) meeting event and chair it asking news about the tiers and other topics
- [ ] do Once a day tasks
## Thursday
- [ ] do Once a day tasks

## Friday
- [ ] [time=10:00] copy and update [LHCb Computing Operations](https://indico.cern.ch/category/4206/) meeting event and chair it asking news about the tiers and other topics
- [ ] do Once a week tasks
- [ ]  do Once a day tasks
## Saturday
- [ ]  do Once a day tasks
## Sunday
- [ ]  do Once a day tasks
- [ ] generate nightly report using [this repo](https://github.com/alex-t-grecu/nightly-status-checker) and update the [codimd](https://codimd.web.cern.ch/n0vdfaeRSQ-xBV2GYrdEvw) for the next user