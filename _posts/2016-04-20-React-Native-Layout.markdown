---
layout:     post
title:      "React Native Layout"
date:       2016-04-20 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Style

#### Flexbox

```java
flexDirection:'row'|'column'

justifyContent:'flex-start'|'flex-end'|'center'|'space-between'|'space-around'

alignItems:'flex-start'|'flex-end'|'center'|'stretch'

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

