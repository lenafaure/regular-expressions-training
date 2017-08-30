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
?           ⟶ 0 or 1
{min, max}  ⟶ number of characters between min and max
{n}         ⟶ specific number of characters "n"
```

### Position
```
^           ⟶ start of the string/line
$           ⟶ end of the string/line
\b          ⟶ word boundary (finds a match at the beginning or end of a word)
```

### Character class
```
[]          ⟶ alternation: matches any one of the characters inside the brackets
[a-z]       ⟶ if the dash is not at the beginning it doesn't mean literal dash but any character a through f
```

**Search for a phone number with format 917-555-1234**
```
\d{3}-\d{3}-\d\{4}
```

**Search for a phone number with format 917-555-1234 Or 917.555.1234**
```
\d{3}[-.]\d{3}[-.]\d\{4}
```

**Search for a phone number with format 917-555-1234 or 917.555.1234 or (917)555-1234**
```
\(?\d{3}[-.)]\d{3}[-.]\d\{4}
```
⟶ Optionally a literal parenthesis at the beginning, no need to escape parenthesis inside character class

**Search for a phone number that has a 3-numbers sequence of 0 through 5**
```
[0-5]{3}
```

**Match all the words at the beginning of a line**
```
^\w+
``` 

**Match all the words at the end of a line**
```
\w+$
```

**Match all single words in a line**
```
^\w+$
```

**Match only four-letter words**
```
b\w{4}\b
```

**Match words between 4 and 6 characters**
```
b\w{4,6}\b
```

**Match the word "lynk or "link"**
```
l[yi]nk
```

