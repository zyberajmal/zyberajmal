# Datadog Security Detection Engineering

## Project Overview

This initiative focused on reviewing and strengthening security detection coverage in Datadog for Windows and Active Directory environments.

The work was not limited to creating individual alerts. The broader objective was to understand the existing detection inventory, identify important coverage gaps, prioritize security use cases, define how detections should be validated and document a repeatable approach for continuous improvement.

The initiative connected Windows event logging, Active Directory security, authentication monitoring, privilege changes, endpoint activity and security operations into a structured detection-engineering process.

This case study is intentionally generalized for public presentation. Internal detection queries, log sources, tenant details, user information, hostnames, alert data and organization-specific configurations are excluded.

## Business Context

Security monitoring becomes less effective when detections grow over time without a clear view of what they actually cover.

The environment already contained a number of Windows-focused security rules in Datadog. These provided useful coverage across authentication, credential activity, malware behavior, local administrative changes and firewall tampering.

However, a rule inventory alone does not prove that the most important risks are covered.

The review therefore focused on a more practical question:

> If a security-relevant action occurs in Windows or Active Directory, will the environment generate the right event, ingest it correctly and produce an alert at an appropriate priority?

This shifted the review from counting rules to evaluating security outcomes.

## Existing Detection Coverage

The existing Datadog rule set included detections such as:

- Excessive distributed authentication failures by source IP
- Excessive Kerberos requests from a user
- Browser credential harvesting attempts
- Windows administrative account lockouts
- Fileless execution activity
- Authentication failures involving highly privileged accounts
- Persistence through addition of a user to the local Administrators group
- Windows Firewall tampering

These rules provided a useful starting point across several security objectives.

At the same time, the review showed that additional visibility was required around Active Directory changes, privileged group membership, organizational units, Group Policy and other administrative activity that can affect security without looking like malware.

## Problem or Requirement

The main requirements included:

- Review existing Windows and Active Directory detections
- Group detections by security objective
- Identify important monitoring gaps
- Prioritize critical identity and privilege changes
- Improve coverage for Active Directory administration
- Review authentication detections
- Define additional Windows security use cases
- Distinguish high-priority alerts from lower-risk administrative events
- Develop a practical validation approach
- Reduce the risk of untested detections
- Consider false positives and operational usability
- Document detection purpose, expected behavior and validation steps
- Create a repeatable process for continuous tuning

## Detection Engineering Approach

The work followed a structured lifecycle:

> **Inventory → Map → Identify Gaps → Prioritize → Design → Validate → Tune → Document → Revisit**

Each stage answered a different question.

### Inventory

What detections already exist?

The first step was to understand the current rule set instead of assuming that important use cases were either present or missing.

### Map

What security objective does each rule support?

Rules were considered in categories such as authentication, credential access, persistence, privilege changes, malware behavior, endpoint control tampering and directory administration.

### Identify Gaps

Which important security events are not sufficiently visible?

This stage focused especially on Active Directory users, groups, computers, organizational units and Group Policy.

### Prioritize

Which events deserve immediate analyst attention?

Not every administrative action should generate the same alert severity.

### Design

What event or behavior should the detection identify?

The logic should reflect the security objective rather than simply matching a log field because it is available.

### Validate

Does the full detection path actually work?

A rule is only useful if the source event is generated, collected, parsed and matched correctly.

### Tune

Does the alert provide useful signal without excessive noise?

Operational experience should be used to improve the rule.

### Document

Why does the detection exist and how should it be tested?

This knowledge needs to remain available after the original implementation.

### Revisit

Does the detection still make sense as the environment changes?

Detection engineering is a continuous process.

## Active Directory Detection Gaps

The review identified Active Directory administration as an area where stronger security use cases were needed.

### User Account Activity

Important monitoring areas included:

- User account creation
- User account deletion
- User account enable and disable activity
- Administrative password-related changes
- Account lockouts
- Important user attribute changes
- Suspicious activity involving privileged accounts

These events support both identity governance and incident investigation.

### Group Changes

Group activity was considered especially important because membership changes can immediately alter privilege.

Required coverage included:

- Security group creation
- Security group deletion
- Group membership changes
- Users added to privileged groups
- Users removed from privileged groups
- Changes involving highly privileged domain groups
- Local Administrators membership changes

