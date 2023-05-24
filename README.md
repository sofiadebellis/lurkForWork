# Vanilla JS: LurkForWork

1. Background & Motivation
2. The Task
3. 3. Getting started

## 1. Background & Motivation

Web-based applications are becoming the most common way to build a digital capability accessible to a mass audience. While there are modern tools that help us build these rapidly, it's important to understand the fundamental JavaScript-based technology and architectures that exist, both to gain a deeper understanding for when these skills may be needed, but also to simply understand the mechanics of fundamental JS. Even when working with a high level framework like ReactJS, understanding (in-concept) the code that it is transpiled to will ensure you're a more well rounded web-based engineer.

This  consists of building a **frontend** website in Vanilla JS (no ReactJS or other frameworks). This frontend will interact with a RESTful API HTTP backend that is built in JavaScript (NodeJS express server) and provided to you.

A theoretical background on how to interface with this API can be found the "promises & fetch" lecture.

The web-based application you build is required to be a single page app (SPA). Single page apps give websites an "app-like feeling", and are characterised by their use of a single full load of an initial HTML page, and then using AJAX/fetch to dynamically manipulate the DOM without ever requiring a full page reload. In this way, SPAs are generated, rendered, and updated using JavaScript. Because SPAs don’t require a user to navigate away from a page to do anything, they retain a degree of user and application state. In short, this means you will only ever have `index.html` as your HTML page, and that any sense of "moving between pages" will just be modifications of the DOM.

## 2. The Task (Frontend)

