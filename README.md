# PostgreSQLDatabase
Created for my Databases module during my second year at the University of Derby. An example of a University database scheduling system which tracks tutors and students in different modules. 

Created using PostgreSQL 9.4 - https://www.postgresql.org/

## Entities and Relations
![ERDiagram](https://github.com/Hesketh/PostgreSQLDatabase/blob/master/EntityRelationshipDiagram.png?raw=true)
*Correction: There is a one-to-one connection from "Session Types" to "Modules" this should instead be a one-to-one connection from "Session Types" to "Module Schedule"*

## Tables
- **Students** (StudentNo [pk], Password)
  - Contains the login credentials for the students
- **Modules** (ModuleCode [pk], Title, ModuleLeaderID [fk])
  - All the modules that the University offers
- **SessionTypes** (SessionType [pk])
  - The different types of sessions, such as Lectures or Tutorials
- **Tutors** (TutorID [pk], Name, Email, PhoneNo)
  - All the tutors employed by the University
- **ModuleLeaders** (ModuleLeaderID [pk], TutorID [pk][fk], OfficeHours, OfficeNo)
  - If a tutor is a module leader, they have additional information such as office hours and an office number
- **ModuleTutors** (TutorID [pk][fk], ModuleCode [pk][fk])
  - Multiple tutors can teach a single module, so each individual tutor for each individual module is recorded
- **ModuleSchedule** (ModScheduleID [pk], ModuleCode [fk], SessionType [fk], StartTime, DayOfWeek, Duration, Location)
  - The times that a module has a schedules session
- **Assessments** (AssessID [pk], ModuleCode [fk], Description, Deadline)
  - Information about any assessments that a module gives to their students
- **StudentSchedule** (StudScheduleID [pk], StudentNo [fk], StartDateTime, Duration, Description)
  - A custom event the student makes for their personal calendar
- **Enrolment** (StudentNo [pk][fk], ModuleCode [pk][fk], SemesterCode [pk][fk], EnrolYear [pk])
  - Each module that a specific student is enrolled in for a specific semester and year
- **TutorialSessions** (StudentNo [pk][fk], ModuleScheduleID [pk][fk])
  - The tutorial session that a student will go to
  - Multiple tutorials are scheduled in the module schedule but students only want to sign up to go to one
  - The specification however said that they were still to have access to the times of the other tutorials
- **Semesters** (SemesterCode [pk], Description)
  - The semesters through the year such as Summer or Autumn.
