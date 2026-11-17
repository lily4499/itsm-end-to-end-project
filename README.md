# ServiceNow ITSM | End-to-End Service Desk Operations

**Project type:** IT Service Management (ITSM) workflow validation  
**Platform:** ServiceNow (provisioned training instance)  
**Scope:** Service Catalog, Request Fulfillment, Incident Management, Problem Management, Change Management  

## Business Scenario

A mid-sized company needs a reliable IT service desk. Employees must be able to order hardware or software, report service disruptions, and track progress. IT specialists need to record incidents, investigate recurring failures, and perform authorized changes without disrupting business operations.

The project validates a complete ITSM lifecycle:

1. Confirm ITSM applications are available.
2. Submit employee service requests and process approvals.
3. Track requested items and fulfillment tasks.
4. Create, escalate, investigate, and resolve incidents.
5. Investigate recurring incidents through problem management.
6. Propose, assess, approve, implement, and close a controlled change.

**Example story:** A new hire requests a laptop. Later, a user experiences Wi-Fi failures; the service desk restores connectivity. When similar failures recur, the team opens a problem record, diagnoses a wireless configuration defect, and submits a change for approval before implementing the long-term fix.

## Tools and Skills

- **ServiceNow:** IT Service Management, Service Catalog, Employee Center (if installed), Incident, Problem, Change
- **Processes:** Ticket logging, routing, approvals, assignment, escalation, root cause analysis, risk assessment, controlled change, closure
- **Documentation:** Test evidence, work notes, record relationships, validation, audit trail
- **Records:** `REQ` (request), `RITM` (requested item), `SCTASK` (catalog task), `INC` (incident), `PRB` (problem), `CHG` (change), and change tasks (`CTASK`) where configured

## Easy ITSM Memory Trick

| Record or process | Plain-English meaning | Example |
|---|---|---|
| Service request | **I need something** | New employee requests a laptop |
| Incident | **Something is broken** | Employee cannot connect to Wi-Fi |
| Problem | **Why does it keep breaking?** | Multiple users experience Wi-Fi disconnections |
| Change | **Fix it safely and with approval** | Correct an access point configuration |

**Record number cheat sheet:** `REQ = full order`, `RITM = one item in order`, `SCTASK = fulfillment task`, `INC = incident`, `PRB = problem`, `CHG = change request`. Record numbers are assigned by your instance; never invent them.

## ServiceNow Navigation Quick Guide

The exact menu may differ by instance, role, and installed applications. Search the module name in **All** when a path below is absent.

| Work | Classic UI path or module search | Alternative |
|---|---|---|
| Catalog item | **All → Self-Service → Service Catalog** | Catalog in Employee Center / Service Portal |
| Submit as employee | **Employee Center → Request something** | Search **Employee Center** in **All** |
| Requests / items | Search **Requests** / **Requested Items** | Open **My Requests** and follow related items |
| Approvals | **All → Self-Service → My Approvals** | **Service Operations Workspace → My Approvals** |
| Incidents | **All → Incident → Create New** or **Incident → All** | Service Operations Workspace → Incidents |
| Problems | Search **Problems** | Related **Create Problem** action on an incident |
| Changes | Search **Change → Create New** | Create change from a linked incident or problem |


---

## Lab 1.2.1 — Verify the ITSM Environment

**Goal:** Confirm that the four key ITSM applications are accessible.
>Scenario: Before employees start using the help desk, you must confirm that the main ITSM applications are available.  

### TC010101 — Service Catalog application
1. Sign in to ServiceNow.
2. Open **All** and search **Service Catalog** in **Self-Service**.
3. Open the catalog through the available module or portal.
4. Confirm catalog categories or items are visible and can be opened (such as hardware, software, and services).
5. Capture a screenshot of the catalog landing page.

**Expected:** Service Catalog opens without an access or load error.

### TC010102 — Incident Management application
1. In the navigator, search **Incident**.
2. Open **Incidents / All** or **Incident > Open**.
3. Confirm the incident list loads.
4. Open an existing training incident if authorized.
5. Capture the list and relevant form fields.

**Expected:** Incident records can be viewed at the access level assigned to the account.

### TC010103 — Problem Management application
1. Search **Problem**.
2. Open the available **Problems / All** list.
3. Confirm existing problem records can be listed or an authorized **New** action is shown.
4. Capture evidence.

