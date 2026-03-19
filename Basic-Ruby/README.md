This is **Part 1 (Basic Ruby for Rails CRUD work)**.

---

# 🌍 The Story: You Join a Rails Backend Team

You open the project and see this:

```ruby
def create
  todo = Todo.create(todo_params)
  render json: todo
end
```

And you’re like:

> “I understand what this does… but how is this even written??”

So let’s rebuild your understanding from scratch.

---

# 🧩 Scene 1 — Handling Data (Object vs Hash)

### 🧠 Problem

In frontend (JS), you get data from API:

```js
const todo = {
  title: "Learn Rails",
  completed: false
}
```

You access it like:

```js
todo.title
```

---

### 🤔 Now in Ruby?

In Rails, you’ll see:

```ruby
todo = { title: "Learn Rails", completed: false }
```

Access:

```ruby
todo[:title]
```

---

### ⚠️ Wait… why `:title` instead of `"title"`?

This is **symbol** in Ruby.

```ruby
:title
```

Think of it like:

```js
// JS
"title"
```

But Ruby symbols are:

* faster
* used for keys
* used everywhere in Rails

---

### 🔁 Mental Mapping

```js
// JavaScript
todo.title
```

```ruby
# Ruby
todo[:title]
```

---

### 🧠 When You’ll See This in Rails

```ruby
params[:title]
```

That means:

> “Get title from request body”

---

# 🧩 Scene 2 — Variables & No `let`, `const`

### 🧠 Problem

In JS:

```js
const name = "Nafis"
```

---

### 🤔 In Ruby?

```ruby
name = "Nafis"
```

That’s it.

No `let`, no `const`.

---

### ⚠️ Important Difference

Ruby is:

```id="dynamic"
dynamically typed
```

So:

```ruby
name = "Nafis"
name = 10
```

Perfectly valid.

---

### 🧠 Backend Relevance

You’ll constantly see:

```ruby
todo = Todo.find(1)
```

Just simple variable assignment.

---

# 🧩 Scene 3 — Conditionals (if)

### 🧠 Problem

In JS:

```js
if (todo.completed === false) {
  console.log("Not done")
}
```

---

### 🤔 In Ruby?

```ruby
if todo[:completed] == false
  puts "Not done"
end
```

---

### ⚠️ Differences

```id="differences"
no parentheses needed
== instead of ===
must write end
puts instead of console.log
```

---

### 🧠 Cleaner Ruby Style

```ruby
unless todo[:completed]
  puts "Not done"
end
```

This means:

> “If NOT completed”

---

# 🧩 Scene 4 — Functions vs Methods

### 🧠 Problem

In JS:

```js
function greet(name) {
  return "Hello " + name
}
```

---

### 🤔 In Ruby?

```ruby
def greet(name)
  "Hello #{name}"
end
```

---

### ⚠️ Differences

```id="diff-method"
function → def
no return needed (last line auto returns)
string interpolation #{}
end required
```

---

### 🧠 Backend Example

```ruby
def create
  todo = Todo.create(...)
end
```

This is just a **method**.

---

# 🧩 Scene 5 — String Interpolation

### 🧠 Problem

In JS:

```js
const message = `Hello ${name}`
```

---

### 🤔 In Ruby?

```ruby
message = "Hello #{name}"
```

---

### 🧠 Where You'll See This

Logs, debug, responses:

```ruby
puts "Todo created: #{todo[:title]}"
```

---

# 🧩 Scene 6 — Arrays

### 🧠 Problem

In JS:

```js
const todos = ["Task 1", "Task 2"]
```

---

### 🤔 In Ruby?

```ruby
todos = ["Task 1", "Task 2"]
```

Same.

---

### Access:

```ruby
todos[0]
```

---

### Loop:

JS:

```js
todos.forEach(todo => console.log(todo))
```

Ruby:

```ruby
todos.each do |todo|
  puts todo
end
```

---

### 🧠 Mental Mapping

```js
forEach → each
```

---

# 🧩 Scene 7 — Loops (Important for reading Rails code)

### 🧠 Problem

Loop through todos.

JS:

```js
for (let todo of todos) {
  console.log(todo)
}
```

---

### 🤔 Ruby:

```ruby
todos.each do |todo|
  puts todo
end
```

---

### 🧠 You’ll See This in Rails

```ruby
todos.each do |todo|
  render json: todo
end
```

---

# 🧩 Scene 8 — Boolean & Truthy/Falsy

### 🧠 Problem

JS has weird truthy/falsy:

```js
if ("") // false
if (0)  // false
```

---

### 🤔 Ruby is simpler

Only false values:

```ruby
false
nil
```

Everything else = true

---

### 🧠 Example

```ruby
if ""
  puts "This runs"
end
```

Yes, it runs 😄

---

# 🧩 Scene 9 — nil vs null

### 🧠 Problem

JS:

```js
null
undefined
```

---

### 🤔 Ruby:

```ruby
nil
```

That’s it.

---

### 🧠 Backend Example

```ruby
todo = Todo.find_by(id: 10)

if todo.nil?
  puts "Not found"
end
```

---

# 🧩 Scene 10 — Simple Class (Very Important for Rails)

### 🧠 Problem

In JS:

```js
class Todo {
  constructor(title) {
    this.title = title
  }
}
```

---

### 🤔 Ruby:

```ruby
class Todo
  def initialize(title)
    @title = title
  end
end
```

---

### ⚠️ Differences

```id="diff-class"
constructor → initialize
this → @
```

---

### 🧠 That `@title` is instance variable

Rails models use this concept internally.

---

# 🧩 Scene 11 — The First Rails-Like Thinking

Now combine everything.

You see this:

```ruby
def create
  todo = { title: "Learn Rails", completed: false }

  if todo[:completed] == false
    puts "Creating todo"
  end

  todo
end
```

Now translate it in your head:

```id="mental"
method
→ create object
→ check condition
→ return result
```

That’s exactly what backend does.

---

# 🔁 Recap (Important)

You learned the **minimum Ruby needed for Rails CRUD work**:

```id="recap"
hash (object)
symbols (:key)
variables
conditionals (if, unless)
methods (def)
arrays
loops (each)
nil
basic class
```