Privileged group additions were considered higher priority than routine group administration because they can create immediate elevated access.

### Computer Account Activity

Monitoring requirements also included:

- Computer account creation
- Computer account deletion
- Important computer object changes
- Unusual computer account activity

This provides better visibility into changes affecting devices participating in the domain.

### Organizational Unit Changes

The review included use cases for:

- OU creation
- OU deletion
- OU modification
- Movement of important objects between OUs

OU activity can affect delegation and policy application, so it should not be treated as purely administrative noise.

### Group Policy Changes

Group Policy was considered a critical monitoring area because one change can affect many systems.

The required use cases included:

- GPO creation
- GPO deletion
- GPO modification
- Security-related policy changes
- Unexpected policy changes involving privileged users

These events were considered important for both security monitoring and change accountability.

## Authentication Detection Review

Authentication detections were already an important part of the existing rule set.

The review considered coverage for scenarios such as:

- Repeated authentication failures
- Distributed authentication failures
- Privileged account authentication failures
- Administrative account lockouts
- Unusual Kerberos request patterns
- Suspicious authentication behavior

The key improvement was to consider authentication events together with identity and privilege changes.

For example, repeated failures involving a recently modified privileged account may deserve more attention than the same failure pattern involving a normal account with no related security changes.

This demonstrates the value of context when prioritizing detections.

## Privilege and Persistence Use Cases

Privilege escalation and persistence were treated as high-priority security objectives.

Existing coverage already included detection of a user being added to the local Administrators group.

The broader review expanded the concept to include:

- Domain privileged-group changes
- Local administrator changes
- New or modified privileged accounts
- Suspicious administrative activity
- Security-control changes that could support persistence

These detections help identify situations where an attacker or unauthorized administrator attempts to retain elevated access.

## Security Control Tampering

Windows Firewall tampering was already represented in the existing detection inventory.

The review treated security-control modification as an important category because attackers may attempt to weaken protections before performing other actions.

Related areas for detection review included:

- Firewall changes
- Endpoint protection changes
- Logging changes
- Other administrative activity that could reduce security visibility or protection

The purpose was to detect attempts to weaken controls, not only the malicious activity that may follow.

## Detection Prioritization

A useful detection program needs a clear way to distinguish critical events from routine administration.

The prioritization approach considered factors such as:

- Privilege level affected
- Potential security impact
- Whether the action changes access
- Whether the action affects many systems
- Whether the activity could support persistence
- Whether the action weakens a security control
- Whether the event is expected during normal operations
- Whether additional contextual information is available

Examples of higher-priority use cases included:

- Addition of a user to a highly privileged group
- Suspicious privileged authentication failures
- Group Policy changes affecting security settings
- Local administrator membership changes
- Credential harvesting behavior
- Fileless execution
- Security-control tampering

Lower-risk administrative activity could still be logged and retained for investigation without generating the same alert urgency.

## Validation Methodology

A major part of the initiative was defining how important detections should be tested.

The validation model followed four stages:

> **Action → Windows Event → Log Ingestion → Datadog Detection**

### Action

Perform a controlled administrative or security-relevant activity.

### Windows Event

Confirm that Windows generated the expected event.

### Log Ingestion

Confirm that the event reached the monitoring platform with the fields needed for detection.

### Datadog Detection

Confirm that the rule matched the event and produced the expected security signal.

This approach made troubleshooting easier because a failed detection could be traced to the correct layer instead of assuming the query itself was the problem.

## Manual Validation

The preferred validation approach for important Windows and Active Directory use cases was controlled manual testing using standard administrative interfaces.

This was intentionally chosen over unnecessary scripting where manual actions were safer and easier to understand.

Representative test scenarios included:

- Creating and removing a controlled test account
- Enabling or disabling a test account
- Adding and removing a test user from an approved group
- Testing a controlled local Administrators membership change
- Generating approved authentication failures
- Performing safe directory or policy changes in an appropriate test context

The purpose was to validate visibility and detection, not to create risky changes in production.

Any testing involving privileged groups, Group Policy or sensitive systems should be performed only with appropriate approval and in a controlled environment.

## False Positives and Tuning

A technically correct rule can still be operationally poor if it generates excessive noise.

The review therefore considered false-positive management as part of detection engineering.

