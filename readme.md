## ThinkUp Tech - Frontend Code Challenge

So, sounds like you're interested in working for ThinkUp Technologies. We think that's awesome! But before we go any further in the process, let's make sure that your coding chops are up to par with what we need for this role. Don't worry, you can take as much time as you need to complete this code challenge.

### Overview

Your primary goal in this code challenge is to build an SPA (_single page application_) that allows users to login and manage a collection of video games. Your SPA must consume a RESTful API which we provide for you and is documented further down. 

You can build your SPA with any frontend language, library or framework that you want.

##### Feature requirements

Your SPA must have the following pages:
- Login page
  - Should accept an email and password.
  - Reject invalid login attempts.
- Games index page
  - Landing page after login.
  - Should display a table of all games in the system.
  - Should have an input for real time search to filter the list of games
    - Use `GET /api/games?filter[search]=text` to have the API perform the search for you.
- Game specific page
  - Page dedicated to displaying details about one individual game.
  - Users should also be able to update the game on this page as well.
- Game create page
  - Page with a form to add a new game to the system.

##### Development requirements
- SPA must be responsive, scale accordingly from desktops all the way down to mobile devices.
- SPA needs to handle user authentication (login, logout, protected routes, etc.)
- Write tests for your web application using Jest, Ava or any testing framework that you prefer.
- Commit all of your code to a personal public repository on GitHub or GitLab.

##### Things to consider

Although not required, the following might help you get this code challenge done faster:

- Use a well known JavaScript library such as Vue, React or Angular. (_Vue.js preferred_)
- Pair your chosen library with a framework. (_Vue / Nuxt.js_) (_React / Next.js_)
- Use a CSS framework such as Bootstrap, Bulma or Tailwind.

##### Things to remember
- If you get stuck, that's okay. We are primarily looking at how you write your code and how you solve problems.
- Quality over quantity.

#### Video Game API Documentation

The RESTful Video Game API can be accessed at http://161.35.15.14/api/

##### Headers

All calls to the API must have the following headers:
```
Accept: application/json
Content-Type: application/json
```

##### Authentication

Endpoints that require authentication will need to be consumed with the corresponding user's access token. You can get a user's token by hitting the "Create token" endpoint documented below. Once you have a token, you will need to send it as a bearer token in your request header:
```
Authorization: Bearer TOKEN_HERE
```

##### Tokens

###### Create token
`POST /api/tokens`

Example payload:
```
{
  "email": "john.smith@example.com",
  "password": "secret-apple"
}
```

Example response `200`:
```
{
  "token": "1|GGHHNNLzix2xCVgJgpkc772H8acSxvDg6GqQ6KGc"
}
```

###### Revoke token
`DELETE /api/tokens` - _Requires authentication_

Example payload:
```
{}
```

Example response `204`:
```
{}
```

##### Users

###### Current user
`GET /api/users/me` - _Requires authentication_

Example payload:
```
{}
```

Example response `200`:
```
{
  "id": 1,
  "name": "John Smith",
  "email": "john@example.test"
}
```

###### List users
`GET /api/users` - _Requires authentication_

Example payload:
```
{}
```

Example response `200`:
```
{
  "current_page": 1,
  "data": [
    {
      "id": 1,
      "name": "John Smith",
      "email": "john@example.test"
    },
    {
      "id": 2,
      "name": "Jane Doe",
      "email": "jane@example.test"
    },
    {
      "id": 3,
      "name": "Sally Sue",
      ...
```

##### Games

###### List games
`GET /api/games` - _Requires authentication_

Example payload:
```
{}
```

Example response `200`:
```
{
  "current_page": 1,
  "data": [
    {
      "id": 1,
      "name": "Grand Theft Auto V",
      "box_art_url": "https:\/\/static-cdn.jtvnw.net\/ttv-boxart\/Grand%20Theft%20Auto%20V-{width}x{height}.jpg",
      "description": null,
      "created_at": "2021-04-26T22:45:48.000000Z",
      "updated_at": "2021-04-26T22:45:48.000000Z"
    },
    {
      "id": 2,
      "name": "Fortnite",
      "box_art_url": "https:\/\/static-cdn.jtvnw.net\/ttv-boxart\/Fortnite-{width}x{height}.jpg",
      "description": "Adipisci autem unde quos culpa nisi rem est. Iure earum in eos et porro dolor.",
      "created_at": "2021-04-26T22:45:48.000000Z",
      "updated_at": "2021-04-26T22:45:48.000000Z"
    },
    {
      "id": 3,
      "name": "Call of Duty: Warzone",
      ...
```

**Notes:**
- Use `/api/games?filter[search]=text` to search for specific games.

###### Show game
`GET /api/games/{id}` - _Requires authentication_

Example payload:
```
{}
```

Example response `200`:
```
{
  "id": 1,
  "name": "Grand Theft Auto V",
  "box_art_url": "https:\/\/static-cdn.jtvnw.net\/ttv-boxart\/Grand%20Theft%20Auto%20V-{width}x{height}.jpg",
  "description": null,
  "created_at": "2021-04-26T22:45:48.000000Z",
  "updated_at": "2021-04-26T22:45:48.000000Z"
}
```

###### Create game
`POST /api/games` - _Requires authentication_

Example payload:
```
{
  "name": "Valheim",
  "box_art_url": "https://static-cdn.jtvnw.net/ttv-boxart/Valheim.jpg",
  "description": "Valheim is an upcoming survival and sandbox video game by the Swedish developer Iron Gate Studio."
}
```

Example response `201`:
```
{
  "name": "Valheim",
  "box_art_url": "https:\/\/static-cdn.jtvnw.net\/ttv-boxart\/Valheim.jpg",
  "description": "Valheim is an upcoming survival and sandbox video game by the Swedish developer Iron Gate Studio.",
  "updated_at": "2021-04-26T23:05:47.000000Z",
  "created_at": "2021-04-26T23:05:47.000000Z",
  "id": 23
}
```

###### Update game
`PUT /api/games/{id}` - _Requires authentication_

Example payload:
```
{
  "description": "Lorem ipsum dolor..."
}
```

Example response `200`:
```
{
  "id": 18,
  "name": "Chess",
  "box_art_url": "https:\/\/static-cdn.jtvnw.net\/ttv-boxart\/Chess-{width}x{height}.jpg",
  "description": "Lorem ipsum dolor...",
  "created_at": "2021-04-26T22:45:48.000000Z",
  "updated_at": "2021-04-26T23:07:29.000000Z"
}
```

###### Delete game
`DELETE /api/games/{id}` - _Requires authentication_

Example payload:
```
{}
```

Example response `204`:
```
{}
```
