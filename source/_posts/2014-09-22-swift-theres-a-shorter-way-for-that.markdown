---
layout: post
title: "Swift: There's a shorter way for that"
date: 2014-09-22 09:40:52 +0900
categories: [ios]
---

Backward sorting array of string using Swift:

<!--more-->

	let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

	func backwards(s1: String, s2: String) -> Bool {
	    return s1 > s2
	}
	var reversed = sorted(names, backwards)

Too long.

	reversed = sorted(names, { (s1: String, s2: String) -> Bool in
    	return s1 > s2
    })

Let's make it one line.

	reversed = sorted(names, { (s1: String, s2: String) -> Bool in return s1 > s2 } )
	
Don't be satisfied yet.

	reversed = sorted(names, { s1, s2 in return s1 > s2 } )
	
You didn't think that's the best we can do, right?

	reversed = sorted(names, { s1, s2 in s1 > s2 } )
	
Shorter!

	reversed = sorted(names, { $0 > $1 } )	
	
You can do it!

	reversed = sorted(names, >)

Use the force!

	😄=sorted(🐷,>)
	
There! We have the winner!