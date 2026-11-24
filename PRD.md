# Product Requirements Document (PRD)

**Course:** BU-209 Backend Engineering (Week 4)
**Product:** Lecture Attendance Management System (working name: uniScan)
**Group:** GROUP 6 DAEMON
**Members:**
1.Mshelia Abba Bata (25/1996)
2.Nelson Jeremiah Chibuke (25/1387)
3.Jaleyemi Moyosore Success (25/1462)
4.Ladenika Daraloba Emmanuel (25/1299)
5.Nwoko Uchenna Marcel (25/3024)

**Institution:** Babcock University
**Date:** 23 November 2026

## 1. Problem

Attendance at Babcock is mostly taken on paper or by roll call. It uses up lecture time, making a student late for his/her next class, students can also sign for friends who are not in class, and lecturers end up with sheets that are slow to total and easy to lose. Students also can't check their own attendance until it is too late to fix anything.

**Who has it:** students, lecturers, and HODs or admins who need attendance summaries.

**How people cope today:** sign sheets, roll call, and asking friends to sign. Google Forms links are sometimes used, but a link can be shared with someone outside the class, so there is no proof the student is present.

**Why existing options fall short:** paper and roll call are slow and easy to fake. Fingerprint systems need hardware and cause queues. Shared links can't confirm presence. It took the whole group C about 10 minutes to finish their fingerprint attendance during the Monday Chapel Seminar

## 2. Research

We surveyed students with a Google Form (https://forms.gle/fwyAVaRvpnGgiDzp6) and got (https://docs.google.com/spreadsheets/d/1dgfM6Ptn97l4h1IGlXv8dNJDOQtEJJpGmSz3NoWO_aQ/edit?usp=sharing) responses. We did not interview lecturers in this phase, so anything about lecturers below is an assumption we will check before building (We ran out of time). 

**Findings:**
- 42.9% said attendance takes too much lecture time
- 50% said they have signed for someone else or know it happens
- 92.9% have a smartphone with a working camera
- 50% said data or wifi would not be a problem
- 78.6% were comfortable scanning a QR code
- 57.1% were comfortable with the app checking their location


## 3. Objective and Success Measures

Replace paper attendance with a QR-code system where the lecturer starts a session, students scan, and records save automatically.

We will count it as working if:
- Attendance for a whole class takes under 2 minutes
- A lecturer can get a report in under a minute
- Most proxy-scan attempts in our own tests are caught or flagged

## 4. Proposed Solution

1. Lecturer starts an attendance session for a course.
2. A QR code is shown on the screen or projector and changes about every 20 seconds.
3. Students log in on their phones and scan it.
4. The system checks the scan and saves the record.
5. Lecturer sees a live count, closes the session, and downloads a report.

**Stopping students from scanning for others:**
- The rotating code makes a photo sent to a friend useless within seconds.
- Students must be logged in, so each scan is tied to an account.
- One device per account, so one phone can't be used for many students.
- One scan per student per session, only while the session is open.
- A location check, used only as a warning flag because indoor GPS is not reliable.
- A live count the lecturer can compare with the people in the room.
- Manual fixes by the lecturer are logged.

No system can fully stop two friends who swap phones on purpose. The goal is to make cheating harder and easier to notice than a paper sheet.

## 5. MVP Scope

**In version 1:**
- Login for students and lecturers (matric number / staff ID)
- Lecturers create courses, students enroll
- Start and end a session
- Rotating QR code and scan validation
- One scan per student per session, one device per account
- Live count for the lecturer
- Reports per session, course and student, with CSV download
- Student view of their own attendance percentage
- Manual add/remove by lecturer, with a log

**Later:** connecting to the school portal, low-attendance SMS/email alerts, face or fingerprint checks, offline scanning, native mobile apps, and a dashboard for many schools.

## 6. Backend Considerations

We are not choosing a language yet. The backend needs to handle:
- Login and roles (student, lecturer, admin)
- Creating sessions and codes that expire
- Validating scans (code, time, enrollment, duplicates)
- Storing attendance so it can't be quietly changed
- Reports, and a log of overrides and device changes

Main data: users, courses, enrollments, sessions, attendance records, devices, audit log.

Still to work out: how many students might scan at once in our biggest hall, how good the network is in halls, where it will be hosted, and how another school could set up its own copy.

## 7. Non-Functional Requirements

- A scan confirms within a few seconds, even when many students scan together
- Works on low-end Android phones with small data use
- Passwords stored hashed, data encrypted, users only see what they should
- Collect only what is needed (names, matric numbers, location) and follow the Nigeria Data Protection Act 2023
- Other schools can change courses, rules and branding without rewriting the system

## 8. Risks

- **Phone swapping or shared logins:** layered safeguards and an audit log.
- **Poor network or GPS in halls:** small requests, and location is only a flag.
- **Lecturers may not want to change (assumption):** make starting a session quick and pilot with one willing lecturer.
- **Students without smartphones:** lecturer manual override.
- **School approval:** ask for a small pilot in one department.

## 9. Next Steps

1. Interview a few lecturers and check our assumptions
2. Choose the technology and design the database and API
3. Build the MVP, then test it by trying to cheat it
4. Pilot in one class and collect feedback



