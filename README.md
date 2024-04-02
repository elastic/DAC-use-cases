# DAC-use-cases
Use cases for end to end implementations of detection-as-code (DAC)

### Core Components of DaC within Elastic

* CC1: Maintaining rules within a Version Control System (VCS)
* CC2: Syncing rules from VCS to Elastic Security
* CC3: Managing rules within Elastic Security (consistent with a DaC approach)
* CC4: Syncing rules from Elastic Security to VCS


### Governance Models Dictating the Core Components of DaC

* GM1: VCS as authoritative
* GM2: Elastic security as authoritative
* GM3: Dual sync between VCS and Elastic Security (optional) 

## Use cases

| use case | governance model | CC1 | CC2 | CC3 | CC4 | notes | 
|----------|------------------|-----|-----|-----|-----|-------|
| [infosec](https://github.com/elastic/DAC-use-cases/tree/use-case-infosec)  | GM1 ||||||
| [fork DR](https://github.com/elastic/DAC-use-cases/tree/use-case-fork-dr)  | GM1 |||||||
| [import DR](https://github.com/elastic/DAC-use-cases/tree/use-case-import-dr) | GM3 |||||||
| [platform centric MSSP](https://github.com/elastic/DAC-use-cases/tree/use-case-gm2-mssp) | GM2 |||||||
