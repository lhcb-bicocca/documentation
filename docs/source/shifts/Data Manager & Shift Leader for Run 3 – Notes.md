# Data Manager & Shift Leader for Run 3 -- Notes
[TOC]
## Useful links
- [ ] [Shift Database](http://lbshiftdb.cern.ch/)
- [ ] [ShifterFormalities](https://lbtwiki.cern.ch/bin/view/Operation/ShifterFormalities)
- [ ] [Shifter Instructions](https://lbtwiki.cern.ch/bin/view/Operation/ShifterInstructions)
- [ ] [Shifter Checklist](https://lbtwiki.cern.ch/bin/view/Operation/SoSchecklist)
- [ ] [Operation Twiki](http://lbtwiki.cern.ch/bin/view/Operation/WebHome)
- [ ] [Shift LogBook](https://lblogbook.cern.ch/Shift/)
- [ ] [MONET](https://lbwebmonet.cern.ch/)
- [ ] [MONET documentation](https://its.cern.ch/jira/projects/LHCBMONET/summary)
- [ ] [JIRA Monet problem database](https://its.cern.ch/jira/projects/LBRUNPROBLEMS/issues/?filter=allopenissues)
- [ ] [JIRA Monet development](https://its.cern.ch/jira/projects/LHCBMONET/summary)
- [ ] [Training slides](https://edms.cern.ch/ui/#!master/navigator/document?D:101448234:101448234:subDocs)
- [ ] [Mattermost channel](https://mattermost.web.cern.ch/lhcb/channels/lhcb-run3-shifter-support-channel)
- [ ] [Run Meeting ](https://indico.cern.ch/category/669/) @ 9:30
- [ ] [SLIMOS instructions](https://lbdokuwiki.cern.ch/infrastructure:instructionsforslimos)

## Acronyms


| Acronym   | Definition                                         | Note                       |
| --------- | -------------------------------------------------- | -------------------------- |
| AI        | Analog Inputs                                      |                            |
| BE_OP     | machine operations                                 |                            |
| BPIM      | Beam Phase and Intensity Monitor                   |                            |
| BCM       | Beam Conditions Monitor                            | or Main Background Monitor |
| CCC       | CERN Control ROOM                                  |                            |
| CR        | Control Room                                       |                            |
| DDS       | Detector Safety System                             |                            |
| DI        | Digital Inputs                                     |                            |
| DM        | Data Manager                                       |                            |
| DQ        | Data Quality                                       |                            |
| EIC       | Engineers-In-Charge                                | accelerator operations     |
| EN-CV     | CERN cooling group                                 |                            |
| EN-EL     | CERN electrical service                            |                            |
| ESO       | Electrical Safety Officer                          |                            |
| LBDS      | LHC Beam DUmp System                               |                            |
| LEXGLIMOS | Large Experiment Group Leader In Matters Of Safety |                            |
| LPC       | LHC PRogram Coordinator                            |                            |
| MC        | Machine Coordinators                               | Run Chief at CCC           |
| MD        | Machine Development period                         |                            |
| PT        | Temperature Probes                                 |                            |
| SL        | Shift Leader                                       |                            |
| SLIMOS    | Shift Leader In Matters Of Safety                  |                            |
| RC        | Run Coordinator                                    |                            |
| RSO       | Radiation Safety Officer                           |                            |
| TSO       | Territorial Safety Officer                         |                            |

## Phone Numbers
Prefix for CERN fixed numbers: +41 22 76 xxxxx
prefix for CERN mobile numbers: +41 75 411 xx xx

| Name                        | Number                                          |
| --------------------------- | ----------------------------------------------- |
| CCC                         | +41 22 76 (7 76 00)                             |
| CCC Techical Infrastructure | (7 22 21)                                       |
| Data manager                | +41 22 76 (6 35 96)                             |
| DSS piquet/GLIMOS           | (16 80 00)                                      |
| EP-DT magnet and DSS piquet | (16 20 82)                                      |
| Fire and Rescue             | +41 22 76 (7 44 44 urgent) (7 48 48 non-urgent) |
| LEXGLIMOS                   | (16 90 56)                                      |
| Run Chief                   | +41 22 75 411 1868 (+41 22 76 161868)           |
| Run Coordinator             | +41 22 76 (6 32 18)                             |
| Shift Leader                | +41 22 76 (fixed=63595, mobile=161866)          |
|                             |                                                 |

## Important
- [ ] subscribe to `lhcb-shift-leaders` and `lhcb-data-managers` mailing list
- [ ] `LHCB_S` and Control Room access permission

## Shifter Duties
- [ ] SL follow the [Run Meeting](https://indico.cern.ch/category/669/) when scheduled
- [ ] SL take data with the **Run Control**, **Operate Voltages and sub-detectors** in the `Big Brother`, handle handshakes and interlocks
- [ ] DM check **data quality and do data management**
- [ ] answer CCC phone when LHC call (if needed take notes for RC)
- [ ] Mostly relay information about the plan of the day, ongoing activities, accesses, problems, LHC status, sub-detectors information
- [ ] DM replace SL when outside CR
- [ ] write **anything happen** in the logbook
- [ ] Control Room Doors should be closed by 7pm
- [ ] Global monitoring panel of LHC: check system status (if problem report/call CCC?)
- [ ] Check if LHCb Timing is synchronous with LHC

## Data Manager Duties
- [ ] check the plots in the "Shift" folder continuously.
 ## SLIMOS Duties
- [ ] Follow up DSS alarms, acknowledge and reset.
- [ ] l

## Daily ToDo
- [ ] if night shifter print `Who's on shift today` @ 6am (select printer "color", printer near keys' cabinet)
- [ ] SL at the end should write a `Shift Summary` entry in the logbook: what happened in the LHC/LHCb and outstanding items to be done using proposed structure
- [ ] SLIMOS check to be logged into DSS as `slimos` and two LEDs next to `Alive` are alternating (if not restart app or reboot the PC)

# Module 1a: Central Shifters
Shift Leader (SL) and Data Manager (DM) refer directly to the Run Chief (**while on shift** and to the Run Coordinator in general) and in alternative to the Run Coordinator. For safety matter, they refer directly to the (LEX-)GLIMOS.

Tasks during operations are provided to you by the Run Chief and/or the Run Coordinator. SLs are in charge of safety but they are not in charge of security!

`LHCB_S` and Control Room access are mandatory for both DM and SL, while `LHCB_U` is strongly recomended for SL.

:::warning
Never ignore DSS or Level 3 alarms: call piquet and follow procedure explained in safety course (link ?)
:::
:::danger
Meeting point for emergencies = building 2890, always carry CERN Access Card
:::
:::info
Login for control room screens:
* user: lhcb_shift
* pswd: top of whiteboard, with ! in front...
:::

## Who you gonna call?
$$ try ~piquet \times 3 \rightarrow try~Run~Chief \rightarrow Run~Coordinator$$
* If you know you cannot make it on time, call the current Shift Leader and call the Run Chief
* If the incoming shifter does not show up within 15 minutes after the start time of the shift, the outgoing shifter should call the Run Chief
* The experts are also available to answer the phones, but first you should always call the sub-detector piquet of the concerned system
* If the call concerns the LHC or something that needs more escalating, call the Run Chief as well
* If there is a safety issue or an alarm, call 168000 (DSS piquet or GLIMOS)
* If in doubt about the LHC doings, call the CCC to clarify

## LHCb Run Control
- The `LHCb Run Control` is the main panel to control all devices needed for data taking: keep it <span style="color:green">`RUNNING`</span> configuration given by the RC
- The `Big Brother` : Main panel to control HV, interfaces to the LHC, clock, BCM, magnet. never ignore an <span style="color:red">`ERROR`</span>.
- The `Alarm Screen` : Never ignore alarms, always follow-up. Any observation, write it in the logbook. If you are in doubt, better call the concerned sub-system piquet.

## LHC cycle
- `Handshake`: $Injection\to Adjust\to Dump$. Done between LHC and all 4 experiments, controlled via Big Brother
- LHC filling scheme, naming convention
![](https://codimd.web.cern.ch/uploads/upload_0bc4126af68287e19f8451e998514bee.png)

| LHCb States | Note                       |
| ----------- | -------------------------- |
| INJECTION   | @ 450 GeV                  |
| RAMP        | @ 6.8 TeV                  |
| SQUEEZE     | beam transversally smaller |
| PHYS_ADJUST |                            |
| PHYSICS     |                            |
| ADJUST      |                            |
| DUMP        | get rid of beams           |
| EOF         |                            |
| NO_BEAM     |                            |

### LHCb Timing
The LHCb timing (clock) is centrally controlled/monitored via a set of electronics boards called RFRx, RF2TTC and BPIM. CHeck status on Big Brother
Two modes of operations:
- INTERNAL: clock is generated locally in LHCb for the whole detector
- EXTERNAL: clock is received via the LHC and it is in phase with the beams (synchronous)
:::warning
- LHCb Clock must be in EXTERNAL while in data taking mode!
- Phase of Beam 1 (blue) must stay within +/- 500ps (with some tolerance)
- DeltaT (difference in arrival time B1/B2 @ IP) within 100ps
:::

### LHCb safety
- LHCb Main Background Monitor rearms automatically if dump was not by itself $\to$ FSM state changes ABORT_PMT  $\to$ PM_READY  $\to$ READY
- if BCM dumps, and FSM stays in PM_READY waiting for manual Rearm  $\to$ CALL CCC "we have probably dumped and we are investigating", and CALL RC before rearming
-use the `Send to logbook` button to record unusual activity in the Monitoring beam-induced background

### LHCb Luminosity
PLUME monitor the LHCb luminosity

| Dictionary    | Definition                                                   | Note |
| ------------- | ------------------------------------------------------------ | ---- |
| $\nu$(nu)     | average number of pp interaction per bunch                   |      |
| $\mu$(mu)     | average number of **visible** pp interaction per bunch       |      |
| pileup        | average number of pp interaction in visible events           |      |
| cross-section | probability of how manu pp collisions per unit time and lumi |      |

Handle alert
| Alarm on screen                                                                  | LED status                                                     | Action                                                    |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------- |
| **LHC leveling receiver not running**                                            | First LED is grey and sentence red                             | Call CCC and ask them to enable the levelling application |
| **No response to leveling since 564 s**                                          | Second LED and sentence green, first LED grey and sentence red | Call CCC and ask them to perform levelling                |
| **X-plane optimization not done, LHCb Leveling master inhibited, please check!** | First LED and sentence green, second LED grey and sentence red | Call CCC and them to optimize LHCb in the crossing plane  |

if LHC is in Machine Development period, they screw arounf with the machine.
:::info
-General rule, if already in MD stay in MD at each injection handshake until next physics fill.
-Make sure the sub-detectors HV are in a state that it is consistent with the LHC activities
:::

# Module 1b: Online Monitoring
Checking live in the control room of the quality of the recorded data. Crucial for the running of LHCb: data with malfunctionning detector will most certainly be discarded for offline analysis.

Monitoring Control Unit controls the running of the monitoring tasks in the monitoring farm $\to$ It must be <span style="color:green">`RUNNING`</span> always when we take data

Data Sources:
- Detector raw data
- Reconstructed quantities: output of HLT or of reconstruction
monitoring jobs
- Environmental quantities, as a function of time: produced by
electronics, HV, ...
- And automatic analyses of these sources

## MONET
web [application](https://lbwebmonet.cern.ch/) Login with the CERN account (not the online one). Histograms can be looked at `Live` or in `History mode`.

- For online monitoring, the main folder to look at is `OnlineMon`
- The `Shift` folder that will contain a selection of important pages for the data
manager to inspect (1 or 2 pages per detector or system)
- The `Reload Tree` button can be used in case new folders were added by
monitoring experts, to see them (otherwise no need to use this button)
- `Prev` and `Next` buttons can be used to browse easily the pages: it will open the
previous or next pages in the folder structure

:::info
- Reference histograms are histograms selected by detector experts to show how the distributions are supposed to look like when everything works well
- if problem is spotted: click on `Send to ELOG` and follow instructions that could be written on the MONET page itself, and call the sub-detector piquet (if the problem is not solved quickly)
:::

A [JIRA site](https://its.cern.ch/jira/projects/LBRUNPROBLEMS/issues/?filter=allopenissues) where issues reported by data managers will be stored and followed up by detector piquets and experts

Some predefined histogram and data analyses are implemented to detect automatically problems in the distributions.

# Module 2a: Safety

Safety covers occupational health and safety, including radiation protection, the protection of the environment and the safe operation of CERN’s Installations (EDMS 1416908).
The responsibilities and organisational structure in matters of safety at CERN are described in Safety Regulation SR-SO (EDMS 1389540).
The Technical Coordinator is supported by the LEXGLIMOS and other safety officers: Radiation Safety Officer (RSO), Electrical Safety Officer (ESO), **Shift Leader In Matters Of Safety** (SLIMOS). Handling safety alarms takes precedence over other Shift Leader tasks.

SLIMOS are expected to:
* be knowledgeable about the safety aspects of the experiment
* handle alarms and emergency situations
* operate safety systems

Handling alarms usually involves contacting experts/piquets and – in case of Level-3 alarms – the CERN Fire and Rescue Service. The DSS/RPE piquet (16 80 00) is your first-line contact in LHCb for all matters of safety and technical infrastructure. (*as backup option use intercoms on Emergency Panel)

In case of **Evacuation**:
* Control Room assembly point outside the SY8 building
* Take the shift leader mobile phone and the list of contacts with you.
* Follow the instructions by the Territorial Safety Officer (TSO).
* Call the subsystem piquets and tell them to monitor the state of the detector.
* Call Run Chief and LEXGLIMOS.
* Wait for the Fire Brigade.



| Emergency           | Actions                                                                                                                                        |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Fire                | Call Fire and Rescue Service, set off evacuation alarm using buttons on the wall, put the fire out if without taking risks, otherwise evacuate |
| Medical Emergencies | Call Fire and Rescue Service, first-AID kit in control room and defibrillator outside in the corridor                                          |

## Detector Safety System (DSS)
The purpose is to detect abnormal and potentially harmful situations and minimise damage to the experiment’s equipment by taking automated protective actions.

* Front-end: (safety-critical part) is a redundant PLC system. It runs
autonomously and takes automated protective hardware actions based on a
predefined alarm-action matrix
* Back-end: supervises the front-end and serves as an interface to the PLC

SLIMOS check to be logged into DSS as `slimos` and two LEDs next to `Alive` are alternating (if not restart app or reboot the PC).

### User interface
The log at the bottom of the panel shows all DSS events in chronological order. It can help you understand the sequence of alarms that were triggered

DSS has a dedicated set of sensors connected to the DSS I/O modules. The inputs can be general or specific to a subdetector.
There are three types of inputs:
* Digital inputs (prefix “DI”) are dry contacts that are normally closed
(state “False”). Examples include signals from cooling plant PLCs or
from the smoke detection system.
* 4 – 20 mA or 0 – 10 V analogue inputs (prefix “AI”).
* PT100 temperature probes (prefix “PT”).

Inputs disappear automatically once the sensor has returned to its nominal status. Sensors with an “abnormal state” appear in the upper table on the DSS user interface. Alarms need to be acknowledged. They can only be reset (“removed”) once the corresponding inputs are no longer active. They start with the prefix “AL_” and are colour-coded in red.
* “!!!” and flashing text indicate that the alarm has not yet been acknowledged.
* The “x” indicates that the alarm has been acknowledged.
* `Left-click` to acknowledge
* `Right-click` to show info and instructions and actions

Actions are usually “brute force”, but can be delayed with respect to the appearance of an alarm to give time for a "soft landing”. Resetting actions should be coordinated with the DSS piquet, Run chief and subsystem piquets.
:::info
A frequent action is an automated call to the LHCb DSS piquet (16 80 00) and hard-wired signal to CCC TI. This action (`CCC_Alarm_signal_sent`) can be reset without consulting piquets or Run Chief.
:::

### Handling Alarms - Istructions
DSS alarms are associated with an audible alarm (siren) and a strobe light on the emergency panel.
1. Stop the siren with the green button “Stop buzzer” on the emergency panel or by clicking “Stop siren” on the DSS user interface.
2. Identify the cause on DSS user interface, give precedence to `Level-3 alarms`.
3. Acknowledge the alarm clicking on it
4. If the action `CCC_Alarm_signal_sent` was triggered, call CCC TI (7 22 01) to confirm that you are aware and taking care of the alarm.
5. Right-click to show details into

## Level-3 Alarms
## SNIFFER
## Access
## Technical Infrastructure




# Module 2b: Run Control & BigBrother

# F.A.Q.

* Before my first shift, I have to arrange the following formalities: Underground LHCB_U access and possession of a personal dosimeter is not required, but encouraged for shift leaders.
* If I find a problem in some of the distributions, what do I do? I create an issue from Monet through the ELOG button and call the subdetector piquet.
* As data manager or shift leader, I can briefly leave my desk, provided that I tell the other shifter where and how to reach me.
* Where is the LHCb detector located? In UX85-B
* During my data manager or shift leader shift, I write any relevant comment in the electronic logbook, because the timestamp can be relevant
* What do I do when I am unavailable to do my assigned shift? I find a replacement myself, for example by sending a mail to all trained shifters,
* I would like to inspect a histogram in more detail, so I can double-click on the histogram in Monet, and ROOT will display the histogram, I can use the icon in Monet to select a region and I can browse through the expert folders per subdetector to find more information
* If I see a feature in a distribution that I don¿t understand, during Stable Beams, then I compare to the reference histogram, and check if the feature is described in the information below. If the feature is new, I call the subdetector piquet.
* If a histogram in the Prompt DQM folder is absent, it is probably because the data has not yet been processed offline
* During physics data taking, I check the plots in the "Shift" folder continuously.

