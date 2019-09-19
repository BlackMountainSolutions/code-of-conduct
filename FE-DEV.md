# BlackMountain

The following points are **mandatory** for all PRs/changes sent 
for our own products and specially for our own clients.
PRs/changes not following these rules won’t be accepted.
Read them carefully and daily since they may change.
Keep these rules close to you since they will help you to write better
and cleaner code; they will help you stand out in quality and prevent many errors. 
Do not allow your code to have flaws or be of low quality, 
that’s not the way we do things here. DO NOT allow you to 
give less than what you can really deliver



## Index
- [Names](#names)
- [Numbers](#numbers)
- [Always handle exceptions](#always-handle-exceptions)
- [Safely dealing with values](#safely-dealing-with-values)
- [Components](#components)
- [Functions with one purpose](#functions-with-one-purpose)
- [Indentation / code-style](#indentation--code-style)
- [Do not abuse inlining](#do-not-abuse-inlining)
- [Linters / warnings](#-linters--warnings)
- [Read the documentation](#-read-the-documentation)
- [Cleaning ourselves up](#-cleaning-ourselves-up)
- [Conclusion](#%EF%B8%8F-conclusion)
- [Contributing to this document](#-contributing-to-this-document)



## Names
Use descriptive names for your variables, methods and functions

#### ❌ DO NOT
```js
const x = userAge() < 18;
```

#### ✔️ DO
```js
const legalAge = 18;
const canVote = userAge() < legalAge;
```

#### 💡 WHY
Descriptive names are essential to any good code, 
they allow programmers to read and understand code more easily

[Go to index](#index)


## Numbers
Treat any math operation as if the result could be NaN

#### ❌ DO NOT
```js
const groupsCount = getUsersCount() / getUsersGroupCount();
```

#### ✔️ DO
```js
const usersCount = getUsersCount();
const usersGroupCount = getUsersGroupCount();
const groupsCount = (usersCount / usersGroupCount) || 0;
```

#### 💡 WHY
Printing or dealing with NaN always result in invalid or 
unwanted results. Be relentlessly with NaN, DO NOT allow it in your code

[Go to index](#index)


## Always handle exceptions
Any operation that can throw an exception must be handled properly. 
Remember, exceptions is just another operation that must be deal 
with, otherwise our code is INCOMPLETE

#### ❌ DO NOT
```js
const parsedJson = JSON.parse(...);
```

#### ✔️ DO
```js
try {
    const parsedJson = JSON.parse(...);
} catch (e) {
    const parsedJson = {};
}
```

#### 💡 WHY
Handling exceptions must be part of your logic. Imagine having 
logic to deal with an operation when it goes as expected but have 
nothing when it fails, ALWAYS HANDLE ALL YOUR CASES

[Go to index](#index)


## Safely dealing with values
Remember, any value in Javascript can be anything, DO NOT 
think you’re dealing with the correct one, ALWAYS make 
use of Lodash to prevent incorrect cases

#### ❌ DO NOT
```js
function hasBankAccounts(bankAccounts) {
    return bankAccounts.length > 0;
}
```

#### ✔️ DO
```js
import 'isEmpty' from 'lodash';
function hasBankAccounts(bankAccounts) {
    return isEmpty(bankAccounts);
}
```

#### 💡 WHY
Lodash is a great library that handles all the incorrect cases
for us, make great use of it. If in doubt, use Lodash, do
not perform these validations yourself, they’re already written in the library

[Go to index](#index)


## Components
Create small and simple components that deal with one thing,
and only ONE thing at a time. Think in terms of lego-blocks, allow
them to be easily reusable and DO NOT make big components

#### ❌ DO NOT
```js
export default class MyComponent extends React.Component {
    buildUserNameField = () => <div>...</div>;
    buildUserNameValidation = () => <div>...</div>;
    buildPasswordField = () => <div>...</div>;
    isPasswordValid = () => ...
}
```

#### ✔️ DO
```js
import * as helper from '...';
export default class MyComponent extends React.Component {
    buildUserNameField = () => <UserNameField ... />
    buildPasswordField = () => <PasswordField ... />;
    isPasswordValid = () => helpers.isPasswordValid(...);
}
```

#### 💡 WHY
Building components that do many things are hard to read,
maintain and reuse. Be smart about it, create as many
components as you want in order to not repeat ourselves

[Go to index](#index)


## Functions with one purpose
Write small and simple functions that do one thing well, and only one thing

#### ❌ DO NOT
```js
function isPasswordValid(password) {
    createUser(); // Creating a user even tho the function name says it's validating a password?
    logUserOut();
    return password.length > 5;
}
```

#### ✔️ DO
```js
import 'size' from 'lodash/size';
function isPasswordValid(password) {
    const minCharsForPassword = 5;
    return size(password) > minCharsForPassword;
}
```

#### 💡 WHY
Creating small and simple functions allow programmers to easily read and re-use code

[Go to index](#index)


## Indentation / code style
Be organized when writing code, place spaces and make your code clean and
always follow the code style used in each specific project

#### ❌ DO NOT
```js
function foo() {
    const x = 42
 const y
    = 33;
    bar(33,y,  x);
}
```

#### ✔️ DO
```js
function foo() {
    const x = 42;
    const y = 33;
    bar(33, y, x);
}
```

#### 💡 WHY
This is a very notorious detail that help the code to be
more readable and show the type of programmers we are

[Go to index](#index)


## Do not abuse inlining
DO NOT abuse inlining

#### ❌ DO NOT
```js
const x = map(filter(users, (user) => user.age > 18), 'name');
```

#### ✔️ DO
```js
const filterUsersWhoCanVote = (users) => {
    const ageToVote = 18;
    return filter(users, (user) => {
        const userAge = Number(get(user, 'age')) || 0;
        return userAge > ageToVote;
    });
}

const usersWhoCanVote = filterUsersWhoCanVote(users);
const nameOfUsersWhoCanVote = map(usersWhoCanVote, 'name');
```

#### 💡 WHY
Abusing inline makes code harder to read and isn’t
reusable, DO NOT do it, if in doubt, create a new function

[Go to index](#index)


## 🔎 Linters / warnings
Always make sure your code throws no warnings or errors. Linters
are excellent tools that prevent us from shooting ourselves in the foot,
be smart about it, use them and take advantage of their suggestions!

[Go to index](#index)


## 📋 Read the documentation
Always make sure to read the documentation of any component
or library we’re using to come up with the best possible solution.
DO NOT fix anything by forcing it or by pure luck

[Go to index](#index)


## 👍 Cleaning ourselves up
Apply the boy scouts rule, “Always leave the campground cleaner than you found it.”.
Every time you see code it can be improved and the
change isn’t big, DO IT, clean it up!

[Go to index](#index)


## ❤️ Conclusion
These rules are what define us as programmers and as a team, we do not
allow bad or low quality to represent us, that is not who I am nor the team I
want to be involved with. Be relentlessly and do not allow poor
results to represent you as a programmer

[Go to index](#index)


## 😺 Contributing to this document
The point of this document it to promote best and good practices
for coding. Is anything missing? please go ahead and suggest
it so we can add it and thus, improve as a team. Thanks!

> ___The best idea and implementation should always win___
>
> Mark Zuckerberg

[Go to index](#index)
