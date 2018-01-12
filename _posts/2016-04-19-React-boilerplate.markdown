---
layout:     post
title:      "React Boilerplate"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# React-boilerplate

# Setting up

1. npm i
2. npm start 
3. You can then open [http://localhost:3000](http://localhost:3000/) to access the server and see your app.

# Learning Path 

[Introduction](https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/general/introduction.md)

[Redux saga](https://app.pluralsight.com/library/courses/redux-saga)

## Structure

### `app/`

We use the [container/component architecture](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.4rmjqneiw). `containers/` contains React components which are connected to the redux store. `components/` contains dumb React components which depend on containers for data. **Container components care about how things work, while components care about how things look.**

#### `components/`

Presentation components, it receives props and provides updated JSX. It is ignorant of the redux world.

If you want to handle click action, pass handler as a param.   

#### `containsers/`

Have access to the redux world (redux state and actions), so they will pass **state** to the presentation components throught **props**,  and they make actions available to the presentation components. These components can then trigger actions and render properly. The presentation components are totally unaware of the redux world. 



### `server/`

As the name suggests, this folder contains development and production server configuration.

### 





# Lib

# styled-components


```
npm install --save styled-components
```



## Style properties

```


justify-content: space-between; // space-around

// To use flex direction, you must specify 'display: flex'
display: flex;
flex-direction: row; //column

align-items: center;

text-align: center;

overflow-y: auto; // Scroll inner list item

background: papayawhip;

padding: 3em 0;


  font-size: 18px;
```



#### Width/Height

```
width: 10em; // 100%; 50px;
max-width: calc(1280px + 16px * 2);
height: 30em;
max-height: 30em;
min-height: 100%;
```

#### Border

```Css
border-top: 0;
border-left: 0;
border-right: 0;
border-bottom-color: rgba(0, 0, 0, 0.2);
border-bottom-width: 1px;
border-bottom-style: solid;
```



## Style insied component

```java
import styled from 'styled-components';

const AppWrapper = styled.div`
  max-width: calc(1280px + 16px * 2);
  margin: 0 auto;
  display: flex;
  min-height: 100%;
  padding: 0 16px;
  flex-direction: column;
`;

export class SlotPage extends React.PureComponent { 
	
  render() {
    return (
    	<AppWrapper>
        </AppWrapper>
  );
  
}
```



## Child to be vertical

```
// To use flex direction, you must specify 'display: flex'
display: flex;
flex-direction: column;
```



## Dinamic 

```
color: ${props => props.primary ? 'white' : 'palevioletred'};
width: ${(props) => props.size ? props.size : '10em'};

// If vertical then add 'flex-direction: column;' property
${(props) => props.vertical && 'flex-direction: column;'}

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



### Colors List

https://github.com/styled-components/polished/blob/master/src/internalHelpers/_nameToHex.js





https://www.youtube.com/watch?time_continue=805&v=bIK2NwoK9xk

# Reselect

Reselect is a library used for slicing your redux state and providing only the relevant sub-tree to a react component. 

Selectors can compute derived data, allowing Redux to store the minimal possible state.

It has three key features:

1. Computational power

   While performing a search operation, reselect will filter the original array and return only matching usernames. Redux state does not have to store a separate array of filtered usernames.

2. Memoization

   A selector will not compute a new result unless one of its arguments change. 

3. Composability

   You can combine multiple selectors. 

   For example, one selector can filter usernames according to a search key and another selector can filter the already filtered array according to gender. 













# **Middleware**

Middlewares are third party libraries which intercept each redux action dispatched to the redux store and then... do stuff. 

For example,  [`redux-logger`](https://github.com/evgenyrodionov/redux-logger) middleware will listen to all the actions being dispatched to the store and print previous and next state in the browser console. It's helpful to track what happens in your app.

#### **Router middleware:**

Keeps your routes in sync with the redux `store`

#### Redux Saga

Background process that handles multiple actions simultaneously, communicates with redux store and react containers at the same time





# Redux Saga

It got access to all the actions that being dispatched, and it can intercept it to execute logic.



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





# Immutable

Make a new copy every time you do a change. It returns a whole new copy of state. 

Problem 1: TypeError: someState.toJS is not a function

Solution: your state is not ImmutableJS object.

https://redux.js.org/docs/recipes/UsingImmutableJS.html

# CSS Modules

It ensure that CSS is properly namespaced. 

```
<Img className = {styles.logo}
```

It will go and create a unique string for you automatically, so you can worry a bit less about clashes in CSS

# PostCSS





# Notes

https://app.pluralsight.com/library/courses/react-boilerplate-building-scalable-apps



[PluralSight boilerplate repo](https://github.com/hendrikswan/react-boilerplate)

