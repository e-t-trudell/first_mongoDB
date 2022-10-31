<!-- Create the following mongo database and copy console text to this document.
1)Create a database called 'my_first_db' -->
test> use 'my_first_db'
switched to db 'my_first_db'
'my_first_db'> show dbs
This_one  80.00 KiB
admin     72.00 KiB
config    72.00 KiB
local     72.00 KiB
'my_first_db'> 

<!-- 2)Create students collection. -->
'my_first_db'> db.createCollection('students')
{ ok: 1 }

<!-- 3)Each document you insert into this collection should have the following format: ({name: STRING, home_state: STRING, lucky_number: NUMBER, birthday: {month: NUMBER, day: NUMBER, year: NUMBER}})
4)Create 5 students with the appropriate info. -->
a)'my_first_db'> db.students.insertOne({name:'Eric',homestate:'Colorado',lucky_number:12, birthday:{month:1, day:2, year:1992}})
{
  acknowledged: true,
  insertedId: ObjectId("635ecf5cda8f9d9619c65dfe")
}
b)'my_first_db'> show collections
students
'my_first_db'> db.students.insertOne({name:'Tim',home_state:'California',lucky_number:15,birthday:{month:2,day:3,year:1990}})
{
  acknowledged: true,
  insertedId: ObjectId("635ed2d9da8f9d9619c65dff")
}
'my_first_db'> 
c)'my_first_db'> db.students.insertOne({name:'CookieMonster',home_state:'Washington',lucky_number:1,birthday:{month:5,day:14,year:1912}})
{
  acknowledged: true,
  insertedId: ObjectId("635ed409da8f9d9619c65e01")
}
d)'my_first_db'> db.students.insertOne({name:'HarryPotter',home_state:'Maine',lucky_number:12,birthday:{month:8,day:29,year:1800}})
{
  acknowledged: true,
  insertedId: ObjectId("635ed44ada8f9d9619c65e02")
}
e)'my_first_db'> db.students.insertOne({name:'Lacy',home_state:'Florida',lucky_number:6,birthday:{month:9,day:23,year:1703}})
{
  acknowledged: true,
  insertedId: ObjectId("635ed47bda8f9d9619c65e03")
}
<!-- 5)Get all students. -->
'my_first_db'> db.students.find()
[
  {
    _id: ObjectId("635ecf5cda8f9d9619c65dfe"),
    name: 'Eric',
    homestate: 'Colorado',
    lucky_number: 12,
    birthday: { month: 1, day: 2, year: 1992 }
  },
  {
    _id: ObjectId("635ed2d9da8f9d9619c65dff"),
    name: 'Tim',
    home_state: 'California',
    lucky_number: 15,
    birthday: { month: 2, day: 3, year: 1990 }
  },
  {
    _id: ObjectId("635ed3c7da8f9d9619c65e00"),
    name: 'Tim',
    home_state: 'California',
    lucky_number: 15,
    birthday: { month: 2, day: 3, year: 1990 }
  },
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 }
  },
  {
    _id: ObjectId("635ed44ada8f9d9619c65e02"),
    name: 'HarryPotter',
    home_state: 'Maine',
    lucky_number: 12,
    birthday: { month: 8, day: 29, year: 1800 }
  },
  {
    _id: ObjectId("635ed47bda8f9d9619c65e03"),
    name: 'Lacy',
    home_state: 'Florida',
    lucky_number: 6,
    birthday: { month: 9, day: 23, year: 1703 }
  }
]
<!-- 6)Retrieve all students who are from California (San Jose Dojo) or Washington (Seattle Dojo). -->
California: 'my_first_db'> db.students.find({home_state:'California'})
[
  {
    _id: ObjectId("635ed2d9da8f9d9619c65dff"),
    name: 'Tim',
    home_state: 'California',
    lucky_number: 15,
    birthday: { month: 2, day: 3, year: 1990 }
  },
  {
    _id: ObjectId("635ed3c7da8f9d9619c65e00"),
    name: 'Tim',
    home_state: 'California',
    lucky_number: 15,
    birthday: { month: 2, day: 3, year: 1990 }
  }
]
'my_first_db'> 
Washington:
'my_first_db'> db.students.find({home_state:'Washington'})
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 }
  }
]
<!-- 7)Get all students whose lucky number is greater than 3 -->
'my_first_db'> db.students.find({lucky_number:{$lt:3}})
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 }
  }
]
<!-- 8)Get all students whose lucky number is less than or equal to 10 -->
'my_first_db'> db.students.find({lucky_number:{$lte:10}})
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 }
  },
  {
    _id: ObjectId("635ed47bda8f9d9619c65e03"),
    name: 'Lacy',
    home_state: 'Florida',
    lucky_number: 6,
    birthday: { month: 9, day: 23, year: 1703 }
  }
]
<!-- 9)Get all students whose lucky number is between 1 and 9 (inclusive) -->
'my_first_db'> db.students.find({lucky_number:{$in:[1,2,3,4,5,6,7,8,9]}})
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 }
  },
  {
    _id: ObjectId("635ed47bda8f9d9619c65e03"),
    name: 'Lacy',
    home_state: 'Florida',
    lucky_number: 6,
    birthday: { month: 9, day: 23, year: 1703 }
  }
]
<!-- 10)Add a field named 'interests' to all student documents in the collection. The field should be an array and contain the following entries: 'coding', 'brunch', MongoDB'. Add this field to all documents using a single command. -->
'my_first_db'> db.students.updateMany({},{$set:{interests:['coding','brunch','MongoDB']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 6,
  modifiedCount: 5,
  upsertedCount: 0
}
'my_first_db'> 

<!-- 11)Add some unique interests for each particular student into each of their interest arrays. -->
'my_first_db'> db.students.updateOne({name:'Eric'},{$push:{interests:['snowboarding']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({name:'Eric'},{$push:{interests:['snowboarding']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed2d9da8f9d9619c65dff")},{$push:{interests:['tennis']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed3c7da8f9d9619c65e00")},{$push:{interests:['Fishing']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed409da8f9d9619c65e01")},{$push:{interests:['Cookies']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed44ada8f9d9619c65e02")},{$push:{interests:['Magic']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed47bda8f9d9619c65e03")},{$push:{interests:['Diamonds']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}


<!-- 12)Add the interest 'taxes' into someone's interest array. -->
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed47bda8f9d9619c65e03")},{$push:{interests:['Taxes']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
13)Remove the 'taxes' interest you just added.
'my_first_db'> db.students.updateOne({_id: ObjectId("635ed47bda8f9d9619c65e03")},{$pull:{interests:['Taxes']}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
'my_first_db'> 

<!-- 14)Remove all students who are from California. -->
'my_first_db'> db.students.deleteMany({home_state:'California'})
{ acknowledged: true, deletedCount: 2 }

<!-- 15)Remove a student by name. -->
'my_first_db'> db.students.deleteOne({name:'Lacy'})
{ acknowledged: true, deletedCount: 1 }

<!-- 16)Remove a student whose lucky number is greater than 5 (JUST ONE) -->
'my_first_db'> db.students.deleteOne({lucky_number:{$gt:5}})
{ acknowledged: true, deletedCount: 1 }

<!-- 17)Add a field to each student collection called 'number_of_belts' and set it to 0. -->
'my_first_db'> db.students.updateMany({},{$set:{number_of_belts:0}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}

<!-- 18)Increment this field by 1 for all students in Washington (Seattle Dojo). -->
<!-- could also use {$inc:{}} here -->
'my_first_db'> db.students.updateMany({home_state:'Washington'},{$set:{number_of_belts:1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
<!-- 19)Rename the 'number_of_belts' field to 'belts_earned' -->
'my_first_db'> db.students.aggregate([{$replaceWith:{$setField:{field:'belts_earned',input:'$$ROOT',value:1}}},{$unset:'number_of_belts'}])
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    lucky_number: 1,
    birthday: { month: 5, day: 14, year: 1912 },
    interests: [ 'coding', 'brunch', 'MongoDB', [ 'Cookies' ] ],
    belts_earned: 1
  },
  {
    _id: ObjectId("635ed44ada8f9d9619c65e02"),
    name: 'HarryPotter',
    home_state: 'Maine',
    lucky_number: 12,
    birthday: { month: 8, day: 29, year: 1800 },
    interests: [ 'coding', 'brunch', 'MongoDB', [ 'Magic' ] ],
    belts_earned: 1
  }
]
'my_first_db'> 

<!-- 20)Remove the 'lucky_number' field. -->
'my_first_db'> db.students.updateMany({},{$unset:{lucky_number:1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}
'my_first_db'> 
<!-- 21)Add a 'updated_on' field, and set the value as the current date.($currentDate) -->
db.students.updateMany({},{$set:{update_on:1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}
'my_first_db'> db.students.updateMany({},{$currentDate:{update_on:{$type:'date'}}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}
'my_first_db'> db.students.find({})
[
  {
    _id: ObjectId("635ed409da8f9d9619c65e01"),
    name: 'CookieMonster',
    home_state: 'Washington',
    birthday: { month: 5, day: 14, year: 1912 },
    interests: [ 'coding', 'brunch', 'MongoDB', [ 'Cookies' ] ],
    number_of_belts: 'belts_earned',
    update_on: ISODate("2022-10-31T00:14:37.493Z")
  },
  {
    _id: ObjectId("635ed44ada8f9d9619c65e02"),
    name: 'HarryPotter',
    home_state: 'Maine',
    birthday: { month: 8, day: 29, year: 1800 },
    interests: [ 'coding', 'brunch', 'MongoDB', [ 'Magic' ] ],
    number_of_belts: 'belts_earned',
    update_on: ISODate("2022-10-31T00:14:37.493Z")
  }
]