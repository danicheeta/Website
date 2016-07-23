---
layout: post
title: "Examples of using mgo in golan ;Part 1"
description: "Some code examples in go language"
tags: [database, go, golang, mgo, mongodb, driver]
---

there is going to be relief examples of using mgo driver in go from creating a session
to running queries

##dialing the server + getting session, database and collection
{% highlight html %}
session, err := mgo.Dial(your address)
if err != nil {
  log.Println(err)
  log.Fatalln("can't connect to database server")
}
defer session.Close()

db := session.DB(DB name)
col := db.C(collection name)
{% endhighlight %}


##adding a document to a collection in database
assume u have a structure called ppl like folowing:
{% highlight html %}
type ppl structure{
  id    bson.ObjectId `bson: "_id"`
  name  string
  phone string
}
{% endhighlight %}

u should notice that in this case mongodb server will take care of making a unique id
in this case witch is a 12byte hex string(i guess), if u want it otherwise (like u want your documents
  seprate by the Email) u can code like this:

{% highlight html %}
type ppl structure{
  Email string  `bson: "_id"`
  Name  string
  Phone string
}
{% endhighlight %}

then for for saving it in collection u gotta pass the address of our object to Inster
func
{% highlight html %}
s1 := ppl{
  Email: ***
  Name:  ***
  Phone: ***
}
collection.Insert(&s1)
{% endhighlight %}
