---
layout:     post
title:      "React Native Layout"
date:       2016-04-20 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Style

## Usage

```javascript
  <View style={styles.viewStyle}>
  	<Text style={styles.textStyle}>Some text</Text>
  </View>



//To not duplicate the styles var, we can do the following
constant {textStyle,viewStyle} = styles;

return(
  <View style={viewStyle}>
  	<Text style={textStyle}>Some text</Text>
  </View>


)

const styles={
  textStyle:{
    fontSize:20
  }
  viewStyle:{
    backgroundColor:20
  }
}
```



#### Flexbox

How to position child element in parent (defined in the parent component )

```java
//default is top left 
  
flexDirection:'row'|'column'

//horizontal direction (left-right)
alignItems:'flex-start'|'flex-end'|'center'|'stretch'

//vertical direction
justifyContent:'flex-start'|'flex-end'|'center'|'space-between'|'space-around' 

alignSelf:'auto'|'flex-start'|'flex-end'|'center'|'stretch'

flexWrap:'wrap'|'nowrap'
```

#### absolute

```java
  box1: {
    position: 'absolute',
    top: 40,
    left: 40,
    width: 100,
    height: 100,
    backgroundColor: 'red'
    transform: [{'translate': [0,0, 1]}]
    borderRadius: 20,

  }
```

#### Base Style

```html

// BaseStyles.js
import {  StyleSheet,Dimensions } from 'react-native';
let winSize = Dimensions.get('window');
const BaseStyles = StyleSheet.create({
  text: {
    fontSize: 40/winSize.scale
  }
});
export default BaseStyles;

// Component
import BaseStyles from './BaseStyles';

class InheritanceStyle extends Component {
  render() {
    return (
      <View style={this.props.parentColor}>
        <Text style={[BaseStyles.text, styles.text]}> this is a long text </Text>
      </View>
    );
  }
}
const styles = StyleSheet.create({
  text:{
    color: '#ffffff'
  }
});
```


#### absolute

```java

```

## Components

## View

```java
alignItems: 'center',
justifyContent: 'center',
shadowColor: '#000',
shadowOffset: {width:0, height:2} //width:0 means no shadow on the left,right side, height:2 means vertical 2 pixel
shadowOpacity: 0.2 //how heavy is the shadow
elevation: 2,
position: 'relative'
```



## Text

```
fontSize:20
```



### TouchableHighlight

```java
class Touch extends Component {
  handlePress(){
    console.log('press');
  }
  handleLongPress(){
    console.log('longPress');
  }
  render() {
    return (
      <TouchableHighlight
        onPress={this.handlePress}
        onLongPress={this.handleLongPress}>
        <View>
          <Text>Press me!</Text>
        </View>
      </TouchableHighlight>
    );
  }
}
```

### TextInput

```java
class Test extends Component {
  //...
  //handle events
  //...
  render() {
    return (
      <TextInput 
        onBlur={...}
        onChange={...}
        onEndEditing={...}
        onSelectionChange={...}
        onSubmitEditing={...}
      </TextInput>
    );
  }
}
```

### [Gesture Responder System](https://unbug.gitbooks.io/react-native-training/content/24_events.html)

```java
 render() {
    return (
      <View 
        onStartShouldSetResponderCapture={this.handleStartShouldSetResponderCapture}
        onMoveShouldSetResponderCapture={this.handleMoveShouldSetResponderCapture}
        onStartShouldSetResponder={this.handleStartShouldSetResponder}
        onMoveShouldSetResponder={this.handleMoveShouldSetResponder}
        onResponderGrant={this.handleResponderGrant} 
        onResponderReject={this.handleResponderReject}
        onResponderMove={this.handleResponderMove}
        onResponderRelease={this.handleResponderRelease}
        onResponderTerminationRequest={this.handleResponderTerminationRequest}
        onResponderTerminate={this.handleResponderTerminate}>
          <Text>Press me!</Text>
      </View>
    );
  }
```

