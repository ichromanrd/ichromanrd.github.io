---
layout: post
title: "Formatting String in Kotlin"
date: 2020-03-28 18:00:00 +7
comments: true
categories:
---

## The Story Behind This Post

Ah, actually this post is not an advanced topic. String is a common data type almost in all programming languages to represent a bunch of sequenced characters. But again, I felt so stupid when my colleague in office gave his review in my pull request. It is a case about String formatting. Here is the problem:

The service I work on receives a date value in format `dd-MM-yyyy` in one of its endpoints. What I had to do with the date is to convert it to actual `java.util.Date` object, with the complete GMT value (we already had this). So what I did is receive the date string, use `java.text.SimpleDateFormat` with pattern: `dd-MM-yyyy HH:mm:ss.SSSZ`. Quite simple right? The value for `HH:mm:ss.SSS` was hardcoded so it was not a big deal. The struggle came with that `Z` code. OK, `Z` accept value with format `(+/-)dddd` where d is an integer. Basically it represents GMT time, so it could be +0700 for Asia/Jakarta, or +0900 for Asia/Tokyo, whatever. There was a given timezone offset, stored somewhere in our DB. Basically they were only 7, 8 and 9 (represented Indonesian timezones).

And to format them into GMT format acceptable by that `Z`, I was using this code (in Kotlin):

```kotlin
private fun createTimeZone(tzOffset: Short): String {
    if (tzOffset >= 0 && tzOffset <= 9) return "+0${tzOffset}00"
    if (tzOffset > 9) return "+${tzOffset}00"
    if (tzOffset < 0 && tzOffset >= -9) return "-0${tzOffset * -1}00"
    if (tzOffset < -9) return "${tzOffset}00"
    return ""
}
```

See how verbose and naive it was? LOL.

And then my colleague gave his review:

> Is +800 treated differently than +0800?
If it does, you can use "02%d".format(tzOffset) to get a 2-digit zero-padded printed number, so that your logic can be simplified.

Seriously, I didn't know I could do that, or I forgot (?). LOL. Yeah, what he meant was, we can do something like this to format a number with leading zeros:

```kotlin
var number = 9
println("%02d".format(number)) // this will produce 09

number = 11
println("%02d".format(number)) // this will produce 11
```

Well, he was right. So I refactored my codes and condemned my self "dumbass". I removed the verbose function and now my code looks simpler. I only needed to check if the timezone:

```kotlin
val tzOffset = city.province.tzOffset

val sign = if (tzOffset < 0) "-" else "+"
val gmt = "$sign${"%02d00".format(if (tzOffset < 0) tzOffset * -1 else tzOffset)}"

val dateFormat = SimpleDateFormat("dd-MM-yyyy HH:mm:ss.SSSZ")
val startTime = dateFormat.parse("$date 00:00:00.000$gmt")
val endTime = dateFormat.parse("$date 23:59:59.999$gmt")
```

And that's all.


## String Templating and Formatting in Kotlin

Yes it is. Let's start with the String templating.

### Templating

In Kotlin we can do something like this to reduce concatenation.

```kotlin
val name = "Ichroman Raditya"
val hello = "Hello $name"
```

We can even evaluate an expression:

```kotlin
val printNumber = "The result of 1 + 2 is ${1 + 2}"
```

### Formatting

`String.forrmat()` really helpful when it comes to string formatting. Well I told you a lot in previous part, the background about this post, LOL. Here is the table of type specifiers and their meanings:

| Code    | Description                                                 |
|---------|-------------------------------------------------------------|
| %s      | String
| %c      | Character
| %d	   | Signed Integer                                             
| %e	   | Float in Scientific Notation
| %f	   | Float in Decimal Format
| %g	   | Float in Decimal or Scientific Notation, depending on value 
| %h	   | Hashcode of the supplied argument
| %n	   | Line separator
| %o	   | Octal Integer
| %s	   | String
| %t	   | Date or Time
| %x      | Hexadecimal Integer

To use them, simply put each of them in the string and then use `.format` with the value.

```kotlin
println("Format this: %s %d %c".format("first string", 10, 'A'))
```

That's all. This post already long enough haha. Thank you!
