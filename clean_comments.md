## What are GOOD comments?

- Short & concise
- Add value
- Clarifies code that has business purpose but looks out of sort
- Warning of ampliciation or importance
- Legal comments

## What are BAD comments?

- When they are undeeded
- Used to explain bad code
- Need to be maintained and may mislead
- TODOs

## Example:

```js
// gets all longest strings
function longestString(inputArray) {
  // initialize the longest string to first value
  let length = inputArray[0].length;

  for (let i = 1; i < inputArray.length; i++) {
    // checks if current string is longer than current longest
    if (length < inputArray[i].length) {
      length = inputArray[i].length;
    }
  }

  // filters out any values not equal to the longest string
  const strs = inputArray.filter((word) => word.length === length);

  return strs;
}

// compared with:
function getLongestStrings(inputArray) {
  let longestString = inputArray[0].length;

  for (let i = 1; i < inputArray.length; i++) {
    let currentString = inputArray[i].length;
    if (longestString < currentString) {
      longestString = currentString;
    }
  }

  const longestWords = inputArray.filter(
    (word) => word.length === longestString,
  );

  return longestWords;
}
```

Other things to avoid

- Version control comments
- Commented out code

```js
// version control / log comments

/**
 * 2018-07-04 Removed Character Limit - Dylan Israel
 */

// remove commented code
function getUserName(firstName, middleName, lastName) {
  // const initials = `${firstName[0]}{MidName[0]}${lastName[0]};
  return `${firstName} ${middleName} ${lastName}`;
}
```

- Visual markers: Unecessary (rather move stuff to different files)

```js
/****************************
 * DEPENDENCIES
 ***************************/

/////////////////////////
// USER CLASS
/////////////////////////
class User {
  /////////////////////////
  // PROPERTIES
  /////////////////////////
  firstName;
  middleName;
  lastName;
}

/****************************
 * ADMIN CLASS
 ***************************/
class AdminUser extends User {
  constructor() {}
}
```
