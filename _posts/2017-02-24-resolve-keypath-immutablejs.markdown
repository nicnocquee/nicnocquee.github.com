---
layout: post
title: "Universal keyPath Resolver For Immutable.js"
date: 2017-02-24T01:16:24+01:00
comments: false
---

Using [immutable.js](http://facebook.github.io/immutable-js/), we can easily read, set, and update a key on nested data.

```
var nested2 = nested.mergeDeep({a:{b:{d:6}}});
// Map { a: Map { b: Map { c: List [ 3, 4, 5 ], d: 6 } } }

nested2.getIn(['a', 'b', 'd']); // 6
```

But it does not work **only** for `Map`. We can use keypath to read or set a value even through a `List` as long as we know the index of the element.

```
const Immutable = require('immutable')

const data = {
  state: {
    users: [
      {
        id: 1,
        pets: [
          {
            kind: 'dog',
            name: 'Luffy'
          },
          {
            kind: 'cat',
            name: 'Nami'
          }
        ]
      },
      {
        id: 2,
        pets: [
          {
            kind: 'rabbit',
            name: 'Robin'
          }
        ]
      }
    ]
  }
}

const immutableData = Immutable.fromJS(data)
const namiCatName = immutableData.getIn(['state', 'users', 0, 'pets', 1, 'name'])
// Nami
```

Unfortunately we need to know in advance the index of the element we're trying to access. So I made this small helper so that I can use a function to find the index as a key.

<script src="https://gist.github.com/nicnocquee/67d44687984b4c1a3f15456ffa89ba93.js"></script>

And to read the name of the `cat` pet for user with id `1`,

```
const immutableData = Immutable.fromJS(data)
const keypath = [
  'state', 
  'users', 
  val => val.get('id') === 1, 
  'pets', 
  val => val.get('kind') === 'cat', 
  'name'
]
const namiCatName = immutableData.getIn(resolveKeyPaths(immutableData, keypath))
// Nami

const newData = immutableData.setIn(resolveKeyPaths(immutableData, keypath), 'Usopp')
/*
{
 "state": {
  "users": [
   {
    "id": 1,
    "pets": [
     {
      "kind": "dog",
      "name": "Luffy"
     },
     {
      "kind": "cat",
      "name": "Usopp"
     }
    ]
   },
   {
    "id": 2,
    "pets": [
     {
      "kind": "rabbit",
      "name": "Robin"
     }
    ]
   }
  ]
 }
}
*/
```