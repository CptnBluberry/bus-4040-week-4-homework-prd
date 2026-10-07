# CBE Speaker & Event Management System

**Product Requirements Document** — Working Draft (Week 4)

| | |
|---|---|
| **Status** | Draft — to be validated with client |
| **Version** | 0.1 |
| **Team** | [Team name] |
| **Client** | CBE, University of Idaho (Center for Business and Economic Research) |
| **Last updated** | [Date] |

> This document describes **what** the product does and how we will know it works. It does not describe how it will be built, what technology it will use, or what it will look like.

---

## 1. Problem Statement

CBE runs executive education for the energy sector through three programs:

- The Energy Executive Course
- The Energy Executive Summit
- The Legislative Energy Horizon Institute

Over the past decade, event schedules and agendas for these programs have been maintained **manually, by different people, in files whose formats have drifted over time.** Looking up a past speaker, rebuilding a historical record, or assembling a new event schedule currently requires searching through inconsistent files by hand.

The problem we are solving: **CBE staff cannot reliably find, manage, and reuse information about past and future events and speakers.** The solution will be a local application that organizes the existing 2016–2026 event data into a single standard format, lets staff maintain it, and supports planning new events from it.

## 2. Goals

What does success look like?

- **G1.** A CBE staff member can find any past speaker or session from 2016–2026 in under a minute, without opening a drawer of files.
- **G2.** A staff member can correct, add, or remove records (speakers, sessions, events) directly in the app.
- **G3.** A staff member can build a new event schedule from scratch using the app, instead of a blank document.
- **G4.** The workflow of planning and recording events is free of the friction described by the client — no hunting through inconsistent files, no re-typing data.
- **G5.** The entire dataset can be backed up and restored without specialized technical knowledge.

Success, in the client's terms: *removing a point of friction from their workflow — a stress-free event planning experience, at least for the parts this product controls.*

## 3. Target Users / Personas

- **Primary user:** [Name/role — e.g., the CBE staff member who plans the three programs.] This person creates and maintains event schedules, looks up past speakers, and produces event documents. [Confirm: is this one person or a small team? How many people will use the app simultaneously?]
- **Secondary user(s):** [Other CBE staff who may look up speakers or review past events — confirm with client.]
- **Non-users:** Attendees, speakers, and the public will **not** use this system directly. All data in scope is public, but the product itself is an internal staff tool. [Confirm there is no need for web access or sharing by link in v1.]

## 4. Scope

### In scope (v1)

- Organizing the existing 2016–2026 event and speaker data into one standard format
- Maintaining records: add, edit, delete speakers, sessions, and events
- Searching and browsing historical data
- Basic analysis/reporting on the data [see OQ-2 for what "analysis" means to the client]
- Backup and restore of the entire dataset
- Building a new event schedule

### Out of scope (v1)

- Public-facing or web-based access; the product is a local, staff-only tool
- Scheduling logistics beyond the program itself: venue booking, travel, catering, speaker invitations/emails
- Automatic import from email, calendar systems, or third-party sources [confirm none exist today]
- [Any feature the team and client agree to defer — fill in after client meeting]

## 5. Constraints

- **C1. Local only.** The product must run on the user's own machine with no server, no account, and no internet dependency.
- **C2. Cross-platform.** The product must run on both macOS and Windows.
- **C3. Modest footprint.** The application and its data should remain small enough to copy, move, and back up easily; no large or sprawling install.

## 6. Functional Requirements

Priority: **M** = Must, **S** = Should, **C** = Could.

### Data organization

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | The system shall accept the existing 2016–2026 event schedules and agendas as input and organize them into a single, consistent, standard format. | M |
| FR-02 | The standard format shall represent at least: an **event** (program, year, [dates? location?]), a **session** (title, time, day, event), and a **speaker** (name, [affiliation, title, program/year spoken, notes?]). | M |
| FR-03 | The system shall preserve, for every imported record, which source file and which program/year it came from, so no information is silently lost during organization. | S |
| FR-04 | Where source data is ambiguous, conflicting, or incomplete, the system shall surface this to the user rather than guessing. | S |

### Record management

