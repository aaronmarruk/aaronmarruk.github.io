---
title:  "Getting started with React using Create React App"
date:   2018-04-12 10:18:00
description: An easy way to quick-start React projects.
---
React is a lightweight JavaScript library for building user interfaces. While the React library itself has a relatively small API footprint, the tooling required to effectively develop React applications can seem overwhelming for beginners.

That was the case until Facebook launched Create React App, which is designed to abstract some of the more complicated aspects of building React apps. 

### Getting started

> This post assumes you have Node.js, NPM and Yarn installed. If you don’t have those installed go and do that now.

Create React App is an NPM package which you install globally. Go ahead and install that first:

```
npm install -g create-react-app
```

Once that has been installed, you can check the installation using:

```
create-react-app
```

You should see output like the following, indicating `create-react-app` has been installed correctly:

```
Please specify the project directory:
  create-react-app <project-directory>

For example:
  create-react-app my-react-app

Run create-react-app --help to see all options.
```

As you can see from the output above, we can create an new project by calling `create-react-app` and providing a project name:

```
create-react-app my-react-app
```

### Project structure

Open up the project folder and take a look inside:

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

#### README.md
This is the main README file for the Create React App package. It’s a good place to find information about using the package and going beyond the basic ‘hello world’ example.

#### node_modules/
Contains all the dependancies for React (of which there are many!)

#### package.json
`package.json` contains configuration for the project. You will notice there are very few dependencies in here. This is partly due to the way the package conveniently abstracts many of the dependencies via `react-scripts` package.

#### public/
The `public` folder contains files which end up being served to the end user, such as the base HTML template.

#### src/
The `src` folder contains all the React files which will get compiled into the application. This is where you will spend most of your time as a React developer.

### Useful commands

The boilerplate also includes some useful commands for running and building the application (you can find out more about these by looking inside the `package.json` file which is included in the boilerplate project). These are:

`yarn start`
Starts the development server.

`yarn build`
Bundles the app into static files for production.

`yarn test`
Starts the test runner.

`yarn eject`
Removes this tool and copies build dependencies, configuration files and scripts into the app directory. If you do this, you can’t go back!

At this point we should be able to start the application created by `create-react-app`. 

```
yarn start
```

If all has gone to plan you should be able to open [React App](http://localhost:3000/) in your browser and see the ‘Welcome to React’ screen. Awesome!


<!-- ![start page](/assets/images/create-react-app-start-page.png) -->

And there you go. A running React application, in only a few simple steps. I'm going to leave it here for now. I just wanted to demonstrate how simple it is to get going with React. 

I've spoken to a few developer friends recently who have expressed concerns about new developers getting into React because of the supposed complicated nature of the tooling. I'm not sure this is the case any more, since Facebook have released the `create-react-app` module. Thanks for reading.