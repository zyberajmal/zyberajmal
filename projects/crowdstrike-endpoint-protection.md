# CrowdStrike Endpoint Protection

## Project Overview

This project focused on strengthening enterprise endpoint security by moving from a traditional signature-based antivirus approach to CrowdStrike Falcon.

The objective was not only to replace an endpoint security product. The broader goal was to improve behavioral threat detection, endpoint visibility, investigation capability and the operational response to suspicious activity.

This case study is intentionally generalized for public presentation. Employer details, endpoint counts, tenant information, internal architecture and sensitive detection logic are excluded.

## Business Context

The existing antivirus approach provided basic malware protection, but modern threats increasingly rely on techniques that may not be identified through signatures alone.

The environment needed stronger visibility into endpoint behavior and a better way to identify suspicious activity such as malicious scripting, credential-related activity, privilege misuse and lateral movement.

A modern endpoint detection and response platform also needed to support security operations after deployment. This meant the implementation had to consider policy management, telemetry, alert review, investigation and continuous tuning.

## Problem or Requirement

The main requirements were to:

- Improve endpoint protection beyond traditional signature-based detection
- Gain better visibility into endpoint activity and suspicious behavior
- Support investigation through richer endpoint telemetry
- Apply security policies consistently across managed endpoints
- Validate that protection policies worked as intended before broader adoption
- Establish practical operational processes for alert triage and investigation

## Research and Evaluation

CrowdStrike Falcon was selected following product evaluation and proof-of-concept activities.

The evaluation considered more than malware blocking. It also looked at behavioral detection, endpoint telemetry, investigation capability, policy flexibility and how effectively the platform could support day-to-day security operations.

This stage reinforced an important principle in my engineering approach. A security platform should be evaluated for how well it can be operated after implementation, not only for the features listed during procurement.

## Design Approach

The implementation was approached as a security capability rather than a simple software replacement.

The design focused on several connected areas:

1. Endpoint protection policies
2. Behavioral detection and prevention
3. EDR telemetry and visibility
4. Alert triage and investigation workflows
5. Controlled device access where additional restrictions were required
6. Validation and policy tuning before wider use

The goal was to strengthen protection while keeping policies practical for normal business operations.

## Implementation

My contribution included supporting the enterprise endpoint deployment and working across policy configuration, validation and ongoing operational improvement.

Key areas of involvement included:

- Assisting with the migration to CrowdStrike Falcon
- Configuring and tuning behavioral protection policies
- Working with EDR telemetry and security dashboards
- Validating endpoint security policies before wider application
- Testing detections to confirm expected visibility and alert behavior
- Supporting alert triage and threat investigations
- Implementing just-in-time USB blocking where removable media controls were required
- Reviewing operational behavior and refining controls where appropriate

The implementation was treated as an iterative process. Policies were reviewed against both security requirements and normal endpoint behavior so that controls could be strengthened without creating unnecessary operational disruption.

## Security Improvements

The move to CrowdStrike introduced stronger behavioral visibility across endpoint activity.

The platform provided improved insight into threat patterns that traditional antivirus could struggle to identify effectively, including:

- Suspicious PowerShell activity
- Privilege abuse
- Credential-related activity
- Lateral movement indicators
- Malicious or unusual process behavior

This improved the ability to investigate activity in context rather than relying only on isolated malware detections.

## Validation

Validation was an important part of the implementation.

The work included checking that policies were applied correctly, confirming expected detection behavior and reviewing the resulting telemetry and alerts.

Detection testing helped verify that the platform was producing useful security visibility. Alert review and investigation also helped identify where policies or operational processes could be improved.

This approach allowed the implementation to move beyond deployment status and focus on whether the security control was actually working as intended.

## Operational Security

Once the platform was deployed, the focus continued through operational use.

CrowdStrike became part of the wider security workflow through:

- Alert review and triage
- Endpoint investigation
- Behavioral analysis
- Policy tuning
- Detection validation
- Device control use cases
- Ongoing review of endpoint security posture

This operational phase was important because endpoint security effectiveness depends on continued review and improvement rather than a one-time deployment.

## Business and Operational Value

The project improved the endpoint security model by introducing real-time behavioral detection and richer endpoint visibility.

From an operational perspective, the platform provided better information for understanding suspicious activity and supported a more structured investigation process.

The main value came from strengthening several areas together:

- Better behavioral threat detection
- Improved endpoint visibility
- Stronger investigation capability
- More consistent endpoint security policies
- Greater control over removable media use cases
- A clearer operational process for reviewing and responding to endpoint alerts

No confidential performance figures or internal security metrics are included in this public version.

## My Contribution

My role focused on practical implementation and operational security rather than product ownership alone.

I contributed to:

- Endpoint deployment support
- Security policy configuration and tuning
- EDR telemetry and dashboard use
- Detection testing and validation
- Alert triage
- Threat investigation
- USB control implementation
- Continuous operational improvement

This work combined infrastructure knowledge with security engineering and helped strengthen my approach to endpoint protection as part of the wider enterprise environment.

## Documentation and Knowledge Transfer

A sustainable security implementation requires clear operational knowledge.

The project reinforced the value of documenting areas such as:

- Implementation decisions
- Policy behavior
- Validation results
- Operational procedures
- Investigation workflows
- Troubleshooting knowledge
- Lessons identified during deployment and tuning

Documentation helps preserve the reasoning behind security decisions and makes the environment easier to support and improve over time.

## Lessons Learned

### Security tools need operational ownership

Deploying an endpoint security platform is only the beginning. Detection quality, policy effectiveness and investigation processes need continued review.

### Validation matters as much as configuration

A policy being enabled does not automatically prove that it works as expected. Detection testing and telemetry review provide the evidence needed to validate the control.

### Security and usability must be balanced

Endpoint controls can affect legitimate business activity. Policy tuning should strengthen security while considering how users and systems actually operate.

### Visibility changes how incidents are investigated

Richer endpoint telemetry makes it possible to understand suspicious behavior in context and supports better security decisions.

### Documentation creates long-term value

Capturing configuration decisions, operational procedures and lessons learned makes future support and continuous improvement more effective.

## Technologies and Areas

- CrowdStrike Falcon
- Endpoint Detection and Response
- Behavioral Threat Detection
- Endpoint Security Policy
- Security Monitoring
- Alert Triage
- Threat Investigation
- Device Control
- Endpoint Hardening

---

[Project Portfolio](README.md) · [Enterprise Capabilities](../career/capabilities.md) · [Engineering Approach](../methodology/engineering-approach.md) · [Knowledge & Lab](../learning/README.md) · [Back to profile](../README.md)
