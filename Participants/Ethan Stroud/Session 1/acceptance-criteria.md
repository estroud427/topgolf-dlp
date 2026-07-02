# Acceptance Criteria: Automated Ad Hoc Work Intake for Platform Engineering

> Derived directly from `user-story.md`. Every criterion traces to the business need expressed in a user story — nothing is imposed beyond what the stories describe. Each item uses **Given / When / Then** so it is clear, testable, and human-consumable.

---

## Story 1 — Automated Intake (Director)

*Business need: ad hoc work requests from other teams are added as stories in JIRA automatically.*

**AC 1.1** — Given a work request is submitted through the intake flow, When it is processed, Then it results in a Story in the Platform Engineering JIRA project without the PE team manually re-entering it.

**AC 1.2** — Given a request moves through intake, When it is completed, Then the path from submission to JIRA Story creation happens automatically.

---

## Story 2 — Slack-Based Request Submission (Requestor)

*Business need: send a specific `/` command in Slack and know it creates a trackable ticket in the PE JIRA project.*

**AC 2.1** — Given a member of the Slack workspace, When they use the `/pe-request` command, Then the intake flow starts.

**AC 2.2** — Given a completed request, When it is submitted, Then a Story is created in the PE JIRA project.

**AC 2.3** — Given the Story is created, When the requestor is responded to, Then they receive confirmation that a trackable ticket now exists.

---

## Story 3 — Guided Context Gathering via AI Interview (Requestor)

*Business need: the requestor is interviewed to gain context, deadlines, and specific information about the ask.*

**AC 3.1** — Given the interview starts, When the requestor is asked questions, Then it gathers the context, deadline, and specific information the ask requires.

**AC 3.2** — Given the requestor's answers, When they lack enough context for the ask, Then the interview asks follow-up questions until the ask is sufficiently understood.

**AC 3.3** — Given a specific request, When the interview runs, Then its questions are driven by that request (AI-driven) rather than a fixed static form.

**AC 3.4** — Given the interview is complete, When the Story is created, Then the information gathered is captured on the ticket.

---

## Story 4 — Clean Hand-off (Platform Engineer)

*Business need: a Platform Engineer is never involved with the ingestion of work until it is assigned to them.*

**AC 4.1** — Given a request being ingested, When it has not yet been assigned, Then no Platform Engineer is involved or notified.

**AC 4.2** — Given a Story, When it is assigned to a Platform Engineer, Then that engineer becomes involved only at that point.

---

## Story 5 — Confirmation & Traceability (Requestor)

*Business need: the requestor receives confirmation with the JIRA link and a summary of what was captured.*

**AC 5.1** — Given a Story is created, When the requestor is confirmed, Then the confirmation includes the JIRA link and a summary of what was captured.

**AC 5.2** — Given a created Story, When it is reviewed, Then it can be traced back to the requestor who submitted it.

---

## Story 6 — Status Visibility (Requestor)

*Business need: the requestor is notified on all major status changes.*

**AC 6.1** — Given a Story the requestor submitted, When its status changes to any of Created, Assigned, In Progress, Blocked, Done, or Closed/Won't Do, Then the requestor is notified in Slack.

**AC 6.2** — Given a status-change notification, When the requestor reads it, Then it conveys which ticket changed and its new status.

---

## Story 7 — Triage & Assignment (Director)

*Business need: the Director triages requests and assigns them, confirming or overriding the requestor's suggested priority and deadline.*

**AC 7.1** — Given a new Story, When the Director triages it, Then they can confirm or override the requestor-suggested priority and deadline.

**AC 7.2** — Given a triaged Story, When the Director assigns it, Then it is routed to a specific Platform Engineer.

---

## Story 8 — Duplicate Prevention (Requestor)

*Business need: if the request is a duplicate, intake stops and informs the requestor that a similar ticket already exists.*

**AC 8.1** — Given a request being submitted, When intake runs the duplicate check, Then it evaluates whether a similar ticket already exists before any Story is created.

**AC 8.2** — Given a similar ticket already exists, When the duplicate check matches, Then intake stops, no new Story is created, and the requestor is informed that a similar ticket has already been created.

**AC 8.3** — Given no similar ticket exists, When the duplicate check runs, Then the request proceeds and a Story is created.

---

## Notes on Scope

- **Escalation** of untriaged work is out of scope — it is handled by a separate, existing process.
- **JIRA statuses** are limited to the standard set used above; there are no custom statuses.
- **How duplicates are matched** (e.g., which ticket attributes signal similarity) is a design detail to be arrived at during design — not a dictated requirement. The business-level requirement is only that a similar existing ticket stops intake and informs the requestor (Story 8).
- **How gathered information is stored on the ticket** (field placement) is likewise a design detail; the business-level requirement is that the gathered information is captured on the ticket (AC 3.4).
