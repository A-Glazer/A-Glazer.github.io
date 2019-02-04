---
layout: post
title:      "What I learned from Pair Programming"
date:       2019-02-04 09:56:02 +0000
permalink:  what_i_learned_from_pair_programming
---


I just did my first pair programming lab on OO School Domain. I wasn't sure how to start it, and working on it as a pair was amazing. I was having trouble with what they wanted with roster, and by working in pairs, I saw how they approached the problem. They put roster into @roster = {} and it worked! We weren't sure how to create a statement that checks if the array contains a certain grade. I remembered using ||= method once, but I wasn't sure how to put it into effect. I copied my notes on the topic and sent it to my pairs. Together, we were able to figure out how to use ||= to make the code work! What we need to do was: 
@roster[grade] ||= []
@roster[grade] << student_name

The first line checks to see if [grade] already exists. If it does, then it goes onto the next line and adds the student_name to it. If it doesn't, it creates an empty array with it. 
I really enjoyed the group effort. It made the lab so much more understandable.
