## Start with a Story (Why Ruby Basics Exist)

Imagine this situation 👇

You’re building a **server**.

A request comes in:

> “Create a user named Nafis, age 25, active user”
> 

Now the server needs to:

- **Store values**
- **Know what kind of data they are**
- **Print logs**
- **Track objects in memory**

Without a clear system for **variables, types, and objects**, the server becomes chaos.

Ruby was designed to solve this cleanly.

---

## 1️⃣ Variables & Constants — *Why do we even need them?*

### The problem without variables

If you didn’t have variables:

- You couldn’t store request data
- You couldn’t reuse values
- You couldn’t pass data between methods

Every server request would be useless.

So Ruby gives us **names for values**.

---

### Variables in Ruby (Mental Model)

In Ruby:

- A variable is **a label**
- The value is **an object**
- The variable points to that object

🧠 **Important shift from JS:**

You’re not storing a primitive — you’re referencing an object.

```ruby
name = "Nafis"
age = 25

```

Here:

- `"Nafis"` is an object
- `25` is an object
- `name` and `age` are just references

---

### Constants — *Why do they exist?*

Problem:

Some values should **never change**:

- App name
- Max limits
- Config values

Ruby’s solution → **constants**

```ruby
APP_NAME = "MyServer"
MAX_USERS = 100

```

📌 Concept:

- Constants communicate **intent**
- Ruby will warn you if you try to change them

> “This value is not supposed to change.”
> 

---

## 2️⃣ puts vs print — *Why two ways to output?*

### The real-world need

On a server, you print things to:

- Debug
- Log
- Monitor behavior

But **how** you print matters.

---

### `print`

- Prints exactly what you give
- No new line

```ruby
print "Hello"
print "World"

```

Output:

```
HelloWorld

```

Use case:

- Formatting output
- Staying on the same line

---

### `puts`

- Prints value
- Adds a **new line**

```ruby
puts "Hello"
puts "World"

```

Output:

```
Hello
World

```

🧠 Ruby convention:

- **99% of the time → use `puts`**
- Cleaner logs
- Better readability

---

## 3️⃣ Data Types — *Why types exist at all?*

### The core problem

Imagine the server receives:

```json
"25"

```

Is it:

- Text?
- Number?
- Something else?

The server must **know how to treat data**.

Ruby solves this using **classes**.

---

### Ruby Data Types = Classes

| Value | Class |
| --- | --- |
| `"Hello"` | `String` |
| `25` | `Integer` |
| `3.14` | `Float` |
| `true` | `TrueClass` |
| `false` | `FalseClass` |
| `nil` | `NilClass` |

Already you can see:

👉 **Everything has a class**

---

### String

Used for:

- Names
- Messages
- JSON keys
- Text responses

```ruby
"Hello"

```

---

### Integer

Used for:

- IDs
- Counts
- Ages
- Status codes

```ruby
25

```

---

### Float

Used for:

- Prices
- Measurements
- Calculations

```ruby
3.14

```

---

### Boolean (true / false)

Used for:

- Conditions
- Flags
- Permissions

```ruby
true
false

```

---

### Nil — *Extremely important*

`nil` means:

> “Nothing exists here”
> 

Not:

- 0
- false
- empty string

Example:

```ruby
user = nil

```

📌 Server-side reality:

- Missing data
- Optional fields
- Failed queries

Understanding `nil` prevents **huge bugs**.

---

## 4️⃣ `.class` — *How Ruby thinks*

Now comes the **big Ruby realization**.

### Question:

How does Ruby know what `"Nafis"` is?

Answer:

Every value **knows its own class**.

```ruby
"Nafis".class
# => String

25.class
# => Integer

nil.class
# => NilClass

```

🧠 Meaning:

- Ruby doesn’t guess
- Objects describe themselves
- Behavior comes from class

---

## 5️⃣ `.object_id` — *Objects in Memory*

### The real problem

Servers run for a long time.

They need to:

- Track objects
- Avoid conflicts
- Manage memory

Ruby assigns **every object a unique identity**.

```ruby
name = "Nafis"
name.object_id

```

This ID represents:

> “This exact object in memory”
> 

---

### Important Concept (JS comparison)

```ruby
a = "hello"
b = "hello"

```

They **look** same

But they can be **different objects**

```ruby
a.object_id != b.object_id

```

This matters when:

- Mutating objects
- Sharing references
- Handling memory safely

---

## 6️⃣ The Big Idea — Ruby is Pure OOP

Here is the **most important takeaway**:

❌ Ruby does NOT have primitives

✅ Everything is an object

That means:

- Numbers have methods
- Strings have behavior
- `nil` has a class

Example:

```ruby
5.times do
  puts "Hello"
end

```

`5` is not a number — it’s an **object with methods**.

---

## Mental Model Recap (Very Important)

Think like this:

- Variables → references
- Values → objects
- Objects → have classes
- Classes → define behavior
- Ruby → everything is object