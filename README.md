# Spotify App Example

## What is this project?
This application was made for a student of mine that is currently taking my open-source development course.
The student wanted to practice their web dev and design UI/UX skills through modifying the code of an existing site, and was specifically
interested in finding a project that utilizes the Spotify API so that they could rearrange and restyle things to their liking.
However, every relevant project the student could find out there had red flag after red flag that made them not a great starting point, so I made this project for them to use as a base.

This project is intentionally very simple and minimally styled. The main purpose of this project was to setup Spotify oAuth so my aforementioned student (and future students)
can expand on this project in any direction they please.

## How was this project made?
I used Vue and the [Spotify API](https://developer.spotify.com/documentation/web-api/).

## How to run this project?
I recommend opening this project up in Visual Studio Code.

Create a copy of the `.env.sample` file, and rename it to `.env`. 

There are two variables defined in the `.env` file that the app requires. 

The `REDIRECT_URI` environment variable is already provided for you if running this website locally.
In the Spotify Developer console, set the Redirect URI to the same value as the `REDIRECT_URI` environment variable.

The `CLIENT_ID` variable comes from an "application" that is registered to your Spotify account.
To get these values, go to Spotify's developer portal [here](https://developer.spotify.com/dashboard), login with your Spotify account credentials,
and then hit the `Create an App` button. 
The fields for "App name" and "App description" can be anything.
After the app has been created, click it and find the app's Client ID.

Copy those values and paste these values into the `.env` file in the appropriate places.

Next, open up a terminal (such as the one that's built into Visual Studio Code), navigate to the root project folder, and run `npm run serve`.
Once the web app has finished building successfully, open up a web browser (such as Google Chrome) and go to the address `localhost:8080`.
If all went well, you will see this site's home page.

## How to use the website?
The home page of this site has a button that will allow you to login to Spotify.
From there, the app can now use your account's context to perform API requests.
The Playlists page shows an example of this by pulling all of the logged in user's playlist data.

## Spotify API Resources
The documentation for Spotify's API resources can be found [here](https://developer.spotify.com/documentation/web-api/reference/#/).
