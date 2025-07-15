# Uppaal_Project
# Scholarship Application Portal Model (UPPAAL)

[cite_start]This project presents a formal model of a Scholarship Application Portal, developed using the UPPAAL model checker[cite: 13]. [cite_start]It simulates the interactions between a user and the portal, encompassing functionalities such as scholarship applications, fetching academic transcripts, and accessing personal information[cite: 13]. [cite_start]The system is designed to ensure secure authentication for unique users, prevent multiple scholarship applications within a single session, and manage interactions with external components[cite: 14, 15, 16, 17].

## Table of Contents

* [Project Overview](#project-overview)
* [Key Components](#key-components)
* [Assumptions](#assumptions)
* [Verification (Liveness & Safety Properties)](#verification-liveness--safety-properties)
* [Contributions](#contributions)
* [Files Included](#files-included)

## Project Overview

The Scholarship Application Portal model aims to simulate a realistic online system where students can log in, apply for scholarships, and access their personal and academic data. The model utilizes UPPAAL to formally verify critical system properties, ensuring reliability and consistency.

## Key Components

The model is composed of several interconnected templates, each handling specific functionalities:

### 1. Website Model
* [cite_start]Handles user login, navigation to the homepage, scholarship application, and logout[cite: 23].
* [cite_start]Distinguishes between Merit Scholarship and Merit-Cum-Need (MCN) Scholarship applications[cite: 23].
* [cite_start]Ensures that only one type of scholarship can be applied for in a single session[cite: 24].

### 2. CredentialChecker Model
* [cite_start]Authenticates unique users based on their email IDs and passwords[cite: 49].
* [cite_start]Manages login requests and responses, with key states including `Waiting` and `Verifying`[cite: 51, 52].
* [cite_start]For simplicity in modeling, input credentials (email and password) are represented as integers[cite: 54].
* [cite_start]Tracks authenticated users globally to prevent duplicate logins[cite: 50].

### 3. ScholarshipComm Model
* [cite_start]Evaluates scholarship applications based on predefined CGPA thresholds[cite: 69].
    * [cite_start]**Merit Scholarship:** Requires a minimum CGPA of 9 (as per `meritCutoff` in the model)[cite: 70, 73].
    * [cite_start]**MCN Scholarship:** Requires a minimum CGPA of 8 (as per `mcnCutoff` in the model)[cite: 70, 72].
* [cite_start]Processes scholarship requests from the Website model and communicates the decision back[cite: 74].
* [cite_start]A default CGPA of 8 is used for checking purposes as user inputs are not handled[cite: 75].
* [cite_start]Restricts further scholarship applications once one has been applied[cite: 78].

### 4. TranscriptInfo Model
* [cite_start]Handles requests for academic transcripts and personal information[cite: 98].
* [cite_start]Capable of generating data based on assumed user data from an academic server[cite: 99, 100].
* [cite_start]Ensures availability of requested data and includes a fallback state for missing information[cite: 101].

### 5. User Model
* [cite_start]A simplified model representing user interactions for accessing the website[cite: 111, 116, 117].

## Assumptions

The model operates under the following assumptions for simplicity and scope:
* [cite_start]Every user is assumed to have a unique ID and valid credentials, verified by an authentication server[cite: 119, 120].
* [cite_start]The model does not ensure records for users logging in from multiple devices or multiple times; each login is treated as a new user session[cite: 121, 122].
* [cite_start]Only one student/user interacts with the model at any given instance[cite: 123].
* [cite_start]The portal ensures state synchronization for consistent user actions[cite: 124].
* [cite_start]Immediate server responses are assumed, without modeling delays or clocks[cite: 127].
* [cite_start]Transcript and personal information are assumed to exist unless specified otherwise[cite: 131].
* [cite_start]Default values (e.g., email=1, password=123, CGPA=8) are used for modeling purposes[cite: 75, 130].

## Verification (Liveness & Safety Properties)

The model has been rigorously verified for key Liveness and Safety properties using UPPAAL queries to ensure its correctness and reliability.

### Liveness Properties (Example Queries)
* [cite_start]**E<>ScholarshipComm.Approved**: Ensures there exists a path where the state of `Approved` is eventually reached for ScholarshipComm[cite: 135, 136].
* [cite_start]**E<>CredentialChecker.Success**: Verifies that the `Success` state in CredentialChecker is eventually reachable[cite: 137, 138].
* [cite_start]**E<>ScholarshipComm.Idle imply ScholarshipComm.scholarshipApplied**: Checks that if `ScholarshipComm.Idle` is reached, it implies `scholarshipApplied` is true[cite: 141, 142].
* [cite_start]**E<>(ScholarshipComm.Approved || ScholarshipComm.Rejected)**: Asserts that ScholarshipComm will eventually reach either an `Approved` or `Rejected` state[cite: 145, 146].

### Safety Properties (Example Queries)
* [cite_start]**A[] !deadlock**: Confirms that there are no deadlocks in the model, ensuring the system does not get stuck[cite: 148, 149].
* [cite_start]**E[]ScholarshipComm.EvaluatingMerit imply ScholarshipComm.scholarshipApplied**: Verifies that if `EvaluatingMerit` is reached, `scholarshipApplied` remains true along that path[cite: 150, 151, 152].
* [cite_start]**E[]CredentialChecker.Verifying imply (!CredentialChecker.is_authenticated || CredentialChecker.is_authenticated)**: Ensures that if the system is in the `Verifying` state, it will either be authenticated or not authenticated[cite: 159, 160].

## Contributions

This project was a collaborative effort. My specific contributions include:
* [**Your Name**]: (Replace with your specific contributions from `GROUP21 _CONTRI (1).docx`)
    * [cite_start]Example: Assisted in designing the website templates and user model[cite: 4].
    * [cite_start]Example: Identified and resolved errors in various templates to ensure smooth model functionality[cite: 5].
    * [cite_start]Example: Contributed to clearing the deadlock condition[cite: 5].
    * *...and so on, for your specific tasks listed in the document.*

**(If you were a group member, list your specific contributions clearly here. If you are presenting this as an individual project and want to show what *you* did, make sure to clearly state your role and tasks from the group document.)**

## Files Included

* `LICS_final21assignmentB.xml`: The main UPPAAL model file containing all templates and global declarations.
* `Group_21_Assignment_ReportB.pdf`: Detailed project report including model descriptions, component breakdowns, assumptions, and a comprehensive list of Liveness and Safety properties with their evaluation results.
* `GROUP21 _CONTRI (1).docx`: Document outlining individual contributions of group members.
* `lics_assignment_Group21.txt`: Assignment submission details including course, instructors, and group member names.
