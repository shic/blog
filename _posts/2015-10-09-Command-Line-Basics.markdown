---
layout:     post
title:      "Linux Command Line Basics"
subtitle:   "Some useful command lines"
date:       2015-10-09 12:00:00
author:     "Shi"
---


# Terminal 

## Search for Command history

### Ctrl+R

Type Ctrl+R at the command line and start typing the previous command. Once a result appears keep hitting Ctrl+R to see other matches. 
`!text`
This will search the history for the most recent command beginning with 'text'.

### history

`history`
Will print a list of commands along with a numeric index
`!1`
You can then execute any of these commands using their numeric index by prefacing the index with a single !

`history | grep "stuff"`
it would return something like
num stuff
then you can type
`!num`

# Linux

## Mesure exe time

### [gnomon](https://github.com/paypal/gnomon)

```
npm install -g gnomon
```

### Total time

```
java -jar ~/Downloads/transformer.jar ~/Downloads/BASE  | gnomon -t elapsed-total
```

### Each process time

```
java -jar ~/Downloads/transformer.jar ~/Downloads/BASE  | gnomon -t elapsed-line
```

#### Options

```
-t <elapsed-line|elapsed-total|absolute>

elapsed-line: Number of seconds that displayed line was the last line.
elapsed-total: Number of seconds since the start of the process.
```





## Print working directory

pwd

## Path setting

1. nano ~/.bash_profile
2. source ~/.bash_profile
3. echo $PATH 

## Search files

find ~/ -name "ImageMagick"

## 



## 



# Mac

## iTerm2

### Search

`Cmd+F`

Use the Find feature to begin searching for text.  
tab to expand the selection to the right or 
shift-tab to expand the selection to the left. 
Option-enter pastes the current match.

### Instant Replay

Cmd+Opt+B



