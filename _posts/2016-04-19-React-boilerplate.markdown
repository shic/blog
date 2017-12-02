---
layout:     post
title:      "React Boilerplate"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# React-boilerplate

## Setting

1. npm i
2. npm start 
3. You can then open [http://localhost:3000](http://localhost:3000/) to access the server and see your app.

## Learning 

[Introduction](https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/general/introduction.md)

### `app/`

We use the [container/component architecture](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.4rmjqneiw). `containers/` contains React components which are connected to the redux store. `components/` contains dumb React components which depend on containers for data. **Container components care about how things work, while components care about how things look.**

### `server/`

As the name suggests, this folder contains development and production server configuration.



# Lib

## styled-components

```
npm install --save styled-components
```

### styled.

##### View

Generic

##### Text

text

##### H1

H1 text



### Flow for styled-components

```
npm i -g flow-typed # if you do not already have flow-typed
flow-typed install styled-components@<version>
```



https://www.styled-components.com/docs/api



### Text

```Java
import styled from 'styled-components';

// Create a Title component that'll render an <h1> tag with some styles
const Title = styled.h1`
	font-size: 1.5em;
	text-align: center;
	color: palevioletred;
`;

// Create a Wrapper component that'll render a <section> tag with some styles
const Wrapper = styled.section`
	padding: 4em;
	background: papayawhip;
`;

// Use Title and Wrapper like any other React component – except they're styled!
render(
	<Wrapper>
		<Title>
			Hello World, this is my first styled component!
		</Title>
	</Wrapper>
);
```



### Button

Pass props

```
const Button = styled.button`
	/* Adapt the colours based on primary prop */
	background: ${props => props.primary ? 'palevioletred' : 'white'};
	color: ${props => props.primary ? 'white' : 'palevioletred'};

	font-size: 1em;
	margin: 1em;
	padding: 0.25em 1em;
	border: 2px solid palevioletred;
	border-radius: 3px;
`;

render(
	<div>
		<Button>Normal</Button>
		<Button primary>Primary</Button>
	</div>
);
```



### Theme

```
// Define our button, but with the use of props.theme this time
const Button = styled.button`
	font-size: 1em;
	margin: 1em;
	padding: 0.25em 1em;
	border-radius: 3px;

	/* Color the border and text with theme.main */
	color: ${props => props.theme.main};
	border: 2px solid ${props => props.theme.main};
`;

// We're passing a default theme for Buttons that aren't wrapped in the ThemeProvider
Button.defaultProps = {
	theme: {
		main: 'palevioletred'
	}
}

// Define what props.theme will look like
const theme = {
	main: 'mediumseagreen'
};

render(
	<div>
		<Button>Normal</Button>

		<ThemeProvider theme={theme}>
			<Button>Themed</Button>
		</ThemeProvider>
	</div>
);

```



https://www.youtube.com/watch?time_continue=805&v=bIK2NwoK9xk

## Reselect

Reselect is a library used for slicing your redux state and providing only the relevant sub-tree to a react component. It has three key features:

1. Computational power

   While performing a search operation, reselect will filter the original array and return only matching usernames. Redux state does not have to store a separate array of filtered usernames.

2. Memoization

   A selector will not compute a new result unless one of its arguments change. 

3. Composability

   You can combine multiple selectors. For example, one selector can filter usernames according to a search key and another selector can filter the already filtered array according to gender. 



## **Middleware**

Middlewares are third party libraries which intercept each redux action dispatched to the redux store and then... do stuff. 

For example,  [`redux-logger`](https://github.com/evgenyrodionov/redux-logger) middleware will listen to all the actions being dispatched to the store and print previous and next state in the browser console. It's helpful to track what happens in your app.

#### **Router middleware:**

Keeps your routes in sync with the redux `store`

#### Redux Saga

Background process that handles multiple actions simultaneously, communicates with redux store and react containers at the same time





## Redux Saga



```
export const GET_FLIGHT = 'GET_FLIGHT'
import {put, take, call} from 'redux-saga/effects';

const fetchFlights = () => {
  return fetch('https://get-flights.json')
  .then((response) => response.json())
  .then((responseJson) => {
    return responseJson;
  })
};
export function* getFlight() {
  try {
    yield take(GET_FLIGHT);
    const flights = yield call(fetchFlights); //1
    yield put({type: 'FLIGHTS_LOADED', flights}); //2
  } catch(error) {
    yield put({type: 'FLIGHTS_LOADED_FAILED', error});
  }
}
```

 Notice how there is a **yield** before every step, it essentially means:

 the middleware stops/suspends the saga from moving on to the next step until the current step is done.