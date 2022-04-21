### Project Title:
  MDT-Training-Tracker

### Authored By:
  Rebels

### Overview:
  A Single-Page Application built with React on the front end, and knex/express on the backend. The application is designed for Mission Defense Teams (MDTs) across the Space Force (USSF) to aid them in accurately tracking operator training.

### Table Of Contents:
  * Sign-In
  * Operator
  * Crews
    * Create Crew
  * Trainer
    * Assign Tasks
  * Back-shop
    * Manage Users
      * Create User
    * Manage Modules
      * Create Module
    * Manage Crews
      * Create Crew
* Approval Authority


### Description:
  USSF MDTs currently require their operators to complete various training modules across a long span of time. The continuous training effort is necessary for operators to stay up-to-date on the latest technologies, techniques, and tactics our adversaries use to steal safeguarded information. Additionally, it provides them with the skills they need in order to accomplish the mission: Defending our networks.

  With all of this training, comes the difficulty to manage personnel records on which modules and tasks they have accomplished and/or have yet to accomplish. Our MDT-Training-Tracker app aims to solve this frustration! Inside, you'll find a basic user sign-in page. Here, operators will authenticate with the system to gain access to their specific training data, and the program will apply higher-level permissions to the account (if applicable). Operators each have their own modules overview in which they can view all of the modules and tasks assigned to them. If an operator also happens to be identified as a trainer, they will have access to a page that allows them to assign tasks to their trainees. This same case is true for those operators who happen to be members of the training back-shop. These operators will have access to edit the list of users, modules, tasks, and crews in the system. Above this permission level, is the approval authority. This individual will have the sole permissions to approve new training modules being added into or removed from the database. Lastly, application users will have access to the crews page in which they will find a list of the crews that currently exist within that Mission Defense Team. Each user is assigned to a crew upon having a profile creation.

### Dependencies:
  * Front-End:
    * React
    * React Router
    * MUI: Box, Button, TextField, DataGrid, FormControl, FormControlLabel
  * Back-End:
    * Knex
    * Express
  * Dev-Dependencies:
    * React Testing Library
    * Jest
    * Cypress
    * SuperTest

    *** run npm install ***

### Usage:

  Our training app is designed for MDTs. Thus, proper usage will primarily revolve around the specific unit's MDT. Ideally, operators will be assigned permissions similar to the outdated, hard-to-use TBA program. An approval authority (ie. Director of Operations) will need to be designated. Similarly, members of the training back-shop (ie. Unit Training Manager) will need to be allocated those permissions to enable those individuals to act as the system administrators. Trainers (ie. Supervisors) will also be designated in the system.

    * Operators - View/Complete all required modules/tasks
    * Trainers - View/Assign tasks to trainee operators
    * Back-shop - Manage modules, users, and crews.
    * Approval Authority - Approve or deny changes to the training modules.

  Once all permission-levels are properly assigned, units and their Mission Defense Teams will be capable of managing their training data -- in a better way.

### Related Projects:
  https://github.com/chrlfshr/mdt-training-tracker-server <br>
  https://github.com/chrlfshr/mdt-training-tracker-client

### Team Members:
  * Charles Fisher - Team Leader
  * Nathan Johnston - Architecture Owner
  * Andrew Gorospe - Dev Team Member
  * Kyle Horne - Dev Team Member

# Mission Defense Team Training Tracker Server

## Overview:
This project contains an Express API Server that is intended to serve as a backend for a MDT Training Tracker application. When connected to a PostgreSQL database and a front end, this application has the necessary end points to create, read, update, and delete data entries regarding the many aspects that go into managing and tracking the training status of operators in a MDT.

## Table of Contents:
1. [Overview](#overview)
2. [Details](#details)
3. [Installation](#installation)
4. [Usage](#usage)

## Details:
This server is designed to manage several parts of the training tracking pipeline for a group of operators, to include:
1. Individual Users
2. Groups of Users on Crews
3. Training Assignments
4. Groups of Training Assignments/Modules
5. Logging the Training Revision/Review Process

Through the different API endpoints, these different sets of information are tracked, as well as their relationships to each other. To go into more detail, the previous entities track the following data:

### Users:
- Name
- Rank
- Username
- Assigned Crew
- Supervisor Status
- Training Management Status
- Training Approver Status

### Training Tasks:
- Task Title
- Task Description
- Directions to access content/register for course/get placed on waitlist


### Training Modules:
- Module Title
- Operator Level module is intended for
- Approval Status of module

### Training Revision:
- Tracks named sets of revisions
- Includes sufficient fields for in-depth descriptions and justifications for training alterations
- Tracks approval status from unit approver

Together these different entities and their relations allow units to track training for their operators all in one place with a streamlined and easy to use system.


## Installation:
**Note:** This project depends on having Node.JS and NPM on your workstation, as well as access to a PostgreSQL database.
1. Download this project to your workstation using your method of choice.
2. Navigate to the location of the project and run `npm install` to download install the project's software dependencies.
3. Open the `knexfile.js` with your preferred editor and fill in the appropriate fields with your PostgreSQL access information.
4. Run the command `npm run` to start the Express API. The server will log to the console the port it is running on, and you may make all API calls to your workstation's address, through that port.

## Usage:

### Users:
User records can be accessed through the `/users/` endpoint with the following options:
- `/users/`
    - GET to receive all users
    - POST to add a new user
- `/users/<id>/` - Address user record by user id
    - GET, PUT, PATCH, & DELETE functionality
- `/users/<id>/modules/` - Access modules assigned to user
    - GET to receieve all assigned modules
    - POST to append a new assigned module
- `/users/<id>/modules/<module_id>` - Access a specific module assigned to a user
    - PUT, PATCH to update the assigned module
    - DELETE to unassign the module
- `/users/account/<username>/` - Address user record by username
    - GET to recieve user information
- `/users/account/<username>/overview/` - Returns all information relevant to the user
    - GET to receieve user overview

### Crews:
Crew records can be accessed through the `/crews/` endpoint.
- `/crews/` - Access information regarding all crews
    - GET to recieve all crews
    - POST to add a new crew to database
- `/crews/<id>/` - Access information regarding a specific crew
    - GET, PUT, PATCH, DELETE functionality

### Modules:
Module records can be accessed through the `/modules/` endpoint.
- `/modules/` - Access information regarding all modules
    - GET to recieve all modules
    - POST to add new modules
- `/modules/<id>/` - Access information regarding a specific module
    - GET, PUT, PATCH, DELETE functionality

### Tasks:
Task records can be accessed through the `/tasks/` endpoint.
- `/tasks/` - Access information regarding all tasks
    - GET to receive all modules
    - POST to add new tasks
- `/tasks/<id>/` - Access information regarding specific tasks
    - GET, PUT, PATCH, DELETE functionality

### Training Modifications
Training revisions can be accessed through the `/requests/` endpoint.
- `/requests/` - Access information regarding all requests
    - GET to receieve all stored requests
    - POST to open a new request
- `/requests/<id>/` - Access information regarding a specific request
    - GET, PUT, PATCH, DELETE functionality