**Expected:** Problem Management is available to the assigned user.

### TC010104 — Change Management application
1. Search **Change**.
2. Open **Change > All** or **Change > Create New** as available.
3. Check for change types such as Normal, Standard, and Emergency.
4. Confirm change requests can be viewed, and the approved creation path is available if permitted.
5. Capture evidence.

**Expected:** The Change Management module loads without errors.

---

## Lab 2.3.1 — Verify Service Catalog Request and Approval

**Goal:** Validate employee request submission, automatic routing, manual approval, and service-desk visibility.

**Scenario:** A new TechReady employee needs a laptop. The employee submits a request, which may require manager approval before IT prepares the device.

### TC020101 — Submit request through Service Catalog
1. Open **All > Service Catalog** or the catalog portal linked in the instance.
2. Search for a permitted test catalog item, for example **Laptop**.
3. Open the item details.
4. Complete any required fields such as **Requested for**, delivery details, and justification.
5. Review the values and select **Order Now**, **Submit**, or the interface's equivalent.
6. Note the resulting **REQ** number and, if displayed, **RITM** number.
7. Open the submitted request in **My Requests** or **Service Catalog > Open Records > Requests**.
8. Capture the submission confirmation.

**Expected:** A request is created and can be found by its record number.

### TC020102 — Submit request through Employee Center
1. Open **Employee Center** if your instance has it enabled.
2. Select **Request something** or use the catalog search.
3. Open an eligible item (use a different test request if the course expects separate records).
4. Fill in required values and submit.
5. Open **My Requests** and locate the new request.
6. Record its REQ/RITM references.

**Expected:** Employee Center accepts the request and displays its tracking record.

### TC020103 — Verify automatic routing and manual approval
1. Open a test request configured to require approval.
2. Locate its **Approvals**, **Requested Item**, or **Approval History** related list (location varies).
3. Confirm the system created an approval record for the intended approver.
4. Sign in as the designated approver **only if authorized**, or use that account's approved workflow.
5. Navigate to **My Approvals**, open the pending approval, inspect the details, and select **Approve**.
6. Return to the request / requested item and refresh.
7. Confirm the approval status changed and fulfillment progressed as configured.
8. Capture before-and-after status screenshots.

**Expected:** Routing occurs based on the catalog item's configured flow, the authorized approver can act, and the request reflects the result.

### TC020104 — Verify Service Desk views and updates
1. With a permitted fulfiller account, open **Service Catalog > Open Records > Requests** or the relevant workspace list.
2. Search by the submitted REQ number.
3. Open the request and related RITM record.
4. Inspect **Requested for**, **Approval**, **State**, **Requested Items**, and related tasks.
5. If allowed, add a safe **Work note** such as `Request received; confirming assigned fulfillment team.`
6. Save / Update and refresh to verify the note is retained.
7. Capture the updated record.

**Expected:** Authorized service-desk staff can view request details and save permitted updates.

---

## Lab 2.3.2 — Verify Request Fulfillment Tracking

**Goal:** Track the lifecycle from REQ to RITM to fulfillment task.
>**Scenario:** The laptop request has been submitted and approved. Now IT must track and complete the work.

**Easy memory:** `REQ = The overall request`, `RITM = The individual item requested, such as a laptop`, `SCTASK = The work IT must perform to fulfill the item`.

### TC020201 — Verify requested item
1. Find the REQ from Lab 2.3.1.
2. Open its **Requested Items** related list.
3. Select the RITM record.
4. Confirm the item name, requested-for person, approval, assignment, and current stage/state.
5. Record the RITM number and capture a screenshot.

**Expected:** The RITM is linked to its parent request and contains accurate details.

### TC020202 — Verify requested item tasks
1. Inside the RITM, find **Catalog Tasks** or **Tasks**.
2. Open a generated task, if the item's fulfillment process created one.
3. Check the assignment group, assignee, short description, and state.
4. If authorized, take ownership, add a work note, and move the task through appropriate states.
5. Complete only work actually performed in the training scenario; save the task.
6. Check whether the RITM stage changes after task completion.

**Expected:** Configured fulfillment tasks are linked to the RITM and can be updated by an authorized fulfiller.

### TC020203 — Verify request state
1. Open the REQ and RITM again.
2. Check status before approval, after approval, and after fulfillment.
3. Compare displayed states with your eBook's expected values.
4. Capture final state and record the outcome.

