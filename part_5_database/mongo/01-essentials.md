---
title: MongoDB Essentials
date: 2016-08-15 17:27:38
tags:
categories: fullstack
---

No-sql?
no talbes

# mongod
Running background
need to specifiy a db path

# mongo
client ？
<!-- more -->
# WebStorm
Mongo Plugin

Create Database and insert data

## create or switch to the database
> use <database>

## list current database
> db

## delete current database
> db.dropDatabase()

json-generateor.com :)

## looking for the collections, if not exist then create it .
> db.players.insert({<new data>})

## insert a group of data
> db.players.insert([{},{}])

## list all the collections
> show collections

## look at all infroamtion on one collection
> db.players.find()

> db.players.find().pretty()

> db.players.findOne()

# Updating, removing collections

I got a "_id"

## remove
db.players.remove({"_id": ObjectId("182190...")})
## update
db.players.update(
	{"id": ObjectId("129191919...")},
	{new object}
)

## drop specific collections
db.players.drop()


## Find and Search Query
db.players.find(
	{"position": "Goalie"}
)

if you only find one
db.players.findOne(
	{"position": "Goalie"}
)

## multi conditions
db.players.find(
	{"position": "Goalie", "age": 21}
)

## OR
> db.players.find(
	{
		$or:[
			{"position": "Left Wing"},
			{"position": "Right Wing"}
		]
	}
)

## Need to know the $gt....
> db.players.find(
	{
		"age":{$gt:30}
	}
)

## only take the name ?
> db.players.find(
	{"postion": "center"},
	{"name":1, _id:0}
)

## only 3 of them, let assume only have 5 records.
> db.players.find(
	{"postion": "center"},
	{"name":1, _id:0}
).limit(3)

db.players.find(
	{"postion": "center"},
	{"name":1, _id:0}
).skip(2)


# Indexing
speed up database
> db.users.find(
	{"age":{$lt: 23}}
).explain("executionStats")

go find totalDocsExam..

> db.users.ensureIndex({"age": 1})
> db.users.getIndexs()

> db.users.dropIndex({"age": 1})


# Aggregation and Groups
How many people have brown eyes
> db.users.aggregate(
	$group:{
		_id : "$eyeColor",
		total: {$sum: 1}
	}
)


> db.users.aggregate(
	$group:{
		_id : "$gender",
		avaAge: {$avg: "$age"}
	}
)

> db.users.aggregate(
	$group:{
		_id : "$gender",
		richest: {$max: "$balance"}
	}
)


express and mongoose

npm install -S mongoose

app.js

var mongoose = require(‘mongoose’);

mongoose.connect(“”)

[Node.js MongoDB Tutorial using Mongoose](https://www.youtube.com/watch?v=5e1NEdfs4is&feature=iv&src_vid=ndKRjmA6WNA&annotation_id=annotation_3022639507)