# Project Setup as on April 2021

- Step 1 : [Create React Application](https://github.com/sharanainapurapu/react-boilerplate-project#step-1-----------------------create-react-application---------------------)
- Step 2 : [Add SCSS to your applicaiton](https://github.com/sharanainapurapu/react-boilerplate-project#step-2-----------------------add-scss-to-your-applicaiton---------------------)
- Step 3 : [Setup ESlint, Jest and Prettier](https://github.com/sharanainapurapu/react-boilerplate-project#step-3-----------------------setup-eslint-jest-and-prettier---------------------)
- Step 4 : [Set up Pre-Commit Hook](https://github.com/sharanainapurapu/react-boilerplate-project#step-4-----------------------set-up-pre-commit-hook---------------------)

------------- Optional -------------

#### If you are planning to add redux to your project

- Step 5 : [Adding Redux](https://github.com/sharanainapurapu/react-boilerplate-project#step-5-----------------------adding-redux---------------------)
- Step 6 : [Adding Thunk](https://github.com/sharanainapurapu/react-boilerplate-project#step-6-----------------------adding-thunk---------------------)
- Step 7 : [Installing useful dev modules](https://github.com/sharanainapurapu/react-boilerplate-project#step-7-----------------------installing-useful-dev-modules---------------------)

#### If you are more interested to know why you are executing above commands

- [Possible errors that I came across while setting up the project](https://github.com/sharanainapurapu/react-boilerplate-project#---------possible-errors-that-i-came-across-while-setting-up-the-project---------)
- [Annexure 1](https://github.com/sharanainapurapu/react-boilerplate-project#---------------------annexure-1---------------------)

### Step 1 : -------------------- Create React application --------------------

```sh
npx create-react-app my-app --template typescript
```

##### (or)

```sh
yarn create react-app my-app --template typescript
```

Navigate to project folder in Terminal/Command prompt for executing below commands.

### Step 2 : -------------------- Add SCSS to your applicaiton --------------------

```sh
npm i --save-dev node-sass
```

##### (or)

```sh
yarn add node-sass -D
```

Rename the App.css and index.css files to App.scss and index.scss, change the path where ever they are being imported

Please try running application using the below command to ensure everything is working fine

```sh
npm start
```

### Step 3 : -------------------- Setup ESlint Jest and Prettier --------------------

#### a) Setup ESlint

There are two ways to Install eslint

- Using direct commands (airbnb - a popular style guide, pelase read annexure 1 for more info)
- Installing the eslint globally

##### Using direct commands - Approach 1

Note, ESLint is installed with create-react-app, so you don’t need to explicitly install it. We will install the packages for Airbnb config.

```sh
yarn add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb-typescript eslint-plugin-jest`
```

##### (or)

```sh
npm i @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb-typescript eslint-plugin-jest --dev`
```

```sh
npx install-peerdeps --dev eslint-config-airbnb
```

- create .eslintrc.js in the project root folder

```sh
  module.exports = {
    extends: [
      'airbnb-typescript',
      'airbnb/hooks',
      'plugin:@typescript-eslint/recommended',
      'plugin:jest/recommended',
      'plugin:prettier/recommended'
    ],
    plugins: ['react', '@typescript-eslint', 'jest'],
    env: {
      browser: true,
      es6: true,
      jest: true,
    },
    globals: {
      Atomics: 'readonly',
      SharedArrayBuffer: 'readonly',
    },
    parser: '@typescript-eslint/parser',
    parserOptions: {
      ecmaFeatures: {
        jsx: true,
      },
      ecmaVersion: 2018,
      sourceType: 'module',
      project: './tsconfig.json',
    },
    rules: {
      'linebreak-style': 'off',
      '@typescript-eslint/explicit-module-boundary-types': 'off',
      "no-use-before-define": "off",
      "@typescript-eslint/no-use-before-define": ["error"],
      'prettier/prettier': [
        'error',
        {
          endOfLine: 'auto'
        }
      ]
    }
  };
```

##### Installing the eslint globally - Approach 2

If you want you want to follow any other design system and if you are okie to install ESlint in your system globally, you can run the following commands and it will take care of creating the eslint config file, downloading all the eslint dependencies.

```sh
npm install -g eslint
```

##### (or)

```sh
yarn global add eslint
```

```sh
eslint --init
```

You will be asked some series of questions, please find more details about it in the annexure 1. After the whole process is done you will see .eslintrc"js/json/yaml" getting generated. You might have different set of items in extends section of the file, based on what options that you are chosing during the questionare. But make sure rest of the sections match with above set of rules.

#### b) Installing Prettier and integrating Prettier with ESLint

```sh
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
```

##### (or)

```sh
npm i prettier eslint-config-prettier eslint-plugin-prettier --save-dev
```

`eslint-config-prettier` Turns off all rules that are unnecessary or might conflict with Prettier.
`eslint-plugin-prettier` Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.

#### c) Installing Jest

```sh
npm i @testing-library/react react-test-renderer jest-dom --save-dev
```

##### (or)

```sh
yarn add -D @testing-library/react react-test-renderer jest-dom
```

#### d) Final setup
Please add below piece of code to scripts section is package.json

```sh
  "scripts": {
    "format": "prettier --write src/**/*.ts{,x}",
    "lint": "tsc --noEmit && eslint src/**/*.ts{,x}",
    "lint:fix": "eslint --fix ."
  }
```

Open .eslintrc.js and add the following items into the extends and rules section

```sh
 extends: [
    "plugin:jest/recommended",
    "plugin:prettier/recommended",
  ],
```

```sh
  rules: {
    "linebreak-style": "off",
    "@typescript-eslint/explicit-module-boundary-types": "off",
    "no-use-before-define": "off",
    "@typescript-eslint/no-use-before-define": ["error"],
    "prettier/prettier": [
      "error",
      {
        endOfLine: "auto",
      },
    ],
  },
```

Try running application once again to make sure it is all running without any errors

```sh
npm start
```

### Step 4 : -------------------- Set up pre-commit hook --------------------

Husky improves your commits. You can use it to lint your commit messages, run tests, lint code, etc... when you commit or push. Husky supports all Git hooks.

```sh
npm install --save-dev husky
```

Set up the husky pre-commit hook by adding following code to our package.json

```sh
  "husky": {
    "hooks": {
      "pre-commit": "npm run lint"
    }
  }
```

### Step 5 : -------------------- Adding Redux --------------------

```sh
npm install redux react-redux
```

##### (or)

```sh
yarn add redux react-redux
```

We should install their types as development dependencies to help TypeScript understand the libraries.

```sh
npm install -D @types/redux @types/react-redux
```

### Step 6 : -------------------- Adding Thunk --------------------

```sh
npm install redux-thunk 
```

##### (or)

```sh
yarn add redux-thunk 
```

###### Okie, what is Thunk

With a plain basic Redux store, you can only do simple synchronous updates by dispatching an action. Middleware extends the store's abilities, and lets you write async logic that interacts with the store. Thunks are the recommended middleware for basic Redux side effects logic, including complex synchronous logic that needs access to the store, and simple async logic like AJAX requests.

```sh
npm install @types/redux-thunk --dev
```

##### (or)

```sh
yarn add @types/redux-thunk -D
```

### Step 7 : -------------------- Installing useful dev modules --------------------

```sh
npm install redux-devtools-extension redux-logger --dev
```

##### (or)

```sh
yarn add -D redux-devtools-extension redux-logger
```

```sh
npm i --save-dev @types/redux-logger
```

##### (or)

```sh
yarn add @types/redux-logger -D
```

The above two tools will help in logging the store and action objects when ever they are manipulated.

```sh

  import { createStore, applyMiddleware } from 'redux'
  import { composeWithDevTools } from 'redux-devtools-extension'
  import logger from 'redux-logger'
  import thunk from 'redux-thunk'

  import rootReducer from './rootReducer'

  const store = createStore(
    rootReducer,
    composeWithDevTools(applyMiddleware(logger, thunk))
  )

  export default store;

```

### -------- Possible errors that I came across while setting up the project --------

- At step 2, If you come across some error like " Couldn't find a declaration file for module 'react "

```sh
npm install @types/react
```

##### (or)

```sh
yarn add @types/react
```

That should solve your issue, while I was setting up this project that was common setup issue.

- In step 3 while creating .eslintrc.json/js, what ever style approach you are taking, make sure that is put on the top in the extends array for example

```sh
  module.exports = {
    extends: [
      'airbnb-typescript',
      'airbnb/hooks',
      'plugin:@typescript-eslint/recommended',
      'plugin:jest/recommended',
    ]
  }
```

```sh
  module.exports = {
    extends: [
      'standard',
      'plugin:@typescript-eslint/recommended',
      'plugin:jest/recommended',
    ]
  }
```

### -------------------- Annexure 1 --------------------

#### Series of questions asked while setting up the eslint in step 3, approach 2.

#### How would you like to use ESLint?

#### To check syntax only =>

it helps you correct your syntax and make sure it conform to standard.

##### To check syntax and find problems =>

to help you check for syntax correctness and also help to find any problems in your code base

##### To check syntax, find problems, and enforce code style\_ =>

to help you check for syntax, find problem and enforce style, enforcing style means to conforms to a particular coding standard such as Airbnb, Google and other Standard coding style. But I always go for the last option the one with syntax, find problems and enforce code style

#### What type of modules does your project use?

##### Javascript module (import/export) =>

if your project has babel installed then you definitely need to choose this option. If you are working on a project such as React, Vue, Angular e.t.c they all use babel so you need choose this option.

##### CommonJS (require/exports) =>

this option is meant for commonJS that has nothing to do with babel, maybe your nodejs project and any other javascript project

#### Which framework does your project use?

##### React =>

if you are using react in/for your project then this option is for you

##### Vue =>

if you are using Vue in/for your project then this option is for you

##### None of these =>

if you are using neither React or Vue in your project choose this option

#### Where does your code run?

##### Browser =>

if your project runs on browser e.g React, Angular, Vue e.t.c then go for this option

##### Node =>

if your project is a node based then gladly choose this option

#### How would you like to define a style for your project?

##### Use a popular style guide =>

- This allows you to choose from set of popular style such as Airbnb,Standard and Google style guide, it is advisable to choose this option in order for you to follow popular and most used style guide and i will be choosen this option in this post.
- Answer questions about your style: This is for custom style guide
- Inspect your JavaScript file(s).: custom style guide

Comparision between popular style guides in the market
![Image](https://miro.medium.com/max/4800/1*K51eiJl-y9IfnWFK4IcHCQ.png)

#### What format do you want your config file to be in?

##### Javascript =>

whether you want your eslint config file to be in .js file

##### YAML =>

whether you want your eslint config file to be in .yaml file

##### JSON =>

whether you want your eslint config file to be in .json file you can choose any option in this section

after you have chosen your preferred configuration file type it will then prompt you to install all necessary dependencies. after all neccessary dependencies has been successfully installed it will now generate a config file with ".eslintrc"."js/json/yaml".

What are those set of rules and extends that we added to .eslintrc.js
[extends and roles](https://eslint.org/docs/user-guide/configuring/configuration-files#extending-configuration-files) 

1. https://brygrill.medium.com/create-react-app-with-typescript-eslint-prettier-and-github-actions-f3ce6a571c97
2. https://betterprogramming.pub/comparing-the-top-three-style-guides-and-setting-them-up-with-eslint-98ea0d2fc5b7
3. https://medium.com/swlh/developer-checklist-react-application-initial-set-up-d4568799b825