| ID | Requirement | Priority |
|---|---|---|
| FR-05 | The system shall let a user **add, edit, and delete** speaker, session, and event records. | M |
| FR-06 | The system shall prevent a deletion or edit from silently destroying related records (e.g., deleting a speaker who has 14 historical sessions must make that consequence visible). | M |
| FR-07 | The system shall make it possible to detect and resolve records that likely refer to the same real-world person or event appearing in more than one form (e.g., "Dr. Smith" in one year's file and "Dr. J. Smith" in another). | S |
| FR-08 | The system shall allow a session to be marked as cancelled/not-attended, so historical records reflect what actually happened. [Confirm with client — see OQ-3.] | S |

### Search

| ID | Requirement | Priority |
|---|---|---|
| FR-09 | The system shall let a user search and filter speakers, sessions, and events across all years by at least name, program, and year. | M |
| FR-10 | Search shall be forgiving of partial names and minor spelling variations common in hand-made files. [Confirm expected level.] | S |

### Analysis

| ID | Requirement | Priority |
|---|---|---|
| FR-11 | The system shall let a user view historical records grouped by program and year (e.g., "everyone who spoke at the 2019 Summit"). | M |
| FR-12 | The system shall support the specific analyses the client performs today [see OQ-2 — replace this row with concrete requirements after the client meeting]. | S |

### Backup and restore

| ID | Requirement | Priority |
|---|---|---|
| FR-13 | The user shall be able to create a backup of the **complete** dataset at any time, and restore it on the same or another compatible machine, with no data loss. | M |
| FR-14 | A restore from backup shall reproduce the system's state exactly as it was at backup time. | M |

### New event scheduling

| ID | Requirement | Priority |
|---|---|---|
| FR-15 | The user shall be able to create a new event with the same structure as historical events and build its schedule by adding sessions and selecting speakers — reusing known speakers from the archive instead of re-entering them. | M |
| FR-16 | A finished or in-progress new schedule shall be exportable as [document format — PDF? Word? CSV? — confirm with client, OQ-5] for distribution to attendees/speakers. | M |
| FR-17 | When a new event is finalized, its records shall merge into the historical archive so future years can search them. | S |

## 7. User Scenarios

Written in the past, from the client's actual work — each maps to the requirements that cover it.

**Scenario A — "Who was that speaker?"**
A staff member needs to find a past speaker (e.g., to confirm a name for a newsletter, or to re-invite them). Today: digging through files, guessing which year. With the product: a single search returns the person and every event they spoke at. *(FR-09, FR-10, FR-11)*

**Scenario B — "The records disagree."**
The same person appears in one year's agenda with one title and in another's with a different name format. Today: nobody notices, or it takes manual comparison. With the product: the system surfaces the likely duplicates and the user decides — one record or two. *(FR-07, FR-04)*

**Scenario C — "Somebody cancelled."**
An agenda lists a speaker who never showed up. The historical record must reflect reality. With the product: the session can be marked cancelled, and analyses can include or exclude it. *(FR-08)*

**Scenario D — "Time to plan next year's program."**
The staff member builds next year's schedule from scratch: new event, new sessions, pulling in returning speakers by name, adding new ones. When done, the schedule is exported as a distributable document and filed into the archive. *(FR-15, FR-16, FR-17)*

**Scenario E — "The machine is new."**
The user gets a new computer (Mac or Windows) and restores everything from a backup; all ten years of data and any in-progress schedule come back intact. *(FR-13, FR-14, C1–C3)*

## 8. Acceptance Criteria

The product is "done" for v1 when all of the following can be demonstrated:

1. A user opens the app for the first time on macOS **and** on Windows and can reach a working state without any server or internet connection.
2. The full 2016–2026 dataset has been imported into one consistent format, and a spot-check against the original files finds no record lost.
3. A search by a partial speaker name returns every matching historical session across programs and years.
4. The user can add a new speaker, edit an existing session, and delete a record — and deleting something with historical references shows the consequence before it happens.
5. The user creates a new event, builds a schedule of at least [N] sessions using a mix of archived and new speakers, and exports it as the agreed document format.
6. A backup is created, the data store is emptied or moved, and a restore from that backup reproduces the exact prior state.
7. [Add client-specific criteria after the meeting — e.g., a known past-speaker lookup the client will personally test.]

## 9. Open Questions for the Client

*(Past-tense, specific, no solutions offered — one per team member is due before class.)*

- **OQ-1 (personas/scale):** Walk me through how you built your last event schedule. Where did you start, and who else touched it before it went out?
- **OQ-2 (analysis):** Tell me about the last time you used past event data for something other than looking up a speaker — a report, a decision, a statistic. What did you put together, and how?
- **OQ-3 (cancelled/ambiguous records):** Some old agendas list speakers who may not have shown up, or who are spelled differently across years. When you've run into one of those, what did you do with it?
- **OQ-4 (one or two?):** If someone spoke in 2018 as a utility VP and in 2024 as a consultant — in your files, is that one person or two? What made it look that way?
- **OQ-5 (output format):** When a schedule is finished, what do you hand out or send — and in what format do those documents actually end up?
- **OQ-6 (search context):** When you look up a past speaker, what do you usually already know about them — just the name, or the company, the year, the topic?
- **OQ-7 (pain points):** Tell me about the last time a planning task on these programs went wrong or took longer than it should have. What happened?

## 10. Assumptions

- A1. [Number] people will use the system, on their own machines, with no concurrent editing of the same dataset. *(confirm — OQ-1)*
- A2. The 2016–2026 files provided by the client are the complete set of historical data; nothing else needs importing. *(confirm)*
- A3. All data is public and non-confidential, per the client.
- A4. v1 is a single-user-per-machine product; multi-user collaboration is out of scope. *(confirm — OQ-1)*
- A5. "Standard format" means one consistent structure inside the system plus exportable output (OQ-5); it does not imply compatibility with any external system. *(confirm)*

## 11. Revision History

| Version | Date | Notes |
|---|---|---|
| 0.1 | [Date] | Initial team draft from course material; to be validated with client. |