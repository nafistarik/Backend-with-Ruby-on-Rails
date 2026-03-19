## The Server Problem (Why Control Flow Exists)

Imagine your server receives this request:

```json
{
  "user_role": "guest",
  "logged_in": false,
  "payment_status": "pending"
}

```

The server must decide:

- Can this user access the page?
- Should we charge them?
- What response should we send?

Without **decision-making**, the server would:

- Always allow access ❌
- Always charge ❌
- Always return success ❌

That’s where **control flow** exists.

---

## 1️⃣ `if / elsif / else` — *Making Decisions*

### The Core Idea

> “If a condition is true, do this. Otherwise, do something else.”
> 

Servers live on this logic.

---

### Server Example: Authentication Check

**Thinking first (no code yet):**

- If the user is logged in → allow access
- Else → reject request

Now the Ruby expression:

```ruby
if logged_in
  puts "Access granted"
else
  puts "Access denied"
end

```

🧠 Key Ruby rule:

- Only `false` and `nil` are false
- Everything else is true

---

### Multiple Conditions (Real Server Logic)

Example:

- If admin → full access
- Else if user → limited access
- Else → no access

```ruby
if role == "admin"
  puts "Full access"
elsif role == "user"
  puts "Limited access"
else
  puts "No access"
end

```

👉 Ruby uses `elsif`, not `else if`.

---

### Why This Matters on Server

Used for:

- Authorization
- Validations
- Feature toggles
- API responses

---

## 2️⃣ `unless` — *Inverse Thinking (Very Ruby-ish)*

### The Problem `unless` Solves

Sometimes your logic is:

> “Do something only when condition is false”
> 

JS example:

```jsx
if (!loggedIn) {
  denyAccess()
}

```

Ruby reads this **more naturally**.

---

### Ruby’s Solution → `unless`

```ruby
unless logged_in
  puts "Please log in"
end

```

This literally reads:

> “Unless logged in, show message”
> 

🧠 Mental model:

- `unless` = `if NOT condition`

---

### With `else`

```ruby
unless logged_in
  puts "Access denied"
else
  puts "Welcome"
end

```

---

### Server Use Case

- Missing parameters
- Unauthorized users
- Invalid tokens

Example:

```ruby
unless token
  puts "Token missing"
end

```

---

## 3️⃣ Inline Conditionals — *Clean Server Code*

Ruby allows **one-line decisions**.

### Example: Status Code

```ruby
status = logged_in ? 200 : 401

```

But Ruby prefers:

```ruby
status = 200 if logged_in
status = 401 unless logged_in

```

👉 Very common in Rails controllers.

---

## 4️⃣ `case` — *Cleaner Multiple Conditions*

### The Problem with Many `if`s

Imagine this:

```ruby
if status == "pending"
  puts "Wait"
elsif status == "paid"
  puts "Proceed"
elsif status == "failed"
  puts "Retry"
else
  puts "Unknown"
end

```

Works — but **hard to read**.

---

### Ruby’s Cleaner Solution → `case`

```ruby
case payment_status
when "pending"
  puts "Wait"
when "paid"
  puts "Proceed"
when "failed"
  puts "Retry"
else
  puts "Unknown status"
end

```

🧠 Mental model:

- One value
- Many possible paths
- Exactly one executes

---

### Real Server Example: HTTP Status Handling

```ruby
case response_code
when 200
  puts "Success"
when 401
  puts "Unauthorized"
when 404
  puts "Not found"
else
  puts "Server error"
end

```

---

## 5️⃣ Truthiness — *Critical Server Concept*

### Ruby Rule (Memorize This)

Only:

- `false`
- `nil`

are false.

Everything else is true:

- `0` → true
- `""` → true
- `[]` → true

---

### Server Bug Example

```ruby
if user
  puts "User exists"
end

```

If `user = nil` → condition fails

If `user = {}` → condition passes

This is **intentional** and powerful.

---

## 6️⃣ Realistic Mini Server Flow

Let’s combine everything conceptually:

**Thinking steps:**

1. If user not logged in → reject
2. If admin → allow
3. Else → limited access

```ruby
unless logged_in
  puts "Unauthorized"
else
  case role
  when "admin"
    puts "Admin access"
  when "user"
    puts "User access"
  else
    puts "Guest access"
  end
end

```

This is **real Rails controller logic**, simplified.

---

## Key Takeaways (Burn This In 🔥)

- `if` → when condition is true
- `unless` → when condition is false
- `case` → clean multiple conditions
- Only `false` & `nil` are falsy
- Server logic = decision trees