**Expected:** Request and item status accurately reflects the configured workflow. REQ and RITM states need not use the same wording.

---

## Lab 3.2.1 — Verify Incident Record Creation

**Goal:** Log and escalate a service interruption.

**Scenario:** `An employee reports that their laptop cannot connect to the company Wi-Fi.`.

### TC030101 — Create incident
1. Open **All > Incident > Open** or **Incidents > All**; select **New**.
2. Enter the authorized test employee in **Caller**.
3. Set **Short description**: `Employee unable to connect to corporate Wi-Fi`.
4. Enter **Description**: `User reports Wi-Fi authentication failures since 9:00 AM. Other applications work on a wired connection. Troubleshooting requested.`
5. Select the appropriate **Category** (commonly Network), **Impact**, and **Urgency** using the eBook's required values.
6. Select the support **Assignment group** available in the lab.
7. Save by selecting **Submit** or **Save**.
8. Record the `INC` number and reopen the incident to verify saved fields.
9. Capture the incident form.

**Suggested example values** (use the eBook values if provided):

| Form field | Suggested value |
|---|---|
| Caller | Authorized training user |
| Category | Network, if available |
| Channel | Phone, if present |
| Impact | 3 – Low (example only) |
| Urgency | 2 – Medium (example only) |
| Short description | Employee unable to connect to corporate Wi-Fi |
| Assignment group | Authorized Service Desk or Network Support group |
| State | New |

**Expected:** A new incident appears with the correct caller, issue, priority calculation, and assignment.

### TC030102 — Escalate incident
1. Open the saved incident.
2. Review impact and urgency; increase them only when the business impact supports it and the eBook directs this.
3. If specialized troubleshooting is needed, change **Assignment group** to the designated network team.
4. Add a **Work note**: `Initial checks completed. Network team assistance required to investigate repeated wireless authentication failures.`
5. Save and check the new assignment and updated activity history.
6. Capture the escalation evidence.

**Expected:** The incident is routed to the responsible team, with justification documented.

---

## Lab 3.2.2 — Verify Incident Tracking and Resolution

**Goal:** Update incident information, create related records, and verify resolution.

>**Scenario:** The Network Support team investigates the incident and restores the employee's connection.

### TC030201 — Verify incident information
1. Find the INC number from Lab 3.2.1.
2. Inspect **Caller**, **Short description**, **Description**, **Impact**, **Urgency**, **Priority**, **Assigned to**, **Assignment group**, and **State** where displayed.
3. Add a work note documenting a permitted diagnostic step, such as verifying the device's connection and testing the network.
4. Save; confirm the activity log shows the update.

**Expected:** The incident's information and history are visible and accurate.

### TC030202 — Verify related record creation
>Scenario: The same Wi-Fi problem has happened to several employees, so IT needs to investigate a possible common cause.
1. From the incident, locate **Related Records**, **Create Problem**, or a corresponding action.
2. If the same failure has recurred and the test requires it, create or link a problem record.
3. Enter an appropriate problem summary and associate it with the incident.
4. Save and capture the new related `PRB` number.
5. Return to the incident and confirm the problem relationship appears.

**Expected:** The related record is created and connected to the incident. UI options and required roles vary.

### TC030203 — Verify incident resolution
>Scenario: IT determines that reconnecting the laptop to the correct Wi-Fi network restores the employee's access. This is a temporary incident fix while the wider network problem remains under investigation.
1. Confirm a documented resolution is actually demonstrated in the lab (for example, correcting an approved wireless setting and verifying the user can reconnect).
2. Open the incident and enter **Resolution code** and **Resolution notes** if required.
3. Example resolution note: `Validated network access after approved wireless configuration correction. User confirmed the connection works.`
4. Set the incident to **Resolved** using the allowed state transition.
5. Save and confirm the state and resolution fields persist.
6. Close only if the course workflow instructs you to close it; resolution and closure may be separate steps.

**Expected:** Incident resolution is documented, and the state accurately reflects the result.

---

## Lab 3.3.1 — Verify Problem Record Creation and Assessment

**Goal:** Investigate recurring incidents rather than treating every report as an unrelated ticket.

**Scenario:** Several employees report recurring Wi-Fi disconnections. IT must investigate the underlying cause.

