# Hack The Tunnels - Starter 2024

![Hack The Tunnels](https://i.imgur.com/1NCyXkn.png)

This is the project template for [Hack The Tunnels](https://ccss.carleton.ca/hackthetunnels/).

The project template utilizes [React](https://react.dev/), [TypeScript](https://www.typescriptlang.org/), [Express](https://expressjs.com/), and [Prisma](https://www.prisma.io/).

## Table of Contents

- [Event Setup Instructions](#event-setup-instructions)
    - [Windows Setup](#windows-setup)
    - [Mac Setup](#mac-setup)
    - [Project Setup](#project-setup)
        - [Create a Github Repository for the Project](#create-a-github-repository-for-the-project)
        - [Client Setup](#client-setup)
        - [Service Setup](#service-setup)
- [Documentation](#documentation)
    - [Important Files and Folders](#important-files-and-folders)
        - [Client](#client)
        - [Service](#service)
    - [Views](#views)
        - [Login Page - `/`](#login-page---)
        - [Menu Page - `/`](#menu-page---)
        - [Build Timetable Page - `/timetables/build`](#build-timetable-page---timetablesbuild)
        - [Timetables Page - `/timetables`](#timetables-page---timetables)
        - [View Timetable Page - `/timetables/:id`](#view-timetable-page---timetablesid)
    - [API Routes](#api-routes)
        - [Login - `POST /login`](#login---post-login)
        - [All Scheduled Events - `GET /scheduledEvents`](#all-scheduled-events---get-scheduledevents)
        - [Account's Timetables - `GET /timetables`](#accounts-timetables---get-timetables)
        - [Create Timetable - `POST timetables`](#create-timetable---post-timetables)
        - [View Timetable - `GET /timetables/:id`](#view-timetable---get-timetablesid)
    - [Database Schema](#database-schema)
        - [Account](#account)
        - [Course](#course)
        - [Scheduled Event](#scheduled-event)
        - [Timetable](#timetable)
        - [Timetable Event](#timetable-event)

# Event Setup Instructions

To avoid many of the environment setup-related issues that occur with Windows, we will be having all [Hack The Tunnels 2024](https://ccss.carleton.ca/hackthetunnels/) participants set up [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/about).

If you are a Windows user, you should follow the [Windows Setup](#windows-setup) and then follow the [Project Setup](#project-setup) in your new WSL environment.

If you are a Mac or Linux user, instead follow the [Mac Setup](#mac-setup) and then follow the [Project Setup](#project-setup) instructions.

Both guides will have you set up [Homebrew](https://brew.sh/) to manage dependencies. Homebrew will help you install additional software like Node.js, Git, Gh, etc.


## Windows Setup
In Powershell or Command Prompt, run the following commands

1. Install WSL

```
wsl --install
```

2. Set WSL to use version 2 as the default.

```
wsl --set-default-version 2
```

3. Install the Ubuntu distribution within WSL.

```
wsl --install -d ubuntu
```
**Note: You will need to create a Linux user**

4. Install Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

5. Follow the on-screen instructions to add Homebrew to your PATH.

```
(This will be instructions displayed after the Homebrew installation)
```

6. Refresh your terminal session to apply the changes made to .bashrc

```
source ~/.bashrc
```

7. Install Node.js

```
brew install node
```

8. Install Git

```
brew install git
```

## Mac Setup
In the Terminal, run the following commands

1. Install Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Install Node.js

```
brew install node
```

3. Install Git

```
brew install git
```

## Project Setup

### Create a Github Repository for the Project

Click on "Use this template" > Create a new repository

![image](https://github.com/user-attachments/assets/ccefc342-83b2-4258-aa73-bc061358008a)

In your WSL terminal (for Windows) or the terminal (for Mac), run the following commands

1. Clone the repository

```
git clone https://github.com/your-github-username/your-repository-name.git
```

2. Move into the project directory

```
cd your-repository-name
```

### Client Setup

1. Move into the client directory

```
cd client
```

2. Install client dependencies

```
npm install
```

3. Run the client

```
npm run dev
```

### Service Setup

Follow the following instructions in a 2nd terminal while your client is running.

1. Move into the service directory

```
cd service
```

2. Install service dependencies

```
npm install
```

3. Run Migrations

```
npx prisma migrate dev
```

4. Run the service

```
npm run dev
```

To get the project working, you will need to have both the client and server running.

# Documentation

The project template for this year is a recreation of the **infamously hard to use Carleton Central**.

Students will be tasked with recreating and improving many of the core components of the application.


## Important Files and Folders

### Client

- `main.tsx`: Initialises app and describes routing for pages
- `client/src/pages`: Where code for individual pages in the web app live
- `client/src/components`: Where code for "components" (ui pieces reusable across pages) live
- `client/src/layouts`: Where code for "layouts", which are kind of like "page themes" live
- `client/src/infrastructure/ServiceAPI`: Where code the evokes the Service via RESTful API live

### Service

- `service/src/api/router.ts`: Where Express.js RESTful API routes are defined
- `service/src/api/routes`: Where all other routers are defined
- `service/src/services`: "Services" are code that handle "business logic" like creating a timetable, handling user login, etc.
- `service/src/db/schema.prisma`: Where our database's schema is defiend. A database schema is the "shape" our data is stored in.

## Views

### Login Page - `/`

The following page is a mostly perfect recereation of the Carleton Central login page, however it should be noted that the inputs for email and password have been hardcoded to send `email: "admin@email.com", "password"` which is the default login information for one of the default accounts.

![image](https://github.com/user-attachments/assets/92644637-bc6e-436d-97ee-2df133262dca)

### Menu Page - `/`

The following page is known within the codebase as the "Menu Page". The only links that actually work on this page are clicking "logout", "Build Your Timetable/Registration", and "Student Timetables".

![image](https://github.com/user-attachments/assets/da5d65d2-ded5-4bcf-9349-30effe2a1d31)

### Build Timetable Page - `/timetables/build`

The following page is an amalgamation of the 4 different pages it takes in Carleton Central to build a timetable.

Upon clicking "search", a list of results will appear that can be added to your timesheet via their respective "add" buttons.

Selected events can be removed by clicking their associated "remove" button.

Upon clicking "create timetable", you will be redirected to that timetables "View Timetable Page".

![image](https://github.com/user-attachments/assets/86aff09c-4ff4-4240-b51b-14caf1774bbc)

### Timetables Page - `/timetables`

This is a page that does not exist in the real Carleton Central.

It acts as a way of all saved timetables associated with the account.

This screen may appear empty to you if you have not created a timetable on `/timetables/build`.

If you have created a timetable, you will likely see a strinified date string as its title, this is because the code the sends the create timetable request does not hard code a name so that it's easier to differentiate timetables:

```typescript
const createTimetable = async () => {
  const result = await ServiceAPI.createTimetable(
    new Date().toISOString(),
    selectedEvents.map((event) => event.id.toString()),
      jwt,
    );

    navigate(`/timetables/${result.data.id}`);
};
```

![image](https://github.com/user-attachments/assets/a881efdc-ef92-423e-afb6-24c589b02396)


### View Timetable Page - `/timetables/:id`

The following page simple allows you to view a previously created timetable.

![image](https://github.com/user-attachments/assets/cafa24e3-ef51-47ae-8b6b-c40ba8987d0f)


## API Routes

This application's RESTful API is powered by Express.js

All routes are appended underneith `{root}/api/v1/`. Ex: `http://localhost:5000/api/v1/scheduledEvents`

**NOTE:** Any endpoint that **requires authorization** must be appended with the **Authorization header** and **jwt token** retrieved from the [login endpoint](#login---post-login).

Example Authorization Header:

```
authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjoiYWRtaW5AZW1haWwuY29tIiwiaWF0IjoxNzI4OTMzNTE2fQ.RM6l7bRyl7gGVeT6prdkaTu_LBB9vWobotIT2CwjLTM
```

### Login - `POST /login`

This route returns a JWT token if the user succesfully entered a corresponding email and password.

Example Payload:

```json
{
  "email": "admin@email.com",
  "password": "password"
}
```

Example Response:

```json
{
  "data": {
    "token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjoiYWRtaW5AZW1haWwuY29tIiwiaWF0IjoxNzI4OTMzNTE2fQ.RM6l7bRyl7gGVeT6prdkaTu_LBB9vWobotIT2CwjLTM"
  },
  "error": null
}
```

### All Scheduled Events - `GET /scheduledEvents`

This route returns a list of available scheduled events.

Example Response: 

```json
{
  "data": [
    {
      "id": 986,
      "crn": "11116",
      "section": "A",
      "instructor": "Leila Chinaei",
      "credit": "0.5",
      "type": "Lecture",
      "term": "Winter 2025 (January-April)",
      "days": "Mon,Wed",
      "startTime": "10:05",
      "endTime": "11:25",
      "additionalRegistrationRequirements": "",
      "url": "https://central.carleton.ca/prod/bwysched.p_display_course?wsea_code=EXT&term_code=202510&disp=22184566&crn=11116",
      "description": "Section Type - IN-PERSON SECTION.For Arts & Social Science students only. See also fall term.Laptop required for all first year COMP courses.See https://carleton.ca/scs/scs-laptop-requirement/.Precludes additional credit for COMP 1004 (no longeroffered). This course cannot be taken for credit bystudents in Business, Engineering, Computer Science,Mathematics or Science.",
      "courseId": 1291,
      "createdAt": "2024-10-12T20:09:35.101Z",
      "updatedAt": "2024-10-12T20:09:35.101Z",
      "course": {
        "id": 1291,
        "subjectCode": "COMP",
        "courseCode": "1001",
        "title": "Introduction to Computational Thinking for Arts and Social Science Students",
        "shortTitle": "Computing for Arts Students",
        "description": "An introduction to computational thinking and its applications to the arts and social sciences.  Students will gain computational thinking skills by exploring data representation, basic programming concepts, a selection of algorithms, and advanced usage of software packages for the arts and social sciences.   Precludes additional credit for COMP 1004 (no longer offered).  This course cannot be taken for credit by students in Business, Engineering, Computer Science, Mathematics or Science.",
        "createdAt": "2024-10-12T20:09:32.190Z",
        "updatedAt": "2024-10-12T20:09:32.190Z"
      }
    },
    ...
  ],
  "error": null
}
```

### Account's Timetables - `GET /timetables`- **AUTH REQUIRED**

This route returns back a list of timetables created by the **authorized account**.

```json
{
  "data": [
    {
      "id": 1,
      "name": "Timetable Example Name",
      "items": [
        {
          "id": 986,
          "crn": "11116",
          "section": "A",
          "instructor": "Leila Chinaei",
          "credit": "0.5",
          "type": "Lecture",
          "term": "Winter 2025 (January-April)",
          "days": "Mon,Wed",
          "startTime": "10:05",
          "endTime": "11:25",
          "additionalRegistrationRequirements": "",
          "url": "https://central.carleton.ca/prod/bwysched.p_display_course?wsea_code=EXT&term_code=202510&disp=22184566&crn=11116",
          "description": "Section Type - IN-PERSON SECTION.For Arts & Social Science students only. See also fall term.Laptop required for all first year COMP courses.See https://carleton.ca/scs/scs-laptop-requirement/.Precludes additional credit for COMP 1004 (no longeroffered). This course cannot be taken for credit bystudents in Business, Engineering, Computer Science,Mathematics or Science.",
          "courseId": 1291,
          "course": {
            "id": 1291,
            "subjectCode": "COMP",
            "courseCode": "1001",
            "title": "Introduction to Computational Thinking for Arts and Social Science Students",
            "shortTitle": "Computing for Arts Students",
            "description": "An introduction to computational thinking and its applications to the arts and social sciences.  Students will gain computational thinking skills by exploring data representation, basic programming concepts, a selection of algorithms, and advanced usage of software packages for the arts and social sciences.   Precludes additional credit for COMP 1004 (no longer offered).  This course cannot be taken for credit by students in Business, Engineering, Computer Science, Mathematics or Science."
          }
        },
        ...
      ]
    },
  ],
  "error": null
}
```

### Create Timetable - `POST timetables` - **AUTH REQUIRED**

This route is used to create a new timetable associated with the authorized account.

Example Payload:

```json
{
  "name": "Example Timetable Name",
  "scheduledEventIds": [
    "986",
    "987"
  ]
}
```

### View Timetable - `GET /timetables/:id`- **AUTH REQUIRED**

This route is used to view a timetable created by the authorized account.

```json
{
  "data": {
    "id": 3,
    "name": "Example Timetable name",
    "items": [
      {
        "id": 986,
        "crn": "11116",
        "section": "A",
        "instructor": "Leila Chinaei",
        "credit": "0.5",
        "type": "Lecture",
        "term": "Winter 2025 (January-April)",
        "days": "Mon,Wed",
        "startTime": "10:05",
        "endTime": "11:25",
        "additionalRegistrationRequirements": "",
        "url": "https://central.carleton.ca/prod/bwysched.p_display_course?wsea_code=EXT&term_code=202510&disp=22184566&crn=11116",
        "description": "Section Type - IN-PERSON SECTION.For Arts & Social Science students only. See also fall term.Laptop required for all first year COMP courses.See https://carleton.ca/scs/scs-laptop-requirement/.Precludes additional credit for COMP 1004 (no longeroffered). This course cannot be taken for credit bystudents in Business, Engineering, Computer Science,Mathematics or Science.",
        "courseId": 1291,
        "course": {
          "id": 1291,
          "subjectCode": "COMP",
          "courseCode": "1001",
          "title": "Introduction to Computational Thinking for Arts and Social Science Students",
          "shortTitle": "Computing for Arts Students",
          "description": "An introduction to computational thinking and its applications to the arts and social sciences.  Students will gain computational thinking skills by exploring data representation, basic programming concepts, a selection of algorithms, and advanced usage of software packages for the arts and social sciences.   Precludes additional credit for COMP 1004 (no longer offered).  This course cannot be taken for credit by students in Business, Engineering, Computer Science, Mathematics or Science."
        }
      },
      ...
    ]
  },
  "error": null
}
```

## Database Schema

This application is powered by a relational database with the following schema.

The schema can be viewed in detail within the Prisma Schema file located at:  
`service/src/db/schema.prisma`

![Prisma Entity-Relationship Diagram](assets/prisma-erd.svg)

### Account

The `Account` model represents a user in the system. Each account has a unique email and password and can have one or more associated timetables.

- **id**: Unique identifier for the account.
- **email**: Email address for the account (unique).
- **password**: Password for the account.
- **role**: Role of the user in the system (e.g., admin, user).
- **createdAt**: Timestamp indicating when the account was created.
- **updatedAt**: Timestamp automatically updated when the account information changes.
- **timetables**: A one-to-many relationship with the `Timetable` model.

### Course

The `Course` model represents a course offering, including details such as its subject code, title, and description. Each course can have multiple scheduled events.

- **id**: Unique identifier for the course.
- **subjectCode**: Subject code for the course (e.g., COMP).
- **courseCode**: Course number (e.g., 1405).
- **title**: Full course title.
- **shortTitle**: Abbreviated course title.
- **description**: Detailed description of the course.
- **createdAt**: Timestamp indicating when the course was created.
- **updatedAt**: Timestamp automatically updated when the course information changes.
- **scheduledEvents**: A one-to-many relationship with the `ScheduledEvent` model.

### Scheduled Event

The `ScheduledEvent` model represents an offering of a course section, including details like the instructor, schedule, and location. Each scheduled event is linked to a course and can have multiple timetable events.

- **id**: Unique identifier for the scheduled event.
- **crn**: Course Reference Number (unique).
- **section**: Section identifier for the event (e.g., A01).
- **instructor**: Instructor name.
- **credit**: Credit value of the course.
- **type**: Type of event (e.g., Lecture, Lab).
- **term**: Term during which the event is offered.
- **days**: Days of the week when the event occurs.
- **startTime**: Start time of the event.
- **endTime**: End time of the event.
- **additionalRegistrationRequirements**: Additional requirements for enrollment.
- **url**: URL for the event's details.
- **description**: Description of the event.
- **courseId**: Foreign key linking the event to a course.
- **course**: Many-to-one relationship with the `Course` model.
- **createdAt**: Timestamp indicating when the event was created.
- **updatedAt**: Timestamp automatically updated when the event information changes.
- **timetableEvents**: A one-to-many relationship with the `TimetableEvent` model.

### Timetable

The `Timetable` model represents a user's schedule, which includes multiple timetable events associated with different scheduled events.

- **id**: Unique identifier for the timetable.
- **name**: User-defined name for the timetable.
- **accountId**: Foreign key linking the timetable to an account.
- **account**: Many-to-one relationship with the `Account` model.
- **createdAt**: Timestamp indicating when the timetable was created.
- **updatedAt**: Timestamp automatically updated when the timetable information changes.
- **timetableEvents**: A one-to-many relationship with the `TimetableEvent` model.

### Timetable Event

The `TimetableEvent` model represents the association of a scheduled event with a timetable. This allows users to add scheduled events to their personal timetables.

- **id**: Unique identifier for the timetable event.
- **scheduledEventId**: Foreign key linking the event to a scheduled event.
- **scheduledEvent**: Many-to-one relationship with the `ScheduledEvent` model.
- **timetableId**: Foreign key linking the event to a timetable.
- **timetable**: Many-to-one relationship with the `Timetable` model.
- **createdAt**: Timestamp indicating when the timetable event was created.
- **updatedAt**: Timestamp automatically updated when the timetable event information changes.
