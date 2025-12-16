# Mongoose-mongoDB Sheet

## Setup & connection

```
const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/node-mongo-app").then(() => {
    console.log("Mongo connected");
}).catch((err) => { console.log("Error while connecting mongo :", err) })
```

## Schema & Model

```
const userSchema = new mongoose.Schema({
  name: { type: String, required: true},
  email: { type: String, required: true, unique: true },
  age: {type:Number},
  isActive: { type: Boolean, default: true }
}, { timestamps: true });

// Create Model
const User = mongoose.model("User", userSchema);
```

## CRUD Operations

#### Create

```
await User.create({ name: "Aman", email: "aman@test.com" });
```

#### Read

```
User.find() // find all entries
User.findOne({ email: "aman@test.com" }) // finds the 1st occurrence
User.findById(id)
User.find({ age: { $gte: 18 } }) // Find all entries with filter
```

#### Update

```
User.findByIdAndUpdate(id, { age: 25 }, { new: true })
```

#### Delete

```
User.findByIdAndDelete(id)
```

## Query Helpers

```
User.find()
  .select("name email")
  .sort({ createdAt: -1 })
  .limit(10)
  .skip(20);

// here sort = -1 is decending || skip is like offset
```

## Indexed & Constraints

-Indexes decide how FAST Mongo finds data.

```
email: { type: String, unique: true } // This internally becomes like below [userSchema.index({ email: 1 });]
```

```
userSchema.index({ email: 1 }); // Indexing based on email && in asending(email) 
```

## Relationships (Populate)

#### Reference (Like foreign key)
```
const postSchema = new mongoose.Schema({
  title: String,
  user: { type: mongoose.Schema.Types.ObjectId, ref: "User" }
});
```
#### Populate - similar to JOIN

```
Post.find().populate("user");
```
- Without populate - Post.find(); =>  {"title": "Mongo Basics", "user": "user456"}
- With Populate - Post.find().populate("user"); => {"title": "Mongo Basics", "user":{ "_id": "user456", "name": "Aman" }}

**NOTE :** We have 

## Validation

```
email: {
  type: String,
  required: true,
  match: /.+\@.+\..+/
}
```
```
age: {
  type: Number,
  min: 18,
  max: 60
}
```

## Middleware (Hooks)

#### Pre-save

```
userSchema.pre("save", function(next) {
  this.name = this.name.toUpperCase();
  next();
});
```

#### Post-save

```
userSchema.post("save", function(doc) {
  console.log("User saved", doc._id);
});
```

## Lean Queries (Performance 🔥)

```
User.find().lean();  // Returns plain JS objects, not Mongoose documents, Faster for read-only APIs
```

## Pagination Pattern
```
const page = 2;
const limit = 10;

User.find()
  .skip((page - 1) * limit)
  .limit(limit);
```

## Transactions

```
const session = await mongoose.startSession();
session.startTransaction();

try {
  await User.create([{ name: "Aman" }], { session });
  await session.commitTransaction();
} catch (e) {
  await session.abortTransaction();
}
session.endSession();
```

## Common mongo Operations

- `$gt` - greater than
- `$lt` - less than
- `$in` - in array
- `$ne` - not equal
- `$exists` - field exists
- `$regex` - pattern match

```
User.find({ name: { $regex: "^Am", $options: "i" } })
```

## Aggregation (Very Important for Backend)

```
User.aggregate([
  { $match: { isActive: true } },
  { $group: { _id: "$age", count: { $sum: 1 } } }
]);
```







