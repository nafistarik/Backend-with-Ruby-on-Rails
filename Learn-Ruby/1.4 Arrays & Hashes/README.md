---

## Why Ruby Has SO Many Collection Methods

On a server, data is constantly:

- Incoming (request params)
- Changing shape
- Being validated
- Filtered
- Transformed
- Sent back as response

Ruby gives **many small, readable methods** so you:

- Write less code
- Avoid bugs
- Express intent clearly

---

# PART 1 — ARRAYS (Deep Dive)

## 1️⃣ Creating Arrays (Different Scenarios)

```ruby
users = []
ids = [1, 2, 3]
mixed = ["Nafis", 25, true]

```

All valid — Ruby doesn’t restrict types.

---

## 2️⃣ Accessing Elements

```ruby
users = ["Nafis", "Sara", "Tom"]

users[0]      # => "Nafis"
users[-1]     # => "Tom"
users.first   # => "Nafis"
users.last    # => "Tom"

```

📌 Server use:

- First record
- Latest record
- Default selection

---

## 3️⃣ Adding Elements (Server Mutations)

```ruby
users = ["Nafis"]

users << "Sara"
users.push("Tom")
users.unshift("Admin")

```

Result:

```ruby
["Admin", "Nafis", "Sara", "Tom"]

```

---

## 4️⃣ Removing Elements

```ruby
users.pop        # removes last
users.shift      # removes first
users.delete("Sara")

```

Used when:

- Removing users
- Clearing invalid data

---

## 5️⃣ Iteration Methods (Core Server Logic)

### `each` — Do Something

```ruby
users.each do |user|
  puts "Sending email to #{user}"
end

```

Use when:

- Logging
- Side effects
- Notifications

---

### `map` — Transform Data

```ruby
names = users.map do |user|
  user.upcase
end

```

Use when:

- Formatting response
- Changing structure

---

### `select` — Filter In

```ruby
ages = [15, 20, 25, 30]

adults = ages.select { |age| age >= 18 }

```

---

### `reject` — Filter Out

```ruby
clean = ages.reject { |age| age < 18 }

```

---

### `find` / `detect` — Find One

```ruby
users = ["guest", "admin", "user"]

users.find { |u| u == "admin" }

```

Returns:

- First match
- Or `nil`

---

### `any?`, `all?`, `none?`

```ruby
roles = ["user", "admin"]

roles.any? { |r| r == "admin" }   # true
roles.all? { |r| r == "admin" }   # false
roles.none? { |r| r == "guest" }  # true

```

Used for:

- Permission checks
- Validation rules

---

### `include?`

```ruby
roles.include?("admin")

```

Very common in auth logic.

---

## 6️⃣ Aggregation — `reduce` / `inject`

### Problem:

Sum prices, count items, calculate totals.

```ruby
prices = [10, 20, 30]

total = prices.reduce(0) do |sum, price|
  sum + price
end

```

🧠 Think:

- `sum` accumulates
- `price` is current element

---

## 7️⃣ Sorting & Ordering

```ruby
scores = [50, 20, 80]

scores.sort
scores.sort.reverse

```

With objects:

```ruby
users.sort_by { |u| u[:age] }

```

---

## 8️⃣ Cleaning Data

```ruby
data = [1, nil, 2, nil, 3]

data.compact     # removes nil
data.uniq        # removes duplicates

```

---

# PART 2 — HASHES (Deep Dive)

## 9️⃣ Creating Hashes

```ruby
user = {
  name: "Nafis",
  age: 25,
  role: "admin"
}

```

---

## 🔟 Accessing & Updating

```ruby
user[:name]
user[:age] = 26
user[:active] = true

```

---

## 1️⃣1️⃣ Fetch vs []

```ruby
user[:country]        # nil
user.fetch(:country)  # KeyError
user.fetch(:country, "BD")

```

Use `fetch` when:

- Value must exist
- Defaults are needed

---

## 1️⃣2️⃣ Iterating Hash

```ruby
user.each do |key, value|
  puts "#{key} => #{value}"
end

```

---

## 1️⃣3️⃣ Hash Utility Methods

```ruby
user.keys
user.values
user.key?(:name)
user.value?("admin")

```

---

## 1️⃣4️⃣ Transforming Hashes

```ruby
user.transform_keys(&:to_s)
user.transform_values(&:to_s)

```

Used when:

- Preparing JSON
- Formatting responses

---

## 1️⃣5️⃣ Merging Hashes (Very Common)

```ruby
defaults = { role: "guest", active: true }
input = { name: "Nafis" }

user = defaults.merge(input)

```

Input overrides defaults.

---

## 1️⃣6️⃣ Nested Hashes (Real APIs)

```ruby
request = {
  user: {
    name: "Nafis",
    address: {
      city: "Dhaka",
      zip: 1207
    }
  }
}

request[:user][:address][:city]

```

---

## 1️⃣7️⃣ Arrays + Hashes Together (Real Data)

```ruby
users = [
  {name: "Nafis", role: "admin"},
  {name: "Sara", role: "user"},
  {name: "Tom", role: "admin"}
]

admins = users.select { |u| u[:role] == "admin" }
admin_names = admins.map { |u| u[:name] }

```

---

## 1️⃣8️⃣ Building Response Data

```ruby
response = {
  status: 200,
  data: admin_names,
  count: admin_names.length
}

```

This becomes JSON in Rails.

---

# Final Mental Model (Very Important)

- Arrays → collections of items
- Hashes → structured data
- Blocks → logic applied to collections
- Ruby methods → expressive intent
- Server code → transform + filter + respond

---

##