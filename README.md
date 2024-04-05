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
| [infosec](https://github.com/elastic/DAC-use-cases/tree/use-case-infosec) | GM1 | <ul><li>no DR repo usage</li><li>use of custom rules</li><li>create detection rules in kibana and export</li><li>versioning?</li><li>custom exceptions and actions management</li><li>custom unit tests</li><li>limited rule schema validation</li><li>no detection logic validation</li></ul> | <ul><li>deploy via CI/CD and custom REST calls</li></ul> | <ul><li>manual management and tines</li></ul> | <ul><li>tines to push based on X trigger? (or schedule?)</li></ul> | need to verify; grimoire |
| [fork DR](https://github.com/elastic/DAC-use-cases/tree/use-case-fork-dr) | GM1 | <ul><li>DR repo usage</li><li>use of custom rules</li><li>create detection rules in kibana and export</li><li>versioning using lock files</li><li>custom exceptions and actions management</li><li>custom unit tests</li><li>rule schema validation</li><li>detection logic validation</li></ul> | <ul><li>use of detection-rules repo features for syncing</li></ul>  | <ul><li>syncing handled via VCS with limited direct management in Elastic Security</li></ul> | <ul><li>not applicable or minimal use</li></ul> | Leveraging detection-rules repo for rule maintenance |
| [import DR](https://github.com/elastic/DAC-use-cases/tree/use-case-import-dr) | GM3 | <ul><li>import rules via detection-rules libraries</li></ul> | <ul><li>automated syncing to Elastic Security</li></ul> | <ul><li>manual rule management within Elastic Security</li></ul> | <ul><li>syncing back to VCS as part of dual sync process</li></ul> | Import libraries to assist dual sync |
| [platform centric MSSP](https://github.com/elastic/DAC-use-cases/tree/use-case-gm2-mssp) | GM2 | <ul><li>secondary role of VCS</li></ul>  | <ul><li>infrequent or batched syncing to Elastic Security</li></ul> | <ul><li>primary rule management within Elastic Security</li></ul> | <ul><li>infrequent syncing back to VCS, if at all</li></ul> | Elastic-centric rule management for multiple clients |


## Reference Automation Workflows in DaC

In practice, the Detection as Code (DaC) approach within Elastic Security leverages a series of GitHub Actions workflows to automate various synchronization tasks. These workflows facilitate the continuous integration and deployment of detection rules, ensuring that they are consistently aligned with the latest developments and threat intelligence. The following workflows can be found in the .github/workflows directory:

- [Push to Production Sync](.github/.DS_Store/push_to_production_sync.yml): Automates the process of pushing verified rules from the Version Control System to the Elastic Security environment upon changes being merged into the main branch.
- [Manual Dispatch Sync Workflow](.github/.DS_Store/manual_dispatch_sync.yml): Allows repository maintainers to manually trigger a rules synchronization, providing control over when rules are updated in Elastic Security.
- [Scheduled Sync Workflow](.github/.DS_Store/scheduled_sync.yml): Executes at predetermined intervals to check for and synchronize any updates from Elastic Security, ensuring the detection rules are current.
- [CI/CD Per-PR Sync Workflow](.github/.DS_Store/pr_sync.yml): Runs a series of checks on pull requests to validate rule changes before they are merged, ensuring that all updates meet the defined standards for detection rules.

These workflows are essential tools in managing the lifecycle of detection rules, contributing to a robust and responsive security posture.