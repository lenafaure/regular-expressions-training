# Regular Expressions Training - Search Patterns for text

### Following [The Coding Train - Regular Expressions Series](https://www.youtube.com/watch?v=7DG3kCDx53c&list=PLRqwX-V7Uu6YEypLuls7iidwHMdCM6o2w)

### Single characters
```
\d          ⟶ 0-9
\w          ⟶ A-Z a-z 0-9 ("word")
\W          ⟶ Anything that is not one of the characters searched by \w
\s          ⟶ whitespace
\S          ⟶ Anything that is not whitespace
.           ⟶ any character
```

### Quantifiers
```
*           ⟶ 0 or more 
.*          ⟶ wildcard (matches everything)
+           ⟶ 1 or more
?           ⟶ 0 or 1, or make the quantifier not greedy (will stop after match is found)
{min, max}  ⟶ number of characters between min and max
{n}         ⟶ specific number of characters "n"
```

### Position
```
^           ⟶ start of the string/line
$           ⟶ end of the string/line
\b          ⟶ word boundary (finds a match at the beginning or end of a word)
```

### Flags
```
g           ⟶ searches for all the matching patterns, not only the first one
i           ⟶ case insensitive
```

### Character class
```
[]          ⟶ matches any one of the characters inside the brackets
[-abc]      ⟶ dash at the beginning of the character class is the literal character
[a-f]       ⟶ if the dash is not at the beginning it doesn't mean literal dash but any character a through f
[^abc]      ⟶ caret at the beginning of the character class negates the sequence that follows
[ab^c]      ⟶ if the caret is not at the beginning it means literal character
(|)         ⟶ matches one of the groups of characters separated by a pipe symbol 
```

### Capturing Groups
```
()          ⟶ adding a parenthesis inside a regular expression adds a subgroup of strings (the whole match is group 0)
$n          ⟶ refers to the captured group index when you want to do a replace
\n          ⟶ refers to the captured group expression index inside a regex
```

### Regex in JavaScript

```javascript

// Write a new regex:
var r = /.../;

// Test the regex for true or false:
r.test("hello"); 

// Returns the matching pattern
string.match(r);

// The regex executes the string
r.exec(string);

```


**Search for a phone number with format 917-555-1234**
```javascript
\d{3}-\d{3}-\d\{4}
```

**Search for a phone number with format 917-555-1234 or 917.555.1234**
```javascript
\d{3}[-.]\d{3}[-.]\d\{4}
```

**Search for a phone number with format 917-555-1234 or 917.555.1234 or (917)555-1234**
```javascript
\(?\d{3}[-.)]\d{3}[-.]\d\{4}
```
⟶ Optionally a literal parenthesis at the beginning, no need to escape parenthesis inside character class

**Search for a number that has a 3-numbers sequence of 0 through 5**
```javascript
[0-5]{3}
```

**Match all the words at the beginning of a line**
```javascript
^\w+
``` 

**Match all the words at the end of a line**
```javascript
\w+$
```

**Match all single words in a line**
```javascript
^\w+$
```

**Match only four-letter words (characters and digits)**
```javascript
b\w{4}\b
```

**Match any four-letter word only with characters in it**
```javascript
\b[A-Za-z]{4}\b
```

**Match words between 4 and 6 characters**
```javascript
b\w{4,6}\b
```

**Match the word "lynk or "link"**
```javascript
l[yi]nk
```

**Match a word beginning with a single capital letter followed by one or more lowercase letters**
```javascript
\b[A-Z][a-z]+\b
```

**Match an email adress with suffix of .com, .edu or .net**
```javascript
[\w.]+@\w+\.(net|com|edu)
```

**Find and replace phone number with the three phone number format by 917-xxx-xxxx**
```javascript
\(?(\d{3})[-.)]\d{3}[-.]\d\{4}
$1-xxx-xxxx
```
⟶ Capturing the first group and replacing the rest

**Reverse Last Name and First Name written in format "Lastname, Firstname"**
```javascript
(\w+),\s+(\w+)
$2 $1
```

**Matching links in markdown with format `[Google](http://google.com)` and translate into html**
```javascript
\[(.*?)]\((http.*?)\)
<a href="$2">$1</a>
```
⟶ Literal square brackets with backslash and question mark to make the quantifier not greedy

**Searching for double words in a row**
```javascript
\b(\w+)\s\1\b
```
⟶ Match any number of word characters in a row - captured as group 1 - followed by a whitespace, and the specific thing you captured as group 1, match that again (`\1`), with boundaries

**JavaScript examples**
⟶ [Test it in JSBin](https://jsbin.com/teyaniguho/edit?js,console)

#### test() and match()

```javascript
/* A regex that matches 3 digits in a row */
var r = /\d{3}/;
console.log(r.test("hello")); //false
console.log(r.test("123")); //true
console.log(r.test("123ABC")); //true because the regex is found within the string

/* A regex that matches exactly 3 digits */
var r1 = /^\d{3}$/;
console.log(r1.test("123ABC")); // false
console.log(r1.test("123")); //true

/* A regex that matches an email adress */
var r2 = /[\w.]+@\w+\.(net|com|edu)/;
console.log(r2.test("mail@mail")); // false
console.log(r2.test("mail@mail.com")); // true

/* A regex that matches the word unicorn */
var s = "unicorns and rainbows and cupcakes";
var r3 = /unicorn/;
console.log(s.match(r3)); // ["unicorn"]

/* A regex that matches all the words in a string */
var r4 = /[a-z]+/g;
console.log(s.match(r4)); // ["unicorns", "and", "rainbows", "and", "cupcakes"]

/* A regex that matches all the words case insensitive */
var s2 = "unicorns and Rainbows and Cupcakes";
var r5 = /[a-z]+/gi;
console.log(s2.match(r4)); // ["unicorns", "and", "ainbows", "and", "upcakes"]
console.log(s2.match(r5)); // ["unicorns", "and", "Rainbows", "and", "Cupcakes"]

/* A regex that matches a phone number format */
var s3 = "Here are these two numbers 111-2222 and 444-5555"
var r6 = /\d{3}[-.]\d{4}/g;
var matches = s3.match(r6);

for (var i = 0; i < matches.length; i++) {
  console.log(matches[i]);
}

// "111-2222" "444-5555"

/* A regex that captures the first three digits */
var s4 = "Here are these two numbers 111-2222 and 444-5555"
var r7 = /(\d{3})[-.]\d{4}/;
var matches2 = s4.match(r7);

console.log(matches2); // ["111-2222", "111"] 

// if you are not using the global flag, the match() function will give you the groups as an array
// if you are using the global flag, you need to use exec()
```

#### exec()

```javascript
/* A regex that executes a string */

var s5 = "Here are these two numbers 111-2222 and 444-5555";
var r8 = /(\d{3})[-.]\d{4}/g;
var result = r8.exec(s5);

while (result != null) {
  result = r8.exec(s5);
  console.log(result);
}

// ["111-2222", "111"] ["444-5555", "444"]
```

