# Chapter1 Code Should Be Easy to Understand

- The Fundamental Theorem of Readability

Code should be written to minimize the time it would take for someone else to understand it.

- Smaller is not always better.

Having fewer lines of code is a good goal, but

minimizing the time-till-understanding is an even better goal.

---

**Surface-Level Improvement**

---

# Chaoter2 Packing Infomation into Names

**key idea: Packing information into your names**

1. Choosing specific words

in a cache program, `getPage()` is not good as `downloadPage()`

in a binaryTree class, `size()` doesn't convey much infomation, a specific name would be 
`height()`, `numNodes()`, `memoryBytes()`

in a thread class, `stop()` depends on what exactly it does, more specific name would be 
`kill()`, `pause()`, `resume()`

- find more colorful words

| word | alternatives |
| --- | --- |
| send | deliver, dispatch, announce, distribute, route |
| find| search, extract, locate, recover |
| strat | launch, create, begin, open |
| make | create, set up, build, generate, compose, add, new |

**key idea: It’s better to be clear and precise than to be cute**

1. Avoiding generic names (or knowing when to use them)
2. Using concrete names instead of abstract names
3. Attaching extra information to a name, by using a suffix or prefix
4. Deciding how long a name should be
5. Using name formatting to pack extra information
