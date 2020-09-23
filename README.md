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

2. Avoiding generic names (or knowing when to use them)

pick a name that describes the entity’s value or purpose

in a JavaScript function that use `retval`

```java
var euclidean_norm = function (v) {
    var retval = 0.0;
    for (var i = 0; i < v.length; i += 1)
        retval += v[i] * v[i];
    return Math.sqrt(retval);
};
```

The name retval doesn’t pack much information. 
Instead, use a name that describes the variable’s value. 

In this case, better name is `sum_squares`

```java
if (right < left) {
    tmp = right;
    right = left;
    left = tmp;
}
```

in this case, tmp is a perfect name that means this variable has no other duties.

but in the following case, tmp is a lazy useway:

```java
String tmp = user.name();
tmp += " " + user.phone_number();
tmp += " " + user.email();
...
template.set("user_info", tmp);
```

`user_info` will be a better choice.

in the fllowing case, tmp is a part of the variable name,:

```java
tmp_file = tempfile.NamedTemporaryFile()
...
SaveData(tmp_file, ...)
```

guess if we use `SaveData(tmp, ...)`, it is not clear.

The name `tmp` should be used only in cases when being short-lived and temporary 
is the most important fact about that variable.

3. Using concrete names instead of abstract names
4. Attaching extra information to a name, by using a suffix or prefix
5. Deciding how long a name should be
6. Using name formatting to pack extra information