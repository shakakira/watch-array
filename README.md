## watch-array

Lets you subscribe to any changes made by **mutator methods** on native JavaScript arrays. 
If you're looking for a safer & complete abstraction: [new-list](http://github.com/azer/new-list)

```js
watchArray = require('watch-array')

people = ['Joe', 'Smith']

watchArray(people, function(update){ // or watchArray.once(people, function(update){

    update.add
    // => { 1: Taylor, 2: Brown }

    update.remove
    // => [0]
    
    update.sort
    // => undefined

})

people.shift()
people.push('Taylor', 'Brown')
```

## Install

```bash
$ npm install array
```

## Subscribing To Deeper Changes

You can easily define your custom type of updates and distribute them using the minimalistic pubsub interface mixed to
any array that you watch *(see [new-list](http://github.com/azer/new-list) for defining native arrays with Pub/Sub by default):*

```js
people = [{ name: 'Joe', age: 27 }, { name: 'Smith', age: 19 }]

watchArray(people, function(update){
    
  if (update.person) {

    update.index
    // => 1
    update.person
    // => { name: 'Smith', age: 20 }

  }
  
})

people[1].age = 20

people.publish({ person: people[1], index: 1 })
```

## How It Works?

* It mixes the given array with [new-pubsub](http://github.com/azer/pubsub). 
* It overrides mutable methods like `push`, `splice` etc to emit the changes.

## Caveats

Following changes won't be catched;

```js
people[people.length] = "Fred";
people[0] = "Barney";
delete people[0];
```


![](https://dl.dropboxusercontent.com/s/vg71zdk29kckx04/npmel_12.jpg)