### TC030301 — Create a problem record
1. Open **All > Problem > Open** or your Problem list, and select **New**.
2. Or, from the incident, select **Create Problem** if available.
3. Enter **Short description**: `Recurring corporate Wi-Fi authentication failures`.
4. Enter **Description**: `Multiple incidents report intermittent authentication failures affecting office wireless access.`
5. Fill in the required assignment and service / CI fields specified by the lab.
6. Save and record the `PRB` number.
7. Link relevant incident records using **Related Incidents** or equivalent.

**Expected:** A problem exists and relevant incidents are linked.

### TC030302 — Assess the problem
1. Open the PRB record.
2. Review business impact, affected users/services, recurrence, priority, and any specified configuration item.
3. Record a hypothesis, such as `Recent wireless configuration may have introduced an authentication mismatch`.
4. Assign investigation to the responsible team.
5. Save and verify work notes, assignment, and current state.

**Expected:** The problem includes meaningful initial assessment and an assigned investigation owner.

---

## Lab 3.3.2 — Verify Problem Diagnosis and Resolution

**Goal:** Document root cause, workaround, permanent fix, and closure.

>Scenario: Network Support discovers that an incorrect wireless access point configuration may be causing recurring disconnections.

### TC030401 — Diagnose the problem
1. Open the PRB record.
2. Review its associated incidents and observations.
3. Document the investigation with confirmed evidence from the lab.
4. Example *hypothesis only*: `Wireless policy changed and no longer matches the client authentication configuration`.
5. Record a temporary workaround if one was verified, for example using a wired connection.
6. If the diagnosis is confirmed, fill **Root cause** and applicable **Workaround** fields.
7. Save, inspect state, and capture evidence.

**Expected:** The record contains the diagnosis, supporting findings, and workaround if applicable. Never describe an unverified hypothesis as a confirmed root cause.

### TC030402 — Verify solution and closure
1. Determine whether the permanent fix requires a controlled change.
2. If it does, create or link the authorized change request from the PRB.
3. Confirm the approved fix was applied and retested.
4. Document test results and final root cause.
5. Move the problem through the states permitted by the configured workflow; resolve or close it only when its closure criteria are satisfied.
6. Save and capture the final record and linked change reference.

**Expected:** The problem is updated with a validated solution and its final state follows the configured lifecycle.

---

## Lab 4.2.1 — Verify Change Creation and Authorization

**Goal:** Propose and authorize a controlled change.

**Scenario:** Network Support recommends correcting the wireless access point configuration. Because the change may interrupt connectivity, the IT team must evaluate the risk and receive approval..

### TC040101 — Create and schedule a change
1. Navigate to **All > Change > Create New**, or create a change from the related PRB if permitted.
2. Select **Normal Change** for a change that requires assessment and approval (unless the eBook specifies otherwise).
3. Enter **Short description**: `Correct corporate Wi-Fi authentication configuration`.
4. Add **Description**: `Standardize wireless authentication settings to address validated connection failures.`
5. Select the relevant **Service** / **Configuration item (CI)** and assignment group when required.
6. Set **Planned start** and **Planned end** times using the course's permitted training dates, and check for conflicts where supported.
7. Enter **Implementation plan**, **Test plan**, and **Backout plan** (examples below).
8. Save and record the `CHG` number.

**Example implementation plan:** `Back up current settings; verify current baseline; apply approved authentication settings in maintenance window; validate test device connections.`

**Example test plan:** `Connect approved test devices; confirm authentication succeeds; verify affected employees can access required resources; monitor for repeat failures.`

**Example backout plan:** `Restore the captured prior settings if validation fails; verify connectivity returns to the baseline; notify stakeholders.`

**Change planning field checklist:**

- **Justification:** Why is the change needed?
- **Service / CI:** What system is affected?
- **Planned start / end:** When will approved work happen?
- **Implementation plan:** What exact approved steps will be done?
- **Test plan:** What will demonstrate success?
- **Backout plan:** How will the old configuration be restored if testing fails?
- **Risk / Impact:** What could break, and how many users could be affected?

**Expected:** A CHG record is created with planned timing and implementation safeguards.

### TC040102 — Verify risk assessment and CI updates
>CI means Configuration Item. In this example, the CI is the network access point that IT wants to modify.
1. Open the CHG record and locate **Risk**, **Impact**, **Configuration item**, and risk-assessment actions.
2. Complete any configured **Risk Assessment** questionnaire with actual lab values.
3. Verify the selected CI identifies the system being changed.
4. Update the CI reference or relevant CI information only when the eBook requires it and you are authorized.
5. Save; confirm risk and CI references are retained.