Your task is to build a frontend for a UNSW rip-off version of the popular professional social networking tool [LinkedIn](https://linkedin.com/). If you haven't used this application before, we would recommend creating your own LinkedIn profile - it's probably good for your career anyway!

UNSW's rip-off of LinkedIn is called "LurkForWork". However, you don't have to build the entire application. You only have to build the frontend. The backend is already built for you as an express server built in NodeJS (see section 3.2).

Instead of providing visuals of what the frontend (your task) should look like, we instead are providing you with a number of clear and short requirements about expected features and behaviours.

The requirements describe a series of **screens**. Screens can be popups/modals, or entire pages. The use of that language is so that you can choose how you want it to be displayed. A screen is essentially a certain state of your web-based application.

### 2.1. Milestone 1 - Registration & Login 

This focuses on the basic user interface to register and log in to the site.

#### 2.1.1. Login
 * When the user isn't logged in, the site shall present a login form that contains:
   * an email field (text)
   * a password field (password)
   * submit button to login
 * When the submit button is pressed, the form data should be sent to `POST /auth/login` to verify the credentials. If there is an error during login an appropriate error should appear on the screen.

#### 2.1.2. Registration
 * When the user isn't logged in, the login form shall provide a link/button that opens the register form. The register form will contain:
   * an email field (text)
   * a name field (text)
   * a password field (password)
   * a confirm password field (password) - not passed to the backend, but an error should be thrown on submit if it doesn't match the other password
   * submit button to register
 * When the submit button is pressed, if the two passwords don't match the user should receive an error popup. If they do match, the form data should be sent to `POST /auth/register` to verify the credentials. If there is an error during registration an appropriate error should appear on the screen.

#### 2.1.3. Error Popup
 * Whenever the frontend or backend produces an error, there shall be an error popup on the screen with a message (either a message derived from the backend error response, or one meaningfully created on the frontend).
 * This popup can be closed/removed/deleted by pressing an "x" or "close" button.

### 2.2. Milestone 2 - Basic Feed 

Milestone 2 focuses on fetching feed data from the API. A feed and it's associated content should only be accessible to logged in users.

#### 2.2.1. Basic Feed

The application should present a "feed" of user content on the home page derived `GET /job/feed`. Note that the feed will only return information from people that the logged in user is watching.

The jobs should be displayed in reverse chronological order (most recent jobs first). 

Each job should display:
1. Who the job post was made by
2. When it was posted
  * If the job was posted today (in the last 24 hours), it should display how many hours and minutes ago it was posted
  * If the job was posted more than 24 hours ago, it should just display the date DD/MM/YYYY that it was posted
3. The job content itself. The job content includes the following:
  * An image to describe the job (jpg in base64 format)
  * A title for the new job (just as a string)
  * A starting date for the job (just as a string)
  * How many likes it has (or none)
  * The job description text
  * How many comments the job post has

### 2.3. Milestone 3 - Advanced Feed
 
Milestone 3 focuses on a richer UX and will require some backend interaction.

#### 2.3.1. Show likes on a job
* Allow a user to see a list of all users who have liked a job. In terms of how it is displayed, consider your preferred user experience approach out of the following 3 options:
  * The list of names is visible on each job in the feed by default
  * The list of names is visible on a job in the feed if a show/hide toggle is clicked (hidden by default).
  * The list of names is visible in a popup, modal, or new screen, when a button/link is clicked on the feed.

#### 2.3.2. Show comments on a job
* Allow a user to see a list of all the comments on the job. Each comment should contain at minimum the user's name and their comment. In terms of how it is displayed, consider your preferred user experience approach out of the following 3 options:
  * The list of names and comments are visible on each job in the feed by default
  * The list of names and comments are visible on a job in the feed if a show/hide toggle is clicked (hidden by default).
  * The list of names and comments are visible in a popup, modal, or new screen, when a button/link is clicked on the feed.

#### 2.3.3. Liking a job
* A user can like a job on their feed and trigger a api request (`PUT /job/like`)
* For this milestone, it's OK if the like doesn't appear/update until the page is refreshed.

#### 2.3.4. Feed Pagination
* Users can page between sets of results in the feed using the position token with (`GET /job/feed`).
* Note: You will automatically receive marks for this section if you end up implementing the infinite scroll alternative in a later milestone.

### 2.4. Milestone 4 - Other users & profiles

Milestone 4 focuses predominately on user profiles and how users interact with them.

#### 2.4.1. Viewing others' profiles
* Let a user click on a user's name from a job, like, or comment, and be taken to a profile screen for that user.
* The profile screen should contain any information the backend provides for that particular user ID via (`GET /user`).
* The profile should also display all jobs made by that person. You are not required to show likes and/or comments for each job here.
* The profile should also display somewhere all other users this profile is watched by (information via `GET /user`). This should consist of a list of names (which for each name links to another profile), as well as a count somewhere on the page that shows the total number of users they are watched by.

#### 2.4.2. Viewing your own profile
* Users can view their own profile as if they would any other user's profile
* A link to the users profile (via text or small icon) should be visible somewhere common on most screens (at the very least on the feed screen) when logged in.

#### 2.4.3. Updating your profile
* Users can update their own personal profile via (`PUT /user`). This allows them to update their:
  * Email address
  * Password
  * Name
  * Image

#### 2.4.4. Watching / Unwatching
* Watching on user profiles:
  * When a logged in user is visiting another user's profile page, a button should exist that allows them to "watch" the other user (via `PUT user/watch`).
  * If the logged in user already watches this person, an unwatch button should exist.
* Somewhere on the feed screen a button should also exist that prompts the enter to enter an email address in a popup. When entered, the email address is sent to `PUT /user/watch` to watch that particular user.

### 2.5. Milestone 5 - Adding & updating content 

Milestone 5 focuses on addition and removing both content and comments.

#### 2.5.1. Adding a job
* Users can upload and job new content from a modal, component, or seperate screen via (`POST /job`)
* How users open this component, modal, or separate screen can be found in a single or multiple places, and should be easily and clearly accessible.

#### 2.5.2. Updating & deleting a job
* Let a user update a job they made or delete it via (`DELETE /job`) or (`PUT /job`).

#### 2.5.3. Leaving comments
* Users can write comments on "jobs" via (`POST /job/comment`)

### 2.6. Milestone 6 - Challenge Components (`advanced`)

#### 2.6.1. Infinite Scroll
* Instead of pagination, users an infinitely scroll through results. For infinite scroll to be properly implemented you need to progressively load jobs as you scroll. 

## 3. Getting started

### 3.1. The Frontend

Stub code has been provided to help you get started in:
 * `frontend/index.html`
 * `frontend/styles/global.css`
 * `frontend/src/helpers.js`
 * `frontend/src/main.js`

To work with your frontend code locally with the web server, you may have to run another web server to serve the frontend's static files.

To do this, run the following command once on your machine:

`$ npm install --global http-server`

Then whenever you want to start your server, run the following in your project's root folder:

`$ npx http-server frontend -c 1 -p [port]`

Where `[port]` is the port you want to run the server on (e.g. `8080`). Any number is fine.

This will start up a second HTTP server where if you navigate to `http://localhost:8000` (or whatever URL/port it provides) it will run your `index.html` without any CORs issues.

### 3.2. The Backend

The backend server exists in your individual repository. After you clone this repo, you must run `yarn install` in `backend` directory once.

To run the backend server, simply run `yarn start` in the `backend` directory. This will start the backend.

To view the API interface for the backend you can navigate to the base URL of the backend (e.g. `http://localhost:5005`). This will list all of the HTTP routes that you can interact with.

Your backend is persistent in terms of data storage. That means the data will remain even after your express server process stops running. If you want to reset the data in the backend to the original starting state, you can run `yarn reset` in the backend directory. If you want to make a copy of the backend data (e.g. for a backup) then simply copy `database.json`. If you want to start with an empty database, you can run `yarn clear` in the backend directory.

Once the backend has started, you can view the API documentation by navigating to `http://localhost:[port]` in a web browser.

The port that the backend runs on (and that the frontend can use) is specified in `frontend/src/config.js`. You can change the port in this file. This file exists so that your frontend knows what port to use when talking to the backend.

Please note: If you manually update database.json you will need to restart your server.

Please note: You CANNOT modify the backend source code for bonus marks.
