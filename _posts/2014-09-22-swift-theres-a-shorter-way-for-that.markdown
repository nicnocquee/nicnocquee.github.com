---
layout: post
title: "Swift: There's a shorter way for that"
date: 2014-09-22 09:40:52 +0900
categories: [ios]
---

Backward sorting array of string using Swift:

<!--more-->

```objc
	let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
	func backwards(s1: String, s2: String) -> Bool {
	    return s1 > s2
	}
	var reversed = sorted(names, backwards)
```

Too long.

```objc
	reversed = sorted(names, { (s1: String, s2: String) -> Bool in
    		return s1 > s2
    })
```

Let's make it one line.

```objc
	reversed = sorted(names, { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```
	
Don't be satisfied yet.

```objc
	reversed = sorted(names, { s1, s2 in return s1 > s2 } )
```
	
You didn't think that's the best we can do, right?

```objc
	reversed = sorted(names, { s1, s2 in s1 > s2 } )
```
	
Shorter!

```objc
	reversed = sorted(names, { $0 > $1 } )	
```
	
You can do it!

```objc
	reversed = sorted(names, >)
```

Use the force!

```objc
	😄=sorted(🐷,>)
```
	
There! We have the winner! Oh, if you see two rectangles on the code above, use Safari or  Firefox, please :)