**Expected:** Risk information and the affected CI are documented accurately. CI updates are not the same as editing the CI database arbitrarily.

### TC040103 — Verify approvals and authorization
1. Advance the CHG using the configured transition to its assessment / authorization stage.
2. Locate its **Approvers**, **Approvals**, or related authorization records.
3. Confirm an approval record was generated for the appropriate authority when applicable.
4. Ask the designated authorized approver to review and approve within the lab workflow (or use the assigned test role if explicitly allowed).
5. Refresh the CHG and verify approval state and audit trail.
6. Do not implement the change before the approval required by the workflow is granted.

**Expected:** Approval and authorization are documented before implementation.

---

## Lab 4.2.2 — Verify Change Tracking and Closure

**Goal:** Track change tasks and close a successfully implemented change.

>Scenario: The change has been approved. The Network Support team needs a task to carry out the planned work.

### TC040201 — Verify change tasks
1. Open the CHG from Lab 4.2.1.
2. Find **Change Tasks** or the related task list.
3. Open an existing generated task, or create a task if the configured workflow and your role permit it.
4. Example tasks: `Back up wireless configuration`; `Apply approved settings`; `Validate connectivity and monitor authentication`.
5. Assign each task to its designated group or technician.
6. Update work notes and task state as work is completed and verified.
7. Capture the task list and task status.

**Expected:** Change tasks are linked to the parent CHG and accurately reflect completed work.

### TC040202 — Verify change completion and closure
1. Ensure authorization is recorded and implementation and validation have actually occurred in the training scenario.
2. Review the change's implementation results and testing notes.
3. Update closure fields such as **Close code**, **Close notes**, or **Actual end** where configured.
4. Example close notes: `Approved wireless configuration update completed in scheduled window. Test devices authenticated successfully. No new connection failures observed during validation.`
5. Move the CHG to the configured completed / closed state.
6. Save; confirm final state, completed tasks, and linked problem/incident records.
7. Capture the final record.

**Expected:** The CHG can be closed with the required approval, implementation, testing, and closure documentation.

---

## Verification Matrix

Use **Pass**, **Fail**, or **Blocked** after performing each action. Blank statuses mean not yet verified.

| Test ID | Verification | Result | Evidence |
|---|---|---|---|
| TC010101 | Service Catalog available | Not tested | `screenshots/01-itsm-applications.png` |
| TC010102 | Incident application available | Not tested | `screenshots/01-itsm-applications.png` |
| TC010103 | Problem application available | Not tested | `screenshots/01-itsm-applications.png` |
| TC010104 | Change application available | Not tested | `screenshots/01-itsm-applications.png` |
| TC020101 | Submit Service Catalog request | Not tested | `screenshots/02-catalog-request.png` |
| TC020102 | Submit Employee Center request | Not tested | `screenshots/03-employee-center-request.png` |
| TC020103 | Request routing and approval | Not tested | `screenshots/04-request-approval.png` |
| TC020104 | Service Desk request updates | Not tested | `screenshots/04-request-approval.png` |
| TC020201 | Requested item visible | Not tested | `screenshots/05-requested-item-and-task.png` |
| TC020202 | Requested item tasks visible | Not tested | `screenshots/05-requested-item-and-task.png` |
| TC020203 | Request state updates | Not tested | `screenshots/05-requested-item-and-task.png` |
| TC030101 | Incident creation | Not tested | `screenshots/06-incident-created.png` |
| TC030102 | Incident escalation | Not tested | `screenshots/07-incident-escalated.png` |
| TC030201 | Incident data and history | Not tested | `screenshots/08-incident-related-records.png` |
| TC030202 | Related record creation | Not tested | `screenshots/08-incident-related-records.png` |
| TC030203 | Incident resolution | Not tested | `screenshots/09-incident-resolved.png` |
| TC030301 | Problem creation | Not tested | `screenshots/10-problem-created.png` |
| TC030302 | Problem assessment | Not tested | `screenshots/10-problem-created.png` |
| TC030401 | Problem diagnosis | Not tested | `screenshots/11-problem-diagnosis.png` |
| TC030402 | Problem solution and closure | Not tested | `screenshots/12-problem-closed.png` |
| TC040101 | Change creation and scheduling | Not tested | `screenshots/13-change-created.png` |
| TC040102 | Risk and CI updates | Not tested | `screenshots/14-change-risk-and-ci.png` |
| TC040103 | Change authorization | Not tested | `screenshots/15-change-approved.png` |
| TC040201 | Change tasks | Not tested | `screenshots/16-change-tasks.png` |
| TC040202 | Change completion and closure | Not tested | `screenshots/17-change-closed.png` |

