## The Problem Without Methods (Why Methods Exist)

Imagine your server receives **100 requests per minute**.

For each request, you need to:

- Check authentication
- Validate data
- Calculate something
- Return a response

Without methods, your code would look like:

- Repeated logic everywhere
- Hard to change
- Easy to break

Servers **must organize behavior**.

That’s why methods exist.

---

## 1️⃣ `def` — *Defining Behavior*

### Concept First

A method is:

> “A named block of behavior that can be reused”
> 

Ruby’s keyword for this is `def`.

---

### Minimal Method

**Thinking:**

> “I want one place that greets a user”
> 

```ruby
def greet
  puts "Hello"
end

```

Call it:

```ruby
greet

```

🧠 Important:

- Ruby does not need parentheses
- Method names describe **actions**

---

## 2️⃣ Method Arguments — *Passing Data In*

### The Server Problem

Requests come with data:

- Name
- ID
- Role

Your method must **receive data**.

---

### Single Argument

```ruby
def greet(name)
  puts "Hello #{name}"
end

greet("Nafis")

```

Concept:

- `name` is a local variable
- Exists only inside the method

---

### Multiple Arguments

```ruby
def create_user(name, age)
  puts "User #{name} is #{age} years old"
end

```

This mirrors real server actions.

---

## 3️⃣ Default Parameters — *Handling Missing Data*

### The Problem

Servers often receive **optional data**.

Example:

- Role not provided
- Country not provided

Without defaults:

- Errors
- Extra condition checks

---

### Ruby’s Solution → Default Parameters

```ruby
def create_user(name, role = "guest")
  puts "#{name} is a #{role}"
end

```

Usage:

```ruby
create_user("Nafis")
create_user("Nafis", "admin")

```

🧠 Server mindset:

- Default values prevent crashes
- Cleaner logic

---

## 4️⃣ Return Values — *The Big Ruby Difference*

### JS Mental Model

In JS:

```jsx
function sum(a, b) {
  return a + b;
}

```

Return is **explicit**.

---

### Ruby Mental Model

Ruby returns:

> The last evaluated expression
> 

---

### Example

```ruby
def sum(a, b)
  a + b
end

```

This method **returns** the result automatically.

---

### Why Ruby Does This

Ruby was designed to:

- Read like natural language
- Reduce noise
- Focus on *what* happens, not boilerplate

---

### Explicit `return` (When Needed)

```ruby
def check_age(age)
  return "Too young" if age < 18
  "Allowed"
end

```

Use `return` when:

- Exiting early
- Guard conditions

---

## 5️⃣ Methods vs puts (Very Important)

### Common Beginner Confusion

```ruby
def calculate_total(price)
  puts price * 2
end

```

This method:

- Prints a value
- Returns `nil`

Server code usually needs:

- **Return values**, not prints

Correct version:

```ruby
def calculate_total(price)
  price * 2
end

```

🧠 Rule:

- `puts` → debugging/logging
- return → logic/data

---

## 6️⃣ Real Server Example — Auth Check

**Thinking steps:**

1. Receive user
2. Check role
3. Return permission

```ruby
def can_access_admin_panel?(role)
  role == "admin"
end

```

Usage:

```ruby
if can_access_admin_panel?(user_role)
  puts "Access granted"
else
  puts "Access denied"
end

```

This is **real Rails-level thinking**.

---

## 7️⃣ Predicate Methods (`?`) — Ruby Convention

Ruby has a naming style:

- Methods returning boolean end with `?`

```ruby
def logged_in?
  true
end

```

This improves readability:

```ruby
if logged_in?

```

Reads like English.

---

## 8️⃣ Methods Are Objects’ Behavior (OOP Hint)

Later you’ll write:

```ruby
user.save
user.valid?
order.total_price

```

All of these are **methods** attached to objects.

This is why Ruby feels expressive.

---

## Mental Model Recap 🧠

- `def` defines behavior
- Arguments bring data in
- Defaults protect against missing data
- Last expression is returned
- `return` is for early exit
- Methods = reusable server actions

---