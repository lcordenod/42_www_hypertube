# Hypertube

Creating a Netflix-like web app to search and stream movies using BitTorrent protocol

## Intro

Objective of this project is to create a complete streaming website that allow users to search and watch movies using BitTorrent protocol

Team of 3: Raphaël ([GitHub](https://github.com/M4sterCiel)), Martin ([GitHub](https://github.com/Scaglia3000)) and I.

See Trello board [here](https://trello.com/b/wteA4xno/42-hypertube)

### Stack

- Node JS (Express)
- React JS (w/ Hooks and Contexts APIs)
- Materialize CSS and Material UI Front libraries
- MongoDB w/ Mongoose
- JSON web tokens
- Axios for API requests
- Passport for OAuth
- torrent-stream for streaming
- ffmpeg for video conversion

### Features

Hypertube project handles:

- User creation and authentication using tokens and sessions
- OAuthentication via Twitter, Google, Facebook and 42
- User profile with basic information, profile picture, movies seen as well as users following
- User profile edition (password, details, preferences)
- App fully available in 3 languages (French, English and Spanish)
- Movies suggestions by rating (w/ movies seen identified on page)
- Movies search by name, filters (release year, rating) and sorted (rating, release year, genre, name...)
- Movie pages with details on cast, summary, duration and torrents, quality, sources available
- Movies streaming with multiple qualities available (720p/1080p)
- Movies subtitles available in up to 3 languages (French, English, Spanish)
- Movie format conversion (to webm) while downloading movie for browser support
- Default player functionalities including download and PiP
- Smart movie download checks to avoid downloading same movie again and help with streaming speed
- Movies downloaded deletion after one month
- Email notifications for authentication and password reset (with auth key)
- Change and reset of email/forgot password with ID validation
- Profile, pictures deletion and user DB cleanup
- Responsive design from mobile to desktop/tablet
- User input and upload checks (front/backend)
- Password hashing (Whirlpool)
- HTML/Javascript/SQL injections prevention

Discover more details below.

## User account

### User creation and authentication

User input has been secured on front and back end with immediate feedback for front end input validation. Also password security has been taken seriously with multiple layers of complexity validated on the go, including:

- A lowercase letter
- A uppercase letter
- A number
- A minimum of 8 characters

Password will be hashed (sha512) with a salt for 5 iterations first before being saved in the DB.

// SCREENSHOT HERE

Before saving user, several checks will also be runned in the background, including:

- Verifying if user already exists
- Verifying if email is already used
- Verifying (as said earlier) if input is in the right format required

Once user is created, he will be receive an email to verify his account, while account isn't validated, he wont be able to access the app (a message will be displayed to inform him).

### Forgot and change of password

If user has forgotten his password, he will be able to reset it using his email or username, a link will be sent to his email address.

The reset of password link will have a unique ID, which will be the latest link sent, others will be made deprecated. This provides security to prevent intruders from resetting someone else password.

### User profile

User profiles are accessible via the `/user/username` url, so this means that each user has his own profile link and can share it. Also if user is on his own profile, he will be able to edit it, while if he is on someone else profile, he can follow that user.

// SCREENSHOT HERE

#### Information edition

User can edit his profile information after his account creation, he can edit:

- Firstname
- Lastname
- Username
- Email (private, hidden from profile)

If he edits his username, he will be redirected seamlessly to his new profile url.

// SCREENSHOT HERE

##### Profile picture

User will necessarily have a profile picture, he sets it on registration and can edit after logging in.

##### Movies seen

Users can retrieve their movies seen on their profile page, they can also what other profiles viewed. Once a movie is view, it will be automatically added to its movies seen list (no refresh needed).

##### Following

Users can also follow each other in order to retrieve easily profiles that they like or want to store on their profile. This will also be shown in a "Following" category on profiles following others, if following no one, the category won't be shown until someone is followed.

Users can also unfollow users so that these profiles no longer appear in their following section on their profile.

#### Edit email and password

User is able to modify his email and password from the account settings modal, password will be hashed.

#### Delete account

User is able to delete his account as well, this will remove him from database and other users no longer will be available to see his profile, nor following him.

## Movies search

### Display list

// SCREENSHOT HERE

Once registered and logged, users will be able to search for movies on the platform. By default, they will get a list of suggestions of movies based on the best ratings.

#### Search terms

User is able to search a movie by entering completely or partly the name of the movie. If movies match his search term, a list will be returned to him ordered by default of the sorting he picked.

##### Filters

User can also refine its search by selecting filters:

- Range of release years
- Range of ratings

##### Sort

Additionally, he can sort the results:

- Default (rating)
- Name
- Release date
