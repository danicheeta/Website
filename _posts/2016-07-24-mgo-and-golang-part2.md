---
layout: post
title: "Examples of using mgo in golan ;Part 2"
description: "Some code examples in go language"
tags: [database, go, golang, mgo, mongodb]
---

In this part we continue what we left of

We're gonna talk about how to find, delete and update a document

## Find
First of all, we should make an empty object to pass through func.
Then we should consider what type of object do we need, is it unique or gonna be set of objects

for unique we have what we had in last part:
{% highlight html %}
person := ppl{}
{% endhighlight %}

And for the set:
{% highlight html %}
type pplSet []ppl
pplset := pplsSet{}
{% endhighlight %}

There is 2 type of finding:

First type is finding by id; witch is the first part of your doc with the `_id` key
{% highlight html %}
collection.findId("your id").One(&person)
//or
collection.FindId("your id").All(&pplset)
{% endhighlight %}
U can make a for loop over your set like :
{% highlight html %}
for _ , person := range pplset{
  person.func()
}
{% endhighlight %}

Second type is finding by other keys
{% highlight html %}
collection.Find(bson.M{"key", "value"}).One(&person)
{% endhighlight %}
Remember that diffrence between these two, first type is faster
cuz the second type search all over the doc to fund the key but finding by Id only checks `_id` keys

## Delete
