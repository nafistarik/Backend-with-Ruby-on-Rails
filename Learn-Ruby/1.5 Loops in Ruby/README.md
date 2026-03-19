---

## Why Loops Exist (Feel the Problem First)

Imagine this server task:

> Send a welcome email to 100 users
> 

Without loops, you’d have to write:

```ruby
send_email(user1)
send_email(user2)
send_email(user3)

```

This is impossible to maintain.

Servers must:

- Repeat actions
- Process lists
- Validate multiple inputs
- Generate responses

Loops solve **repetition**.

---

## Ruby Loop Philosophy (Important Mental Shift)

### JS mindset:

```jsx
for (let i = 0; i < arr.length; i++) {}

```

### Ruby mindset:

> “Do something for each element”
> 

Ruby focuses on:

- Readability
- Intent
- Less index math

---

# 1️⃣ `times` — Repeat Fixed Number of Times

### When to Use

- Retry logic
- Pagination
- Seed data
- Simple repetition

### Thinking First

> “Run this block 5 times”
> 

```ruby
5.times do
  puts "Processing request"
end

```

🧠 `5` is an object → `.times` is a method.

---

### With Index

```ruby
5.times do |i|
  puts "Attempt #{i}"
end

```

Index starts from `0`.

---

# 2️⃣ `while` — Loop While Condition Is True

### When to Use

- Polling
- Waiting for condition
- Manual counters

### Thinking

> “Keep running until something changes”
> 

```ruby
count = 0

while count < 3
  puts "Count: #{count}"
  count += 1
end

```

⚠️ Forgetting to change `count` = infinite loop.

---

# 3️⃣ `until` — Loop Until Condition Becomes True

Ruby gives **inverse logic** (very expressive).

### Thinking

> “Run until task is finished”
> 

```ruby
attempts = 0

until attempts == 3
  puts "Trying..."
  attempts += 1
end

```

Same as:

```ruby
while attempts != 3

```

---

# 4️⃣ `each` — Loop Through Collections (MOST IMPORTANT)

### Why `each` Exists

Most server work = **processing data collections**

Example:

```ruby
users = ["Nafis", "Sara", "Tom"]

```

### Thinking

> “For each user, do something”
> 

```ruby
users.each do |user|
  puts "Sending email to #{user}"
end

```

🧠 No indexes, no counters — clean intent.

---

# 5️⃣ `for` — Rarely Used (But You Should Know)

```ruby
for user in users
  puts user
end

```

⚠️ Rubyists prefer `each` because:

- Better scoping
- More idiomatic

---

# 6️⃣ `loop do` — Infinite Loop (Controlled Manually)

### When Used

- Background jobs
- Long-running workers

```ruby
loop do
  puts "Running..."
  break
end

```

Use `break` to exit.

---

# 7️⃣ Loop Control Keywords

### `break` — Stop Loop

```ruby
users.each do |user|
  break if user == "Sara"
  puts user
end

```

---

### `next` — Skip Current Iteration

```ruby
users.each do |user|
  next if user == "guest"
  puts user
end

```

---

### `redo` — Repeat Same Iteration

```ruby
retry_count = 0

begin
  retry_count += 1
  puts "Trying..."
end while retry_count < 3

```

(Rare, but exists)

---

# 8️⃣ Nested Loops — Real Server Example

### Problem:

Validate multiple users and their permissions.

```ruby
users = [
  {name: "Nafis", roles: ["admin", "editor"]},
  {name: "Sara", roles: ["user"]}
]

users.each do |user|
  user[:roles].each do |role|
    puts "#{user[:name]} has role #{role}"
  end
end

```

---

# 9️⃣ Loop vs Method Chains (Important)

Instead of:

```ruby
users.each do |u|
  puts u[:name]
end

```

Ruby allows:

```ruby
users.map { |u| u[:name] }

```

Loops evolve into **expressive pipelines**.

---

# Mental Model Summary 🧠

- `times` → repeat fixed number
- `while` → condition-controlled
- `until` → inverse condition
- `each` → collection processing (most important)
- `break` / `next` → control flow
- Ruby prefers **meaning over mechanics**

---