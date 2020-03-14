---
layout: post
title: "Using Kotlin for Few Months: Amazing"
date: 2020-03-14 20:00:00 +7
comments: true
categories:
---

So, it's been around two months I've been using Kotlin for my daily job. No, not for Android. I use it for back-end stuffs, leverage the power of Spring Framework which is already supported Kotlin. And Kotlin surprised me a lot, besides the fact it does not require semicolon to end the line, haha. So much magical syntax and code-simplifying it has. It got me saying: "Holy crap, we can do this??"

These are some summaries I gather while learning-by-doing Kotlin:

## Powerful Collection Library

Kotlin has built-in library for Collection, so we won't need to import basic Collection data structure type from `java.util.*`. We can simply define a variable with *List* type by typing:

```kotlin
val lists: List<Books>
```

We can even create those variables and put values directly in it, all in one line:

```kotlin
val listOfTitles = listOf("One Upon A Time in Hollywood", "Sapiens", "Homo Deus")
val arrayListOfFruits = arrayListOf("Mango", "Durian", "Peach")
```

How about map? Of course, Kotlin got me amazed for this.

```kotlin
val mapOfCars = mapOf(
	"car-A" to "Toyota 1990",
	"car-B" to "BMW 2000"
)
```

Did you see that? These collections also equipped with cool functions. Let's see.

### List.forEach

This is quite obvious, basically it does for-loop operation, which I prefer to use native for-loop if my task is quite heavy.

```kotlin
listOfFruits.forEach {
	println(it)
}

```

What I did in the code was just print all the elements in the list.

### List.map

This could be the function I have been using the most so far. It basically iterating through every element on the list, do whatever task we address to the element and produce new list from it.

```kotlin
// Let's say I have this data class
data class Book(val id: Int, val title: String)

val listOfNumbers = listOf(1, 2, 3)
listOfNumbers.map {
	Book(it, "Once Upon a Time: $it Episode")
}
```

It produces a list of Book entities.

### List.filter

Kotlin's List have filter function, and this is just amazing. That means, I don't have to iterate to all over the element one by one and do checking for every element it has, instead I only have to do this:

```kotlin
val listOfNumbers = listOf(11,23,3,54,122,55,66,482,172,28,9,0,1812)
listOfNumbers.filter { it > 10 && it < 100 }
```

The code above will produce a new list with filtered elements. See how easy is that.

### List.associate & List.associateWith

These functions are really awesome. It converts our list to Map. `associate` will produce `Pair<K, V>` and we can define what type our key will be while `associateWith` will produce Map with current element as a key. Let's take a look.

```kotlin
val listOfNumbers = listOf(1, 2, 3)
listOfNumbers.associate {
	Pair("key-$it", "Value of $it")
}
// will produce map contains:
//	("key-1", "Value of 1")
//	("key-2", "Value of 2")
//	("key-3", "Value of 3")


listOfNumbers.associateWith {
	"Value of $it"
}
// will produce map contains:
//	(1, "Value of 1")
//	(2, "Value of 2")
//	(3, "Value of 3")

```

So cool, right?

## Spring x Kotlin = Cool!

Since the rising of Spring Boot, it help us developers to build robust and secure web application faster, upon the infrastructure of Spring Framework. And Kotlin actually made it even better.

### Less Usage of @Autowired

To inject a property with pre-defined `@Bean` in Spring, we need to add `@Autowired` annotation to that property. We can omit that annotation in Kotlin by defining the class like this:

```kotlin
@Service
class MessageService(
	private val kafkaProperties: KafkaProperties,
	private val loggerUtils: LoggerUtils
) {
	// class implementation . . .	
}
```

That will force the class to have constructor with all required properties, thus will inject those properties with pre-defined `@Bean`. In Java, we have to self-define the constructor, or we can do that with the help of **Lombok** library. In Kotlin, we don't need additional library.

### All configurations in the same file

Since Kotlin supports multiple class declaration in one file, I could say this is a good advantage.

### Less lines of code

Well, Kotlin actually made my codes look beautiful and clean. We can get rid a lot of lines and the codes still working, LOL. One of the cool feature is the one-line-function (this is our self-named feature, me and my workmates, LOL).

```kotlin
fun decideTheNumber(input: Int) = if (input > 10) "It's more than ten, dude" else "Hmm, can you give me more?"
```

## Summary

That's all I can tell for now, about my experience during these last 2 months working with Kotlin. Actually it's a romantic story and I love it so much. 

Thanks!