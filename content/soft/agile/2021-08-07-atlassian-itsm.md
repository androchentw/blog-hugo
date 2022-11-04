---
title: "Atlassian - ITSM"
url: /atlassian-itsm
#date: 2021-08-06T01:20:28+08:00
date: 2021-08-07T10:55:28+08:00
author: androchentw
type: post
categories:
  - life
  - soft
tags: 
  - agile
share_img: https://i.imgur.com/NJKXgVc.png
series: agile
---

<img style="width:40%;" src="https://i.imgur.com/NJKXgVc.png">

## Overview

Continuing previous post: [Agile Life](https://blog.androchen.tw/2021-agile-life/), let's dive deeper into a series of ITSM methodologies and products proposed by [Atlassian](https://www.atlassian.com/itsm), with a view to applying them in work and life to further enhance productivity and narrative skills.

### Challenges

1. Profile: Data Engineer + Operations Administrator
2. Jobs
   1. Provisioning and troubleshooting data pipeline, visualization and monitoring
   2. Collaborate with other developers and administrators
3. Pains
   1. Repeated or similar questions
   2. Long communication time to do situation analysis
   3. Hard to find thorough SOP or agile workflow
   4. Hard to prioritize ad-hoc tasks
4. Gains
   1. Single source of truth
   2. Organized knowledge base, working documents
   3. Unified way to handle similar incidents

### Objectives

1. Build smart and modern IT Service Management and cultivate mindset with team

### KRs

1. [x] 2021-08 Learn from all [Atlassian ITSM topics](https://www.atlassian.com/itsm) and whitepapers
2. [x] 2021-08 Establish Knowledge-Centered Service for users

<!--more-->

## ITSM

* [What is IT Service Management (ITSM)?](https://www.atlassian.com/itsm)

> IT service management -- often referred to as ITSM -- is simply how IT teams **manage the end-to-end delivery of IT services to customers**. This includes all the processes and activities to design, create, deliver, and support IT services.
> The core concept of ITSM is the belief that IT should be delivered as a service.

<img style="width:40%;" src="https://wac-cdn.atlassian.com/dam/jcr:f313f3ad-dcae-43cd-83a3-feb8db0abaa0/IT%20teams.png?cdnVersion=1746">

### Core

1. Team First
   1. [team playbook](https://www.atlassian.com/team-playbook).
   2. Rather than answering to rules imposed by a tiered reporting structure or rigid process, IT teams can make informed decisions about things like adopting SLAs and which software to implement. Because **IT teams enable productivity and digital transformation**, strong IT teams are critical to strong organizations.
2. Then Practice
   1. Successful IT teams build their approach from frameworks like **ITIL (the Information Technology Infrastructure Library)**, but are careful to think about how to adapt processes that will resonate with their customers.
3. Finally Technology
   1. It empowers end-users and automates mundane work, so **everyone gets more time to focus on what matters most to them**.

### ITSM vs ITIL vs DevOps

<img style="width:80%;" src="https://valueinsights.ch/wp-content/uploads/2020/06/The-ITIL-4-Big-Picture_v1.0.png">

* [The ITIL 4 Big Picture](https://valueinsights.ch/the-itil-4-big-picture/)

* [淺談 ITIL 4 與服務管理實踐](https://www.gss.com.tw/blog/itil4)
  1. Four dimensions model
     1. Organizations & people
     2. Information & technology
     3. Partners & suppliers
     4. Value streams & processes
  2. SVS：Service Value System
     1. Opportunity / Demand => Value
     2. Guiding Principles
     3. Governance
     4. SVC: Service Value Chain
     5. Practices
     6. Continual Improvement
  3. SVC: Service Value Chain
     1. [Value Stream](https://www.scaledagileframework.com/value-streams/)
     2. [9 Essential Value Stream Mapping Templates to Immediately Discover Flows in Your Processes](https://creately.com/blog/examples/value-stream-mapping-templates/)

<img style="width:80%;" src="https://www.scaledagileframework.com/wp-content/uploads/2020/03/Value-Streams_F03_WEB-new.png">

* DevOps promised benefits include
  1. Increased trust
  2. Faster software releases
  3. An ability to solve critical issues quickly
  4. Better management of unplanned work.

* DevOps is much more than just automated development, and promotes the importance of collaboration and a blame-free culture.

* The importance of ITSM (Common benefits)
  * Aligning IT teams with business priorities tracked through success metrics.
  * Improving request coordination for more efficient service.
  * Promoting customer-centricity with self-service and better processes.
  * Responding more quickly to major incidents, and preventing future ones.

* ITSM Processes / Practices
  1. [Service request management](#service-request-management) is a **repeatable procedure** for handling the wide variety of customer service requests.
  2. [Knowledge management](#knowledge-management) is the process of creating, sharing, using, and **managing the knowledge** and information of an organization.
  3. IT asset management (also known as ITAM) is the process of ensuring an organization’s **assets are accounted for**, deployed, maintained, upgraded, and disposed of when the time comes.
  4. [Incident management](#incident-management) is the process to **respond to an unplanned event** or service interruption and restore the service to its operational state.
  5. [Problem management](#problem-management) is the process of **identifying and managing the causes** of incidents on an IT service.
  6. [Change management](#change-management) ensures **standard procedures are used for efficient and prompt handling of all changes** to IT infrastructure.

## Service Request Management

<img style="width:40%;" src="https://wac-cdn.atlassian.com/dam/jcr:cb4f6608-7a1f-44ce-b4bf-1afef2e614d5/service%20request%20priorities.png?cdnVersion=1746" title="Atlassian - Service Request Managament Priorities">
<br />
<img style="width:40%;" src="https://wac-cdn.atlassian.com/dam/jcr:b494279c-f2f0-42c6-b665-2bdbf435cba0/service-request-flow%20.png?cdnVersion=1746" title="Atlassian - service request fulfillment process">

* [What is a service request?](https://www.atlassian.com/itsm/service-request-management)
* [IT Metrics: 4 best practices for success](https://www.atlassian.com/itsm/service-request-management/it-metrics-and-reporting)
* [How to run IT support the DevOps way](https://www.atlassian.com/itsm/service-request-management/how-to-run-it-support-devops-way)

* smart support workflow
  * [Are your support services as SMART as they could be?](https://blogs.servicenow.com/2019/smart-support-services.html)
  * [Create a Help Desk Workflow Streamline Your Support Process](https://www.happyfox.com/help-desk-work-flow/)
* [Opsgenie](https://www.atlassian.com/software/opsgenie)

## Knowledge Management

<img style="width:40%;" src="https://wac-cdn.atlassian.com/dam/jcr:942dab82-b26c-440b-bd58-f0dfb3355168/Knowledge%20management%20cycle.png?cdnVersion=1738" title="Atlassian - Knowledge Management">
<br />
<img style="width:40%;" src="https://wac-cdn.atlassian.com/dam/jcr:39e1e686-ab57-42d3-ada9-cfeb117607d9/Knowledge%20base%20ways.png?cdnVersion=1735" title="Atlassian - KM Benefit">

* [Best Practices](https://www.atlassian.com/itsm/knowledge-management)
  1. Aggregate your team’s knowledge in a single repository or system.
  2. Increase **transparency** with open and shared information.
  3. **Make work visible** with a [project poster](https://www.atlassian.com/team-playbook/plays/project-poster).
  4. Focus on **brief** articles or answers.

* [Benefits of a knowledge base](https://www.atlassian.com/itsm/knowledge-management/what-is-a-knowledge-base)
  1. More consistent service.
  2. Higher resolution rates at first contact.
  3. Lower training costs.

### KCS - Knowledge-Centered Service

<img style="width:80%;" src="https://raw.githubusercontent.com/androchentw/diagrams-res/main/2021-08-07%20KCS%20UML.svg" title="KCS Flowchart">

* [What is knowledge-centered service (KCS)?](https://www.atlassian.com/itsm/knowledge-management/kcs)
* Benefits
  1. Numbers
     1. 30 – 50% increase in first-contact resolution
     2. 70% faster time-to-proficiency for new analysts  
     3. 20 – 40% improvement in employee satisfaction
     4. 10% fewer reported issues/support requests
     5. 50 – 60% of KCS adopters also improved time to resolution
  2. Less problem-solving from scratch frees up time
  3. More consistent customer experiences mean happier stakeholders
  4. KCS creates continuous improvement
  5. Good documentation enables true self-service
* Challenges
  1. Teams often experience cultural challenges that make it hard to shift out of [what expert David Kay calls](https://www.dbkay.com/culture/what-does-a-bad-knowledge-sharing-culture-look-like-2) “an obsession with the urgent and tactical.”
  2. IT managers get too busy fighting fires using current processes (ineffective as they may be) to focus on doing something more strategic.
* How does KCS work?
  1. Capture knowledge
  2. Structure knowledge
  3. Reuse knowledge
  4. Improve knowledge
  5. Use knowledge to see the big picture
* [KCS v6](https://www.serviceinnovation.org/faq-about-kcs/)

### Tips

* [Team Playbook](https://www.atlassian.com/team-playbook)
  * [Elevator Pitch](https://blog.androchen.tw/elevator-pitch/)
  * [OKRs](https://www.atlassian.com/team-playbook/plays/okrs)
  * [Prioritize, as a team](https://www.atlassian.com/team-playbook/plays/prioritize-tasks-how-to)
  * [Roles and Responsibilities](https://www.atlassian.com/team-playbook/plays/roles-and-responsibilities)
  * [Retrospective](https://www.atlassian.com/team-playbook/plays/retrospective)
  * [Learning Circle](https://www.atlassian.com/team-playbook/plays/learning-circle)
* [5 tips](https://www.atlassian.com/blog/archives/5_tips_for_building_a_knowledge_base_with_confluence)

## Incident Management

* [What is incident management?](https://www.atlassian.com/itsm/incident-management)

## Problem Managment

* [What is problem management?](https://www.atlassian.com/itsm/problem-management)

## Change Management

* [The evolution of IT change management](https://www.atlassian.com/itsm/change-management)

## ITIL

* [A guide to ITIL and its place in modern ITSM](https://www.atlassian.com/itsm/itil)

## Murmur

* 2021-08-07 knowing is one thing, doing is another. Recently I just realize deeply how important these precise definition is, as I'm working on advocating these "well-known" knowledge and really implements these concepts into my work and team collaboration.
