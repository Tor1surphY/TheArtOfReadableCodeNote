# Chapter1 Code Should Be Easy to Understand

- The Fundamental Theorem of Readability

Code should be written to minimize the time it would take for someone else to understand it.

- Smaller is not always better.

Having fewer lines of code is a good goal, but

minimizing the time-till-understanding is an even better goal.

---

**Part I Surface-Level Improvement**

---

# Chapter2 Packing Infomation into Names

**key idea: Packing information into your names**

### 1. Choosing specific words

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

### 2. Avoiding generic names (or knowing when to use them)

- pick a name that describes the entity’s value or purpose

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

- Sometimes there are better iterator names than i, j, and k.

```c++
for(int i = 0; i < clubs.size(); i++)
    for(int j = 0; j < clubs[i].members.size(); j++)
        for(int k = 0; k < users.size(); k++)
            if(clubs[i].members[k] == users[j])
                cout << "user[" << j << "] is in club[" << i << "]" << endl;
```

better choice is `if(clubs[ci].members[mi] == users[ui])`

- there are some situations where generic names are useful

If you’re going to use a generic name like `tmp`, `it`, or `retval`, 
have a good reason for doing so.

### 3. Using concrete names instead of abstract names

When naming a variable, function, or other element, describe it concretely rather than
abstractly.

### 4. Attaching extra information to a name, by using a suffix or prefix

A variable’s name is like a tiny comment.

`string id; // Example: "af84ef845cd8"`

`hex_id` is more explicit for the reader to remember the ID’s format.

- Value with Units

```java
var start = (new Date()).getTime(); // top of the page
...
var elapsed = (new Date()).getTime() - start; // bottom of the page
document.writeln("Load time was: " + elapsed + " seconds");
```

this code doesn't have any wrong but dosen't work, 
because `getTime()` return `ms` not `s`.

By attaching `_ms` to make more explicit.

```java
var start_ms = (new Date()).getTime(); // top of the page
...
var elapsed_ms = (new Date()).getTime() - start_ms; // bottom of the page
document.writeln("Load time was: " + elapsed_ms / 1000 + " seconds");
```

| Function parameter | Renaming parameter to encode units |
| ---- | ---- |
| Start(int delay ) | delay → delay_secs |
| CreateCache(int size ) | size → size_mb |
| ThrottleDownload(float limit) | limit → max_kbps |
| Rotate(float angle) | angle → degrees_cw |

- Encoding Other Important Attributes

You should do it any time there’s something 
dangerous or surprising about the variable.

| Situation | Variable name | Better name |
| ---- | ---- | ---- |
| A password is in “plaintext” and should be encrypted before further processing | password | plaintext_password |
| A user-provided comment that needs escaping before being displayed | comment | unescaped_comment |
| Bytes of html have been converted to UTF-8 | html | html_utf8 |
| Incoming data has been “url encoded” | data | data_urlenc |

They’re most important in places where a bug can easily sneak 
in if someone mistakes what the variable is, 
especially if the consequences are dire, as with a security bug. 

### 5. Deciding how long a name should be

- shorter name is okay for shorter scope

When you go on a short vacation, you typically pack 
less luggage than if you go on a long vacation. 

- Acronyms and Abbreviations

Would a new teammate understand what the name means? 

If so, then  project-specific abbreviations are probably okay.

- Throwing Out Unneeded Words

`convertToString()` is not clear and simple as `toString()`

### 6. Using name formatting to pack extra information

`to_be_process` for variable names

`ClassName`     for class names

`quickSort()`   for function names

`MAX_DATA_SIZE` for macro definition names

`my_name_`      for const variable names

`_my_sercet`    for private variable names in class

### Summary

- Use specific words
- Avoid generic names
- Use concrete names
- Attach important details
- Use longer names for larger scopes
- Use capitalization, underscores, and so on in a meaningful way

# Chapter3 Names That Can’t Be Misconstrued

**key idea: Actively scrutinize(仔细检查) your names by asking yourself, “What other meanings could someone interpret from this name?”**

- Example 1:

`results = Database.all_objects.filter("year <= 2011")`

If you want “to pick out,” a better name is `select()`. 
If you want “to get rid of,” a better name is `exclude()`.

- Prefer `min` and `max` for (Inclusive) Limits

- Prefer `first` and `last` for Inclusive Ranges

- Prefer `begin` and `end` for Inclusive/Exclusive Ranges

- Naming Booleans

In general, adding words like `is, has, can, or should` can make booleans more clear.
it’s best to avoid *negated terms* in a name. 

### Matching Expectations of Users

```java
public class StatisticsCollector {
    public void addSample(double x) { ... }
    public double getMean() {
        // Iterate through all samples and return total / num_samples
    }
    ...
}
```

Instead, the method should be renamed to something like `computeMean()`.

```c++
void ShrinkList(list<Node>& list, int max_size) {
    while (list.size() > max_size) {
    FreeNode(list.back());
    list.pop_back();
    }
}
```

`list.size()` is an O(N) operation, 
which makes `ShrinkList()` an O(N^2) operation.
`countSize()` or `countElements()`, the same mistake would be less likely.