**Note:** Evidence links are filenames to populate after collecting screenshots; they are not included in this starter README. Replace filenames if you use different captures. To embed an image in GitHub Markdown, use `![Description](screenshots/filename.png)` after the file exists.

## Example IT Support Work Notes (copy only when accurate)

| Record | Example work note |
|---|---|
| Request / RITM | `Catalog item reviewed; awaiting configured approval and fulfillment assignment.` |
| SCTASK | `Device preparation started; hardware and access checks pending validation.` |
| Incident | `Verified user cannot authenticate to corporate Wi-Fi; wired connection succeeds. Escalated for network investigation.` |
| Problem | `Compared multiple incidents; reviewing wireless policy changes as a possible root cause.` |
| Change | `Implementation and validation steps documented. Awaiting required authorization before execution.` |

Only paste a note that truthfully describes work you performed or observed in the training instance.

## Troubleshooting Missing Buttons or Modules

| What you see | What to check |
|---|---|
| **Employee Center** not available | Check if the module is provisioned; use the eBook-prescribed interface; mark Blocked if unavailable |
| No **Approve** button | Verify that the current account is an assigned, authorized approver and the record is awaiting approval |
| No **Catalog Tasks** | Verify that the catalog item has the proper fulfillment flow and that required approval is complete |
| No **Create Problem** action | Look for related-record actions or create a new Problem and link the incident, if permitted |
| No **Risk Assessment** | Verify normal/emergency change type, state, role, and that risk assessment is configured |
| Change Task read-only | Check task ownership, role, and change state; do not override permissions |
| Cannot close problem or change | Check mandatory fields, outstanding tasks, approvals, and required state transitions |

## Results and Lessons Learned

*Complete this section after running the labs.*

- **Test cases executed:** ___ / 25
- **Passed:** ___
- **Failed:** ___
- **Blocked:** ___
- **Created records:** REQ ___, RITM ___, INC ___, PRB ___, CHG ___
- **Workflow observations:** ___
- **Issues / troubleshooting:** ___
- **Skills demonstrated:** ITSM navigation, structured ticket documentation, request fulfillment, service restoration, investigation, authorized change tracking.

## Value to IT Operations

This portfolio project demonstrates how to document service requests and disruptions, route work to the correct teams, maintain auditable approvals, connect incidents to long-term problem investigations, and close controlled changes only after validation. It models a service desk focused on traceability, customer impact, and responsible operational change.

## GitHub Evidence Convention

After capturing screenshots, upload files into the `screenshots/` folder and use Markdown image links in the appropriate lab section, for example:

```markdown
![Incident created in ServiceNow](screenshots/06-incident-created.png)
```

Do not insert broken image links before the screenshot actually exists. Use sanitized training evidence only.

## References

- Course eBook: Labs 1.2.1, 2.3.1, 2.3.2, 3.2.1, 3.2.2, 3.3.1, 3.3.2, 4.2.1, 4.2.2 (test objectives supplied by the learner)
- [ServiceNow Track a request from the service catalog](https://www.servicenow.com/docs/r/it-service-management/procurement/t_TrackReqFromServiceCatalog.html)
- [ServiceNow Create a record from incident](https://www.servicenow.com/docs/r/it-service-management/incident-management/t_PromoteAnIncident.html)
- [ServiceNow Create a problem](https://www.servicenow.com/docs/r/it-service-management/problem-management/create-a-problem-v2.html)
- [ServiceNow Create a change request](https://www.servicenow.com/docs/r/it-service-management/change-management/t_CreateAChange.html)
- [ServiceNow Perform risk assessment](https://www.servicenow.com/docs/r/it-service-management/change-management/t_AssessRisk.html)
- [ServiceNow Create a change task](https://www.servicenow.com/docs/r/it-service-management/change-management/create-a-change-task.html)

---

*Documentation based on simulated training scenarios. Product names belong to their respective owners. Do not share production or personal information in screenshots.*
