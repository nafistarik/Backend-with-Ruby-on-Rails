# 1️⃣ Blocks (`do...end`, `{}`)

## ❌ Life without blocks (the problem)

Imagine you want to repeat **custom behavior** on every element of an array.

Without blocks, Ruby would need **many different methods**:

```ruby
print_names(users)
print_uppercase(users)
print_lengths(users)
```

That’s ugly and inflexible.

---

## ✅ Why blocks exist

Ruby says:

> “Instead of creating many methods, pass behavior to a method.”

That behavior is a **block**.

---

## 🧠 How to think

- A block is **anonymous code**
- It runs **inside a method**
- Method decides **when** to run it

---

## 🧪 Practice 1

```ruby
[1, 2, 3].each do |n|
  puts n * 2
end
```

### What’s happening?

- `each` controls the loop
- block controls **what to do**

✅ **Output**

```
2
4
6
```

---

## `{}` vs `do...end`

```ruby
# multi-line → do...end
[1,2,3].each do |n|
  puts n
end

# single-line → {}
[1,2,3].each { |n| puts n }
```

📌 Same behavior

📌 Style difference only

---

# 2️⃣ `yield`

## ❌ Problem without `yield`

You write a method…

But you want **caller to decide part of the logic**.

Without `yield`, you’d hardcode behavior.

---

## ✅ Why `yield` exists

`yield` lets a method **pause** and run the block passed to it.

---

## 🧠 Think like this

> “I’ll handle setup, you (caller) handle the custom logic.”

---

## 🧪 Practice 2

```ruby
def greet
  puts "Before block"
  yield
  puts "After block"
end

greet do
  puts "Hello Nafis"
end
```

✅ **Output**

```
Before block
Hello Nafis
After block
```

---

## ⚠️ Block safety

```ruby
def greet
  yield if block_given?
end
```

📌 Prevents error when no block passed

---

# 3️⃣ Symbols vs Strings (DEEP difference)

## ❌ Problem with only strings

```ruby
status = "active"
status = "active"
status = "active"
```

Each `"active"` creates **new object** → memory waste.

---

## ✅ Why symbols exist

Symbols represent **identifiers**, not text.

---

## 🧠 Key differences

| Feature       | String | Symbol      |
| ------------- | ------ | ----------- |
| Mutable       | ✅     | ❌          |
| Object reused | ❌     | ✅          |
| Memory        | More   | Less        |
| Use case      | Text   | Keys, names |

---

## 🧪 Practice 3

```ruby
puts "ruby".object_id
puts "ruby".object_id

puts :ruby.object_id
puts :ruby.object_id
```

✅ **Answer**

- String → different IDs
- Symbol → same ID

---

📌 Hash keys should be **symbols**

```ruby
user = { name: "Nafis", age: 25 }
```

---

# 4️⃣ Truthiness (`nil` & `false`)

## ❌ Confusion without knowing this

```ruby
if 0
  puts "runs?"
end
```

Surprise: it **runs**.

---

## ✅ Ruby rule

Only **two values are false**:

- `false`
- `nil`

Everything else is truthy.

---

## 🧪 Practice 4

```ruby
puts "yes" if ""
puts "yes" if 0
puts "yes" if nil
puts "yes" if false
```

✅ **Output**

```
yes
yes
# nothing
# nothing
```

---

## 🧠 Mental model

> “Unless Ruby sees nil or false, it says TRUE.”

---

# 5️⃣ Bang methods (`!`)

## ❌ Problem without bang methods

You don’t know:

- Does this method change original?
- Or return a new object?

---

## ✅ Why bang methods exist

Bang (`!`) = **danger sign**

> “This modifies the original object.”

---

## 🧪 Practice 5

```ruby
arr = [1, 2, 3]

arr.map { |n| n * 2 }
p arr
```

✅ Output

```
[1, 2, 3]
```

---

```ruby
arr.map! { |n| n * 2 }
p arr
```

✅ Output

```
[2, 4, 6]
```

📌 Not all methods have bang versions

📌 Bang means **mutation**

---

# 6️⃣ Nil handling (`nil?`, safe navigation `&.`)

## ❌ Common crash

```ruby
user = nil
puts user.name
```

💥 `NoMethodError`

---

## ✅ Ruby solution

### `nil?`

```ruby
puts user.nil?
```

✅ `true`

---

### Safe navigation `&.`

```ruby
puts user&.name
```

✅ `nil` (no crash)

---

## 🧪 Real example

```ruby
user = { name: "Nafis" }

puts user[:name]&.upcase
puts user[:age]&.to_i
```

✅ **Output**

```
NAFIS
nil
```

---

# 🧠 Final Mental Map (IMPORTANT)

- **Blocks** → pass behavior
- **yield** → execute behavior inside method
- **Symbols** → identifiers, memory efficient
- **Truthiness** → only `nil` & `false` are false
- **Bang methods** → mutate original
- **Safe navigation** → avoid nil crashes
