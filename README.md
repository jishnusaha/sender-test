# People Sorting Training System

## Project Overview

The **People Sorting Training System** is a web application designed to train civil servants of the Democratic Republic of Potatostan. The system challenges users to sort a list of people based on the number of potatoes they own, helping to improve their sorting skills.

## Features

- **Start Sorting:** Click a button to initiate the sorting challenge.
- **Input Modal:** Enter a number between 20 and 100 to generate a list of people.
- **Dynamic List Generation:** Each person has a unique number of potatoes, a random email, and a random name.
- **Drag and Drop Sorting:** Users must arrange the list from most to least potatoes.
- **Timer:** Tracks how long it takes to complete the sorting.
- **Success Modal:** Congratulations window to show score upon sorting completion

## Technologies Used

- Vue.js

## Installation

### Prerequisites

Ensure you have the following installed:

- [git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/)

### Steps To Run Development Server

```bash
# Clone the repository
git clone https://github.com/jishnusaha/sender-test.git

# Navigate to project directory
cd sender-test

# Install dependencies
npm install

# Run the development server
npm run dev
```

## Available Scripts

| Command         | Description                   |
| --------------- | ----------------------------- |
| `npm run dev`   | Runs the development server   |
| `npm run build` | Builds the app for production |

|

## Project Structure

```
├── src
│   ├── assets       # Static assets
│   ├── components   # Reusable components
│   ├── App.vue      # Root component
│   ├── main.ts      # Entry point
│   ├── libs.ts      # custom functions
│
├── public           # Static files
├── package.json     # Project dependencies
├── README.md        # Documentation
```

## Deployment

To deploy the project:

```bash
npm run build
```

The production-ready files will be available in the `dist` folder, which can be deployed to any static hosting service AWS(S3).
