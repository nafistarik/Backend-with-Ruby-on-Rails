## Why Ruby Is Designed Around OOP (Feel the Problem First)

Imagine you’re building a server **without classes**.

You have:

- user names
- user emails
- user roles
- user permissions

Without classes, you’d do this:

```ruby
name = "Nafis"
email = "nafis@email.com"
role = "admin"
```

Now imagine **100 users**.

You’d need:

- name1, name2, name3 ❌
- role1, role2 ❌
- total chaos ❌

The server needs:

> “One concept that groups data + behavior together.”
> 

That concept is **a class**.

---

## 1️⃣ Class — A Blueprint (Not a Value)

### Mental Model

A class is:

> A blueprint for creating objects
> 
- Class ≠ user
- Object = actual user

Think:

- Class → design
- Object → real thing

---

### Ruby Syntax

```ruby
class User
end

```

This **does nothing yet** — and that’s fine.

---

## 2️⃣ Object — A Real Instance

Now let’s create a real user:

```ruby
user1 = User.new
user2 = User.new

```

Each `User.new`:

- Creates a **new object**
- Allocates memory
- Has its own identity

```ruby
user1.object_id != user2.object_id

```

---

## 3️⃣ `initialize` — Birth of an Object

### The Problem

When a user is created, we want:

- name
- email
- role

Without control, objects are empty and useless.

Ruby gives us `initialize`.

---

### Concept

`initialize` is:

> Automatically called when .new is used
> 

You never call it manually.

---

### Example

```ruby
class User
  def initialize(name)
    @name = name
  end
end

```

Usage:

```ruby
user = User.new("Nafis")

```

What happens step-by-step:

1. Memory allocated
2. `initialize("Nafis")` runs
3. `@name` is set

---

## 4️⃣ Instance Variables (`@`) — Object Memory

### Why `@` Exists

Local variables disappear after method ends.

Objects need **persistent state**.

---

### Example

```ruby
class User
  def initialize(name)
    name = name       # ❌ local variable
    @name = name      # ✅ instance variable
  end
end

```

Only `@name` stays with the object.

---

### Each Object Has Its Own State

```ruby
user1 = User.new("Nafis")
user2 = User.new("Sara")

```

- `user1.@name` → "Nafis"
- `user2.@name` → "Sara"

No collision. No shared data.

---

## 5️⃣ Methods Belong to Objects

### Add Behavior

```ruby
class User
  def initialize(name)
    @name = name
  end

  def greet
    "Hello #{@name}"
  end
end

```

Usage:

```ruby
user.greet
```

🧠 Important:

- Methods **read and modify** instance variables
- Objects know how to act

---

## 6️⃣ Getters — Reading Object State

### The Problem

This fails:

```ruby
user.name  # ❌ undefined method

```

Why?

- `@name` is private
- Ruby protects internal state

---

### Manual Getter

```ruby
class User
  def initialize(name)
    @name = name
  end

  def name
    @name
  end
end

```

Now:

```ruby
user.name  # "Nafis"

```

---

## 7️⃣ Setters — Changing Object State

### Manual Setter

```ruby
class User
  def name=(new_name)
    @name = new_name
  end
end

```

Usage:

```ruby
user.name = "New Name"

```

🧠 Ruby trick:

- Setter methods use `=`
- But are called like assignment

---

## Final Mental Model 🧠

- Class → blueprint
- Object → real entity
- `initialize` → object birth
- `@variable` → object memory
- Methods → behavior
- Getters/setters → controlled access

---