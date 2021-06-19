# IoT Parking Lot Project - VP-Dibris Smart Parking

## Project Description

To **design a parking lot system** with ability to find:

- Cars registration numbers

- Check car registration numbers of all with particular color

- Parking slot where car is parked with reference to registration number

- Parked cars with color reference

[![Parking Lot](./assets/logo.png)]

## Pre requisite requirements to run the project

The source code for this project is written using [Node.js](https://nodejs.org/). Make sure you have [Node.js](https://nodejs.org/) installed on your computer before running this application, **if not please install Node.js from [here](https://nodejs.org/en/download/)**.

To check if you have Node.js and NPM installed by running simple commands to see what version of each is installed:

> **Note:** [Node installer](https://nodejs.org/en/download/) installs both Node.js and npm on your system.

 - **Test Node.js**: To see if Node is installed, type `node -v` in Terminal. This should print the version number so you’ll see something like this `v16.3.0`.

 - **Test NPM**. To see if NPM is installed, type `npm -v` in Terminal. This should print the version number so you’ll see something like this `7.16.0`.


## To run this project

This is a console application written in `Node.js`. This can be run in two modes:

1. **Interactive Mode**: An interactive terminal based shell where commands can be typed in to perform different actions.

2. **File Mode**: It accepts a filename as a parameter at the terminal and read the commands from that file.

### Quick Start

**Proceed to the steps below only if you've `Node.js` installed.** If not, please refer [pre requisites](#pre-requisites) section.

#### For Interactive Mode

Open terminal and navigate (`cd`) to this folder and type the following commands:

```bash
1. npm install (It will install all the npm files fron the folder)
2. npm start (start the npm)
```

#### To close the terminal
Ctrl+z  and then enter Y to exit

#### For File Mode

Open terminal and type `node src/index.js data/input.txt`.

```terminal
node src/index.js <path_to_file.txt>
```

**Note**: You can find a few sample input files inside `data/` folder.

#### Explained

**STEP 1**: `npm install` or `npm i` will download all the dependencies defined in `package.json` file and generate a `node_modules/` folder with the installed modules. Learn more [here](https://docs.npmjs.com/cli/install).

**STEP 2**: `npm start` or `npm run start` will start the application. It is equivalent to `node src/index.js`

#### Console Application

Navigate to `bin/` folder and open `parking_lot` with double click. It'll open a terminal where different [commands](#list-of-user-commands) can be typed in.
You may face permission related issues, please allow opening applications from unauthorized developers as it's blocked due to security reasons.

## List of User Commands

Users can interact with the Parking Lot system via a following simple set of commands which produce a specific output:

- **create_parking_lot**: `create_parking_lot 10` will create a parking lot with 10 slots.

- **park < REGISTRATION NUMBER > < COLOR >**: `park AA-123-AA White` will allocate the nearest slot from entry gate.

- **leave**: `leave 3` will make slot number 4 free.

- **status**: `status` will display cars and their slot details

```bash
Slot No.  Registration No Color
1         PP-651-PP  White
2         PP-826-AA  Red
3         PP-912-DD  White
5         AA-019-GG  Black
6         AA-412-HH  Black
```

- **registration_numbers_for_cars_with_colour < COLOR >**: `registration_numbers_for_cars_with_colour White` will display the registration number of the cars of white color e.g. `PP-651-PP, PP-912-DD`

- **slot_numbers_for_cars_with_colour < COLOR >**: `slot_numbers_for_cars_with_colour White` will display slot numbers of the cars of white color e.g. `1, 3`

- **slot_number_for_registration_number < REGISTRATION NUMBER >**: `slot_number_for_registration_number AA-723-HH` will display the slot number for the car with registration number AA-723-HH.

- **leave_car_by_registration_number**: `leave_car_by_registration_number GG-923-AA` will free the slot occupied by car with registration number GG-923-AA.

- **available_slot_numbers**: `available_slot_numbers` will display available slot numbers e.g. 2, 6, 8.

- **allocated_slot_numbers**: `allocated_slot_numbers` will display occupied slot numbers e.g. 1, 3, 4, 5, 7.

- **exit**: `exit` will quit the application and return to the console.

> **NOTE: Any commands which are not mentioned above will throw an error: `<INPUT> is an invalid command`**

**To view all the commands in terminal, please run `npm run help`**

## Modules - OOPS Approach

There are two classes defined:

`ParkingLot()`: It is the main class which is used to initialize a parking lot. In each parking lot there is maximum number of slots and an array of slots that will be occupied by the car. It has following methods:

- `createParkingLot(input)` : Creates a parking lot with given input. It throws an error `Minimum one slot is required to create parking slot` if zero or negative number (n <= 0) is provided as an input.

- `parkCar(input)` : Allocates nearest slot from entry gate to the car. It can throw following errors:

    - `Minimum one slot is required to create parking slot` : When parking lot is not initialized.

    - `Sorry, parking lot is full` : When parking lot has reached its maximum capacity.

    - `Please provide registration number and color both` : When input contains either of two i.e. registration number and color of the car, not both.

- `leaveCar(input)` : Removes car in given slot in parking lot. It throws following errors:

  - `Parking lot is empty` if parking lot is empty.

  - `Slot number <SLOT NUMBER> is not found` when slot number is absent.

  - `Slot number <SLOT NUMBER> is already free` when slot number is not occupied.

- `leaveCarByCarNumber (input)` : Makes the slot free for car of given registration number.

- `getParkingStatus()` : Returns an array containing slot number, registration number and color. It throws an error `Sorry, parking lot is empty` if parking lot is empty.

- `getCarsWithSameColor(input)` : Returns a comma separated string containing registration numbers of cars with same color e.g. `AA-351-HH, GG-927-AA, AA-172-AA`.

- `getSlotsWithSameColorCar(input)` : Returns a comma separated string containing slot numbers of car with same color e.g. `3, 5, 6`.

- `getSlotByCarNumber(input)` : Finds slot number of car for given registration number. It returns `Not found` when car is not present.

- `findNearestAvailableSlot()` : Finds nearest free slot.

- `findAllAvailableSlots()` : returns a comma separated string of free parking slots e.g. 1, 4, 7. It returns `null` if parking lot is not created.

- `findAllAllocatedSlots()` : returns a comma separated string of allocated parking slots e.g. 2, 3, 5, 6. It returns `null` if parking lot is not created.

`Car()`

- `new Car(NUMBER, COLOR)` : Constructor used to initialize a car object containing two fields, registration number and color.

- `isCarEqual()` : Checks whether two cars are equal or not.

**Note:** *Here we made an assumption that the registration number for two cars can never be same.*

## Test Scripts

Tests are written using [Mocha](https://mochajs.org/) and can be run using `npm test`

- `npm run test-unit` : Run unit tests only (Tests for functions in Parking Class)
- `npm run test-system` : Run repository tests only (See [this](#system-tests) section)
- `npm run test-lint` : Run lint tests using ESLint
- `npm run test` : Run all tests (lint tests + unit tests + system tests)

#### Unit tests

Unit tests are written for the methods of `ParkingLot` class.

#### System tests

System tests mainly include repository structure tests. It tests for the following:

Repository must contain:

- `package.json`
- `README.md`
- `.gitignore`
- `.eslintrc`
- `npm/` folder
- `src/` folder
- `tests/` folder

`package.json`

- must have valid name, author and license
- must have proper keywords
- must have valid version string
- must have scripts definitions
- must point to precise version for dependencies
- should not overlap dependencies
- must have devDependencies

`.gitignore` must contain `build/`, `dist/`, `out/`, `node_modules/` folders.

#### Lint tests

`npm run test-lint` is used to run JavaScript lint tests. It detects the coding style issues. ESLint rules are defined in `.eslintrc.js` file.

`node_modules/eslint/bin/eslint.js --fix src/` can be run to fix lint errors.

#### Code Coverage

To see code coverage report, run `npm run test`.

The current code coverage for the tests are following:

| Type  | Percentage  |
|---|---|
| Statement  | 91.48  |
| Branch  | 69.57  |
| Function  | 89.53  |
| Lines  | 91.25  |

- **Function coverage:** Has each function (or subroutine) in the program been called?
- **Statement coverage:** Has each statement in the program been executed?
- **Branch coverage:** Has each branch (also called DD-path) of each control structure (such as in if and case statements) been executed?
- **Line coverage:** Has each executable line in the source file been executed?


**NOTE:** Code coverage is added to the mocha tests (`npm run test`) using **[nyc](https://www.npmjs.com/package/nyc)**.
You can see the code-coverage report in terminal as well as detailed HTML report inside `coverage/` folder.
Go to `coverage/` folder and open `index.html`.

## Build Script

`npm run build` will build the executable(console application) inside `bin/` folder which can be opened by double clicking on it.
Make sure you've already done with `npm install`, if not, please install dependencies first. Please refer [this](#explained) section for the same.

> Note: [pkg](https://www.npmjs.com/package/pkg) is used to package the Node.js application into an executable. Learn more [here](https://www.npmjs.com/package/pkg).

## Documentation

> Writing code is easy but maintaining isn’t? One can read one's code but it's difficult for others to read.
With this spirit, I've added [JSDoc](https://www.npmjs.com/package/jsdoc) comments in code.

Go to `out/` folder and open `global.html`. You'll find the documentation for the source code there.

**To generates the docs locally**, open terminal and run `npm run create-docs`.

## Dependencies Used


- [Mocha](https://mochajs.org/): A JavaScript test framework for Node.js programs. Learn more [here](https://mochajs.org/).

- [Chai](https://www.chaijs.com/): A BDD/TDD assertion library for Node.js and it can be paired with any JS testing framework. Learn more [here](https://www.chaijs.com/).

- [nyc](https://www.npmjs.com/package/nyc): A JS code coverage tool extensively tested with Mocha for measuring code coverage. Learn more [here](https://istanbul.js.org/docs/tutorials/mocha/).

- [Chalk](https://www.npmjs.com/package/chalk): A npm module used to style terminal string. Learn more [here](https://www.npmjs.com/package/chalk).

- [ESLint](https://eslint.org/): A static code analysis tool for identifying problematic patterns found in JavaScript code. It covers both code quality and coding style issues. Learn more [here](https://eslint.org/).

- [pkg](https://www.npmjs.com/package/pkg): It is used to package a Node.js project into an executable that can be run even on devices without Node.js installed. Learn more [here](https://www.npmjs.com/package/pkg).

- [JSDoc](https://www.npmjs.com/package/jsdoc): An open source API documentation generator for Javascript. It allows developers to document their code through comments. It is supported only for Node.js versions > `v8.15.0`. Learn more [here](https://devdocs.io/jsdoc/).

## Screenshots

Please go to `screenshots/` folder to find screenshots of running **Parking Lot** console application. 
> **Click [here]) to view e2e working demo video.**

## TL; DR

Here's the **few commands** for you!

Open terminal and type the following:

1. `cd parking_lot` : Navigates to the `parking_lot` root folder.

2. `npm install` : Installs all the dependencies.

3. `npm run start` : Starts the console application in interactive mode.

4. `npm run test` : Runs all the tests.

5. `npm run test-unit` : Runs all the unit tests.

6. `npm run test-system` : Runs system tests.

7. `npm run test-lint` : Runs lint test.

8. `npm run build` : Builds the application in `bin/` directory.

9. `npm run create-docs` : Creates documentation inside `out/` folder.

10. `npm run help` : Displays all supported user commands.

11. `node src/index.js data/input.txt` : Runs the application in file mode.

-----------

```javascript

  _____ _                 _     __   __          
 |_   _| |__   __ _ _ __ | | __ \ \ / /__  _   _ 
   | | | '_ \ / _` | '_ \| |/ /  \ V / _ \| | | |
   | | | | | | (_| | | | |   <    | | (_) | |_| |
   |_| |_| |_|\__,_|_| |_|_|\_\   |_|\___/ \__,_|
                                                 

```

-----------