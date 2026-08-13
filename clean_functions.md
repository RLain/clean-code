### How do we write clean functions?

- Write small functions

- Eliminiate boolean flags

- Reads top to bottom

- Correct function naming

- Limiting parameters

- DRY

- Avoid side effects

- NO GLOBALS

### Some good heuristics

- If passing in more that two params to a function, pause and consider if it should be broken up into smaller methods.

- Have consistent naming e.g. retrieveAdminById vs getUserById. Choose one: get OR retrieve

🛠️ Clean Code: Naming and Standardization Challenge

```js
function addmessage(message) {
  const messageData = { ...message, type: "EMAIL" };

  // adds message to the DB
}

function emptyAdmin(id) {
  return { type: "Admin" };
}

function removeUserById(id) {
  // delete user
}

function deleteAdminById(id) {
  // delete admin
}
```

My proposal

```js
function createMessage(message) {
  const messageData = { ...message, type: "EMAIL" };

  // adds message to the DB
}

function returnAdmin(id) {
  return { type: "Admin" };
}

function deleteUserById(id) {
  // delete user
}

function deleteAdminById(id) {
  // delete admin
}
```

- Encapsulating conditionals

If you have two or more conditionals in a statement, it is worth considering moving them into their own method e.g.

```js
function getNonPrimaryUsers(user) {
  if (user.isActive === true && user.isPrimaryAccount === true) {
    return user.subMembers;
  } else {
    return new Error("User is not Primary Account Holder.");
  }
}

// Improved
function getNonPrimaryUsers(user) {
  if (getIsUserPrimaryActiveAccount(user)) {
    return user.subMembers;
  } else {
    return new Error("User is not Primary Account Holder.");
  }
}

function getIsUserPrimaryActiveAccount(user) {
  const isPrimaryAccount = user.isPrimaryAccount === true;
  const isActive = user.isActive === true;

  return isActive && isPrimaryAccount;
}
```

Challenge:

```js
// Clean Code: Encapsulating Conditionals Challenge
function getLoadingState(state) {
  if (!!state.user && state.loading === false && state.hasError === false) {
    return "Finished Loading";
  }

  if (
    state.user === null &&
    state.loading === true &&
    state.hasError === false
  ) {
    return "Loading...";
  }

  return "Error occured";
}

// My attempt:
function getLoadingState(state) {
  const { hasUser, isLoading, hasError } = getStateStatus(state);

  if (hasError) return "Error occured";

  if (!hasUser && isLoading) return "Loading...";

  if (!hasUser && !isLoading & !hasError)
    throw new Error("Oh no, something has gone wrong");

  return "Finished Loading";
}

function getStateStatus(state) {
  const hasError = state.hasError === true;
  const isLoading = state.loading === true;
  const hasUser = state.user !== null;

  return { hasUser, isLoading, hasError };
}

// The lecturers updates

function getLoadingState(state) {
  if (hasUserLoadedSuccesfully(state)) {
    return "Finished Loading";
  }

  if (isUserLoadingSuccesfully(state)) {
    return "Loading...";
  }

  return "Error occured";
}

function hasUserLoadedSuccesfully(state) {
  return !!state.user && state.loading === false && state.hasError === false;
}

function isUserLoadingSuccesfully(state) {
  return (
    state.user === null && state.loading === true && state.hasError === false
  );
}
```