Tuning questions included:

- Is the activity expected for specific administrative accounts?
- Is the alert triggered frequently during approved operational work?
- Can known administrative activity be distinguished from unusual behavior?
- Is the rule priority appropriate for the actual risk?
- Does the alert contain enough context for investigation?
- Would suppression or exception logic improve signal quality without hiding real risk?

The goal was not to eliminate every alert. The goal was to improve the ratio of useful signals to routine administrative noise.

## Detection Documentation

Documentation was treated as part of each use case.

A mature detection record should explain:

- Detection name
- Security objective
- Why the use case matters
- Relevant Windows or Active Directory activity
- Expected log source
- Alert priority
- Known legitimate scenarios
- Validation method
- Investigation considerations
- Tuning notes
- Ownership
- Review history

This makes the rule easier to maintain and helps other analysts understand why it exists.

## Continuous Improvement

Detection engineering does not end when a rule is enabled.

The review emphasized a continuous cycle of:

- Monitoring alert quality
- Reviewing false positives
- Investigating missed use cases
- Adding new detections when risks change
- Updating priorities
- Retesting important rules
- Reviewing changes in Windows or Active Directory
- Improving documentation

Operational feedback is essential because real alerts reveal whether a rule provides enough context and whether its severity matches the actual risk.

## Business and Operational Value

The initiative created a more structured approach to security monitoring in Datadog.

The main value included:

- Clearer understanding of existing detection coverage
- Better visibility into Active Directory monitoring gaps
- Stronger focus on privileged changes
- Better prioritization of high-risk Windows events
- A repeatable validation methodology
- Improved distinction between detection presence and detection effectiveness
- Better consideration of false positives and alert quality
- Stronger documentation for future review
- Better alignment between Windows administration and security operations
- A foundation for continuous detection improvement

No confidential queries, alert volumes, internal event data, tenant details or organization-specific thresholds are included in this public version.

## My Contribution

My role focused on reviewing the existing Windows security use cases and developing a more complete detection-engineering approach.

I contributed to:

- Reviewing the current Datadog detection inventory
- Grouping rules by security objective
- Identifying missing Windows and Active Directory use cases
- Prioritizing critical identity and privilege changes
- Reviewing authentication-related detections
- Defining monitoring requirements for users, groups, computers, OUs and GPOs
- Developing a structured validation methodology
- Designing controlled manual testing scenarios
- Considering alert severity and operational priority
- Reviewing false-positive and tuning requirements
- Documenting detection gaps and recommendations
- Supporting continuous improvement of the security monitoring model

This work reflects how I approach security monitoring. A detection should have a clear purpose, reliable event source, appropriate priority, practical validation method and enough documentation to remain useful over time.

## Lessons Learned

### A large rule count does not prove strong coverage

Detection quality should be measured against security objectives and important attack or administrative actions rather than the number of alerts configured.

### Active Directory changes deserve dedicated detection coverage

Important identity and privilege changes may not look like malware, but they can have significant security impact.

### Privilege changes should be easy to investigate

Events involving privileged groups and administrative access require higher visibility because they can immediately change what a user can do.

### Validation must test the complete pipeline

The detection query is only one part of the system. Event generation, audit policy, ingestion and parsing all affect whether an alert works.

### False-positive tuning is part of engineering

A noisy rule may be ignored even if it technically works. Operational usability matters.

### Manual testing can provide strong validation

Controlled manual actions can be an effective and low-complexity way to test many Windows and Active Directory detections.

### Documentation gives detections a lifecycle

Rules are easier to validate, tune and hand over when their purpose, expected behavior and testing process are documented.

### Detection engineering is continuous

New systems, administrative patterns and threats change what useful monitoring looks like. Detection coverage should be revisited regularly.

## Technologies and Areas

- Datadog Security Monitoring
- Detection Engineering
- Microsoft Windows
- Active Directory
- Windows Security Events
- Authentication Monitoring
- Privileged Access Monitoring
- Group Policy Monitoring
- Identity Change Monitoring
- Credential Access Detection
- Persistence Detection
- Security Control Tampering
- Alert Prioritization
- Detection Validation
- False-Positive Tuning
- Security Use Case Documentation

---

[Back to project portfolio](README.md) | [Back to profile](../README.md)
