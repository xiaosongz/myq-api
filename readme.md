# myq-api

Interface with your [MyQ](https://www.liftmaster.com/for-homes/myq-connected-home?gclid=CjwKCAjw2NvLBRAjEiwAF98GMePqZknk7-vCeYlvOITPCbuuhbUBgB8XqIF61GsimwJAmjQHIZvgLRoCgSMQAvD_BwE&gclsrc=aw.ds) garage doors.

This is an updated API forked from [this repository](https://github.com/chadsmith/node-liftmaster). This module uses ES6 syntax and promises.

## Installation

```bash
npm install myq-api --save
```

or 

```bash
yarn add myq-api
```

## Usage Overview

### new MyQ(email, password)

Initialize credentials of the user.

```js
const MyQ = require('myq-api');
const garageDoor = new MyQ('email', 'password');
```

### garageDoor.login()

Logs into your MyQ account and returns your account security token. Running this function is a prerequisite to running other functions that make up this API.

```js
garageDoor.login()
  .then((token) => {

  }).catch((err) => {
    console.error(err);
  });
```

Example returned object if call is successful:
```js
{
  returnCode: 0,
  token: "2sdf99a103190zdsv13nn13"
}
```

### garageDoor.getDoors()

Returns an array of garage doors on the account.

```js
garageDoor.getDoors()
  .then((doors) => {

  }).catch((err) => {
    console.error(err);
  });
```

Example returned object if call is successful:
```js
{
  returnCode: 0,
  doors: [{
    door1
  },
  {
    door2
  }]
}
```

### garageDoor.getDoorState(id)

Retrieves the latest state of the requested door.

Door states: 1 = open, 2 = closed, 3 = stopped, 4 = opening, 5 = closing.

```js
garageDoor.getDoorState(door.id)
  .then((state) => {

  }).catch((err) => {
    console.error(err);
  });
```

Example returned object if call is successful:
```js
{
  returnCode: 0,
  state: doorState
}
```

### garageDoor.setDoorState(id, toggle)

Set the requested door to open or close. Returns a confirmation once complete. Note that the door might not be opened or closed fully by the time this function returns.

Toggles: 0 = close, 1 = open

Door states: 1 = open, 2 = closed, 3 = stopped, 4 = opening, 5 = closing.

```js
garageDoor.setDoorState(door.id, 1)
  .then((state) => {

  }).catch((err) => {
    console.error(err);
  });
```

Example returned object if call is successful:
```js
{
  returnCode: 0
}
```

## Return Codes

Each call to the API will include a return code as well as an error message if applicable. The return codes as well their correlated messages have been listed here for convenience.

| Return Code | Message                                                         |
|-------------|-----------------------------------------------------------------|
| 0           | Successful!                                                     |
| 11          | Something unexpected happened. Please wait a bit and try again. |
| 12          | MyQ service is currently down. Please wait a bit and try again. |
| 13          | User not logged in.                                             |
| 14          | Email and/or password are incorrect.                            |
| 15          | Toggle provided is not 0 or 1.                                  |
| 16          | User is locked out due to too many tries. Please go to the MyQ website and click "Forgot Password" to reset the password and gain access to the account. Note that it might take a while before being able to login through this application again - this error might keep popping up despite having unlocked the account. |

Example returned object if call is unsuccessful:
```js
{
  returnCode: 14,
  error: "Email and/or password are incorrect."
}
```

## TODO

See the [issue tracker](http://github.com/thomasmunduchira/node-liftmaster/issues) for more.

## Author

[Thomas Munduchira]() ([thomas@thomasmunduchira.com](mailto:thomas@thomasmunduchira.com))

## Original Author

[Chad Smith](http://twitter.com/chadsmith) ([chad@nospam.me](mailto:chad@nospam.me))

## License

This project is [UNLICENSED](http://unlicense.org/) and not endorsed by or affiliated with [Chamberlain](https://www.chamberlain.com/) or [LiftMaster](https://www.liftmaster.com/).
