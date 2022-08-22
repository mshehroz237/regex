# Regex Tutorial 	 | ✉️ Email Matching

(brought to you by: Muhammad Shehroz, August 21st 2022)

In this tutorial I will be discussing the wonderful world of regular expressions, aka Regex. A Regex is a set of characters that together make a pattern. They can by used inside of code or algorithms to locate, or even locate and replace if that's what you desire, specific patterns inside of a string. An example of this would be to validate a user's password, identify phone numbers, email addresses, URLs, and so much more.

## Summary :electron:

Moving forward we will be disecting, with consent from the Regex of course, that is being used to locate( as well as verify) an email address. Our volunteer is:</br> 

`\b[a-z0-9#$_-]+@[a-z0-9]+\.[a-z]{2,3}\b/gi`</br>

## Table of Contents

- [Email Validation Breakdown](#breakdown)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Author](#author)
- [Validation Image](#validation-image)


## 🐸 Email Validation Breakdown 
The breakdown of our brave Regex `\b[a-z0-9#$_-]+@[a-z0-9]+\.[a-z]{2,3}\b/gi`:

- The Alpha and the Omega(the beginning and the end) of it is of course the `\b`. That portion is called the "word boundaries". That states that the expression needs to be matched as a stand-alone word( or string if you're nasty). A good example would be the enclosed parenthesis, without separating spaces, their validation most certainly will fail as it will not match.

- The very 1st group `[a-zA-Z0-9#$_-]+` matches up any upper/lower case letter, any number, as well as the characters `#$_-`. The `-` used between the "a" and "z" provides the requirement of any letter between those two. On that note, the `0-9` means the same regarding numbers. The plus(`+`) sign(AKA a quantifier) after the closing bracket states that any of those characters before it can occur one time or more than one, an example would be `Rowdy_roddy388`. The square brackets are known as a "character class", which I will explain a bit further down. You may wonder how the Regex knows to identify both upper and lower case letters, to that I answer with a spotlight on that little `i` flag right at the end of it all. We'll also go into that below.

- After that is the `@`. The `@` is required for emails, nothing fancy needed there.

- The following group is `[a-z0-9]+` which also matches any upper/lower case letter, any number, and let's not forget the lovely `+` flag outside of the brackets. So if they have a username from somewhere like `nada1` it's all good, as the kids say, in the hood.

- Following that would be the `\.`, which is simply the dot before the extension(`com`,`gov`,`ca`, etc.,) escaped.

- Last, but certainly not least, is the `[a-z]{2,3}` which houses the extension. Which as you may have guessed is a two parter. The first part `[a-z]` you can probably guess what this is for, but let me secure your guess, yes it is the same as the 1st 2 parts. It simply is indicating the characters within the range of `a` to `z` and `A` to `Z`. The `{2,3}`(a fixed quantifier) is a new one for you. This is simply defining the minimum and maximum length for that extension. Some other examples would be `au`(Australia), `edu`(A school!), and `dd`(Germany).

- By their powers combined, they form `Rowdy_roddy388``@``nada1``.``com` or simple `Rowdy_roddy388@nada1.com`!

- I will include an image showing the validation in "action". Not only does the legendary `Rowdy_roddy388@nada1.com` make an appearance as proof pudding prime, but there are 2 other emails that can be seen passing(all highlighted in blue), plus one that didn't make the cut(It's kinda easy to see which failed). I also provided a JavaScript code that can be used via your browser's dev tool if you want to try it there, I also included a screenshot showing the ones that passed and failed(true = pass, false = fail).

### ⚓	 Anchors

The Regex, as stated earlier in this tutorial, begins with `\b`. This is called an anchor and it's job is to define a "word boundary". By using this at the beginning/end we are forcing what's called a "whole word" search. So for example, if the Regex was `\b867530\b`, then only `867530` would match up but not `8675309`, which as we all know would ruin the famous 1981 rock hit by Tommy Tutone.

Some other anchors are `^` and `$`:

^XXXXX will match any string that starts with ^XXXXX

XXXXX$ will match any string that ends with XXXXX$

Anchors are just a type of "meta-character". They don't match any characters, but instead they match specific positions. As you just saw `^` matches the starting position right before the 1st character of the search string. On the other hand `$` matches the end of the last character, and of course `\b` defines the entire boundary for the search string itself.

### 📡 Quantifiers

This sci-fi sounding portion is best simplified as a repeater. A quantifier repeats the previous item zero, 1, or more times. There are a fairly large list of quantifiers, but let's stick with the one we've already used. The `+` is part of that group, which states that the previous item(the collection of characters) can be repeated multiple times. They are also known as a "greedy quantifier" due to the fact that an item can be matched multiple times.

As we reviewed above, `{2,3}` is a fixed quantifier. This one specifically states that the search must be between 2 and 3 characters.

There are also simpler quantifiers, `{3,}` is a good example. This simply states that the preceding item repeats at least 2 times. This is an example of the "greedy quantifier" due to the fact that an item can be matched multiple times.


### 🧙‍♀️ Character Classes 🧝

No we aren't talking about your D&D half-orc Grumblethrust, we are referring to the the characters inside the square brackets. Those characters inside are the ones being matched, for example `[abceasyas123]` which will match `a`, `b`, `c`, `d`, `e`,`a`,`s`,`y`,`a`,`s`,`1`,`2`, or `3`. Seems like a lot, right? Well there's a <b>way</b> easier way to do lengthier parts, above you may have seen `[a-z]`, that states that <i>any</i> character between `a` and `z` will match(we ensured that both upper/lower case will also match with the `i` flag at the end). You can even get fancy like this `[a-z[aeiou]]` and match only the consonants, excluding every vowel!


### 🏴󠁵󠁳󠁰󠁲󠁿 Flags

This one we have gone over several times, but let's do a quick review. An example of a flag for Regex is that lovely `i` at the end of `\b[a-z0-9#$_-]+@[a-z0-9]+\.[a-z]{2,3}\b/i`, that's what prevents us from having to type out `\b[a-zA-Z0-9#$_-]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}\b/i`(note the addition of `A-Z`, with the `i` we don't need to put that in there as the flag provides that for us!). Now there's one other flag to keep in mind, that's the `g` flag. The `g` flag by itself provides a global search for the Regex definition matches, but you will have to include those pesky upper cases. How to resolve this you may be asking? Create the most ambitious cross-over event since Avengers: Endgame, add `gi`. That covers global searches AND upper/lower casing. 🌈⭐

### 💢 Bracket Expressions 💥

Brackets are pretty simple, these `[]` simply define the character class. Any characters placed inside them will produce a match to the Regex pattern, unless of course the negate character(`^`) precedes the characters in the class. In the Regex example above `[a-z]` defines any character class that is within the alphabet (let's not forget we are including both upper/lower cases due to that lovely `i`).

### 💰 Greedy and Lazy Match 🥱

The general concept of greedy and lazy quantifiers is related to the usage of quantifiers and what is being matched. A greedy quantifier matches as many items as possible like the Scrooge McDuck of searches, such as the `+` used above. A lazy match will attempt to match a Regex pattern just once, like an R2 droid with a bad motivator, and then it's done with that way.

### 🚪 Boundaries

Boundaries are important in and outside of code, but we're talking strictly about code here. The example that is defining the "red light/green light" for our example above is the `\b` at the start and end of the Regex. This indicates that a match will only occur if the string is matched in isolation, AKA is a whole word. To beat the digital horse mentioned above, if the Regex was `\b867530\b`, then not only do we ruin a great song, but it will never match up with `8675309` only `867530`.

## 🧙‍♂️ Author

Dan is one who loves to learn how things work, loves to make things his own by adding his personal touch to anything he can, loves to refer to himself in the 3rd person, and is fascinated by everything he has been learning in the University of Phoenix's full Stack Bootcamp and how he can utilize it for exciting projects in the future. While he has become quite adept at the back end of the stack, he has recently discovered that he seems to always gravitate towards the user experience and how to enhance it.

- :octocat: [Dan Arbelo](https://github.com/govepitr)<br />


## Github Gist
https://gist.github.com/mshehroz237/61683ffaf437c1b480d2075bd99dad14