### Summary

- The best names are ones that can’t be misconstrued
- Before you decide on a name, imagine how your name might be misunderstood
- `max_` and `min_`  for upper or lower limit for a value
- `first` and `last` for inclusive ranges
- `begin` and `end` for inclusive/exclusive ranges, because they’re the most idiomatic(惯用的)
- use words like is and has to make boolean clear and avoid negated terms
- Be aware of users’ expectations about certain words

# Chapter4 Aesthetics

three principles we use:

1. use consistent layout(布局), with patterns the reader can get used to
2. make similar code look similar
3. group related lines of code into blocks

### Why Do Aesthetics Matter?

bad aesthetically code example:

```c++
class StatsKeeper {
public:
    // A class for keeping track of a series of doubles
    void Add(double d); // and methods for quick statistics about them
    private: int count; /* how many so far
    */ public:
            double Average();
private: double minimum;
    list<double>
    past_items
        ;double maximum;
};
```

aesthetically pleasing code example:

```c++
// A class for keeping track of a series of doubles
// and methods for quick statistics about them.
class StatsKeeper {
public:
    void Add(double d);
    double Average();
private:
    list<double> past_items;
    int count; // how many so far
    double minimum;
    double maximum;
};
```

### Rearrange Line Breaks to Be Consistent and Compact

a good example

```java
public class PerformanceTester {
    //    TcpConnectionSimulator(throughput, latency, jitter, packet_loss)
    //                           [Kbps]      [ms]     [ms]    [percent]
    public static final TcpConnectionSimulator wifi =
        new TcpConnectionSimulator(500,      80,      200,      1);

    public static final TcpConnectionSimulator t3_fiber =
        new TcpConnectionSimulator(45000,    10,      0,        0);

    public static final TcpConnectionSimulator cell =
        new TcpConnectionSimulator(100,      400,     250,      5);
}
```

### Use Methods to Clean Up Irregularity

### Use Column Alignment When Helpful

Straight edges and columns, example:

```c++
CheckFullName("Doug Adams" ,  "Mr. Douglas Adams" , "");
CheckFullName("Jake Brown ",  "Mr. Jake Brown III", "");
CheckFullName("No Such Guy" , ""                  , "no match found");
CheckFullName("John" ,        ""                  , "more than one result");
```

### Pick a Meaningful Order, ans Use It Consistently

- Match the order of the variables to the order of the input
- Order them from “most important” to “least important.”
- Order them alphabetically.

Whatever the order, you should use the same order throughout your code.

### Oraganize Declarations into Blocks

a good exmaple:

```c++
class FrontendServer {
public:
    FrontendServer();
    ~FrontendServer();

    // Handlers
    void ViewProfile(HttpRequest* request);
    void SaveProfile(HttpRequest* request);
    void FindFriends(HttpRequest* request);

    // Request/Reply Utilities
    string ExtractQueryParam(HttpRequest* request, string param);
    void ReplyOK(HttpRequest* request, string html);
    void ReplyNotFound(HttpRequest* request, string error)

    // Database Helpers
    void OpenDatabase(string location, string user);
    void CloseDatabase(string location);
};
```

### Break Code into "Paragraphs"

as above

### Personal Style versus Consistency

**key idea: Consistent style is more important than the “right” style.**

### Summary

- If multiple blocks of code are doing similar things, try to give them the same silhouette.
- Aligning parts of the code into “columns” can make code easy to skim through.
- If code mentions A, B, and C in one place, don’t say B, C, and A in another. Pick a meaningful order and stick with it.
- Use empty lines to break apart large blocks into logical “paragraphs.”

# Chapter5 Knowing What to Comment

**key idea: the purpose of commenting is to help the reader know as much as the writer did**

organized the chapter into the following areas:

1. knowing what not to comment
2. recording your thoughts as you code
3. putting yourself in the readers' shoes, to imagine what they'll need to konw

### What NOT to Comment

**key idea: don't comment on facts that can be derived quickly from the code itself**

#### don't comment just for the sake of commenting

comment like this:

```c++
// Find the Node in the given subtree, with the given name, using the given depth.
Node* FindNodeInSubtree(Node* subtree, string name, int depth);
```

is not as good as this:

```c++
// Find a Node with the given 'name' or return NULL.
// If depth <= 0, only 'subtree' is inspected.
// If depth == N, only 'subtree' and N levels below are inspected.
Node* FindNodeInSubtree(Node* subtree, string name, int depth);
```

#### don't comment bad names - fix the names instead

a good name is better than a good comment, a function name should be "self-documenting"

good code > bad code + good comments

### Recording Your Thoughts

#### include "director commentary"

include comments to record valuable insights about the code

#### comment the flaws in your code

| Maker | Typical meaning |
| ---- | ---- |
| TODO: | stuff I haven't gotten around to yet |
| FIXME: | konwn-broken code here |
| HACK: | admittedly inelegant solution to a problem |
| XXX: | danger! major problem here |

The important thing is that you should always feel free to comment on your thoughts about how the code should change in the future.

#### comment on your constants

most constants could be improved by adding a comment.