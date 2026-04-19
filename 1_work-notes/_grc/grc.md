---
title:  "GRC Overview"
intro: "A brief overview of Governance, Risk, and Compliance"
description: "A brief overview of Governance, Risk, and Compliance"
tags: "grc, governance, risk, compliance"
date: "2026-04-16"
---

### GRC

In Cybersecurity, GRC sets how the organization conducts itself via policy, tests its compliance against the policy, and manages risk.

#### Governance
Sets how the organization must conduct itself.

- Informed from both internal and external sources, for example:
    - Regulatory requirements (HIPAA, PCI, etc.)
    - Business purpose (mission statement, vision, etc.)
    - Industry best practices (OWASP, etc.)
    - Certifications (ISO-27001, SOC2, etc.)
- Typically results in a set of Policies the organization must follow

#### Risk
Although Risk is a discipline in itself with a lot of work inside it, an easy way to think of it (at a very high-level), is the delta (gap) between Governance and Compliance.

#### Compliance
Sets requirements and controls that conform to the Policies, tests how well the organization follows them.

### So what's it mean?

As an example, if policy dictates that Vulnerability scanning must occur at regular intervals:

Compliance may set Controls and Tests to validate that systems have vulnerability scanning tools:
> Control: Vulnerability scanning tool installed on all systems
>
> Test: For each system check that approved vulnerability scanning tool is installed and enabled
> 
> Control: Vulnerability scanning occurs at regular intervals
> 
> Test: For each system check that approved vulnerability scanning tool is configured to run every 24-hours.

You might notice that Control and Test say the same things in different ways, the difference is that the Test evaluates if the Control is met. 

If a Test fails the existence of a Risk is implied but must be evaluated against the organization's Risk practice.

*Note:* Tests may require a procedure to be created and run manually but I try to ensure that Tests are automatable whenever possible.