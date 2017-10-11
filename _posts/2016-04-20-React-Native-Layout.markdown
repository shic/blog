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



## Flexbox

How to position child element in parent (defined in the parent component )

```java
//default the element is placed at top left 
//flexDirection default rule is 'column',  justifyContent is used more often

flexDirection:'column'
//vertical direction
justifyContent:'flex-start'|'flex-end'|'center'|'space-between'|'space-around' 
//horizontal direction (left-right)
alignItems:'flex-start'|'flex-end'|'center'|'stretch'

flexDirection:'row'
//horizontal direction (left-right)
justifyContent:'flex-start'|'flex-end'|'center'|'space-between'|'space-around' 
//vertical direction
alignItems:'flex-start'|'flex-end'|'center'|'stretch'


//aligns itself in parent
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

### Common properties

```
width: 100,
height: 100,

marginLeft:5,
marginRight:5,
marginTop:10,
marginBottom:1,
padding:2,

backgroundColor: 'red'

//The item will occupy all the parent space
flex:1,
alignSelf:'stretch' //alignSelf aligns itself, alignItems aligns the children.

```



### View

```
flexDirection:'column'
justifyContent: 'space-around',

shadowColor: '#000',
shadowOffset: {width:0, height:2} //width:0 means no shadow on the left,right side, height:2 means vertical 2 pixel
shadowOpacity: 0.2 //how heavy is the shadow from 0--1
shadowRadius: 2, //shadowRadius should have the save value of borderRadius, otherwith the shadow will be out of border
elevation: 2,
position: 'relative',

borderWidth:1,
borderRadius:2,
borderColor:'#ddd',
borderBottomWidth:0,

flexDirection: 'row',
borderColor: '#ddd',
position: 'relative',

```



## Text

```
fontSize: 16
fontWeight: '600'
```



## TextInput

By default it has no width and height

```
width:100
height:10


```



```javascript
state = {email:''};
render(){
    return(
    	<TextInput
      		autoCorrect={false}
     		placeholder='example@gmail.com'
          	secureTextEntry={true} //if the value is true, we can just pass 'secureTextEntry'
      		value={this.state.email}
      		onChangeText = {text=>this.setState({email:text})}
		   style = {{width:100, height:20}}
           
        />
    )
}

//Make a Input component

const input=({lable,placeholder,value,onChangeText,secureTextEntry})=>{
  return(
    <View>
      <Text>{lable}</Text>
      <TextInput
      		autoCorrect={false}
    		secureTextEntry={secureTextEntry} 
     		placeholder={placeholderText}
      		value={value}
      		onChangeText = {onChangeText}
		   style = {{width:100, height:20}}
           
      />
    </View>
  )
    
}
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

## Image

```
    //The following code defines the fix height and match parent width
    imageStyle:{
        flex:1,
        width:null,
        height:300,
    },
```

### TouchableOpacity

```
    <TouchableOpacity onPress={this._onPressButton}>
      <Image
        source={require('./myButton.png')}
      />
    </TouchableOpacity>
```



## FlatList

In parent view add `flex:1` to make the list fill the screen



## Picker

```
<Picker
	style = {{flex:1}}
/>
//Picker has with and height 0. So add a style to show the picker 
```

