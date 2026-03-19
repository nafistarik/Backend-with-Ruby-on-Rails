# 💎 Starter 2 (Basic Ruby for Rails CRUD work)

---

# 🌍 Story Continues — You Open a Real Controller

You now see this:

```ruby
def index
  todos = Todo.where(completed: false).order(created_at: :desc)
  render json: todos
end
```

And your brain goes:

> “Where is the loop? Where is the filtering logic? How is this even working?”

Let’s break the “magic”.

---

# 🧩 Scene 1 — Method Chaining (Feels like Array.filter + sort)

### 🧠 Problem (JS Thinking)

In JS, you’d write:

```js
const todos = allTodos
  .filter(todo => todo.completed === false)
  .sort((a, b) => b.createdAt - a.createdAt)
```

---

### 🤔 Ruby / Rails Way

```ruby
todos = Todo.where(completed: false).order(created_at: :desc)
```

---

### ⚠️ What’s happening?

```id="chain"
where → filter
order → sort
```

Each method returns something, and the next method continues.

---

### 🧠 Mental Mapping

```js
filter → where
sort   → order
```

---

### 🔥 Why this matters

Backend developers don’t manually loop data.

They **ask the database** to do it.

---

# 🧩 Scene 2 — Blocks (`do |x| ... end`)

This is the **most confusing part for JS devs**.

---

### 🧠 Problem

In JS:

```js
todos.forEach(todo => {
  console.log(todo)
})
```

---

### 🤔 Ruby:

```ruby
todos.each do |todo|
  puts todo
end
```

---

### ⚠️ What is `|todo|`?

Think of it like:

```js
(todo) => {}
```

---

### 🧠 Another Example

```ruby
[1,2,3].each do |num|
  puts num * 2
end
```

JS version:

```js
[1,2,3].forEach(num => console.log(num * 2))
```

---

### 🔥 Why this matters in Rails

You’ll see blocks everywhere:

```ruby
params.each do |key, value|
  puts key
end
```

---

# 🧩 Scene 3 — Strong Params (Very Important for CRUD)

### 🧠 Problem

Frontend sends:

```json
{
  "title": "Learn Rails",
  "completed": false
}
```

---

In JS backend (Express), you’d do:

```js
const { title, completed } = req.body
```

---

### 🤔 Rails Way

```ruby
params.require(:todo).permit(:title, :completed)
```

---

### ⚠️ Why this exists?

Security.

Rails **does not trust incoming data**.

---

### 🧠 Mental Mapping

```js
req.body.title → params[:title]
```

But Rails forces you to whitelist:

```ruby
permit(:title, :completed)
```

---

### 🔥 Real Controller Example

```ruby
def create
  todo = Todo.create(todo_params)
  render json: todo
end

private

def todo_params
  params.require(:todo).permit(:title, :completed)
end
```

---

### 🧠 Translate to your thinking

```id="mental-params"
get request data
validate allowed fields
create database entry
return response
```

---

# 🧩 Scene 4 — ActiveRecord (The “Magic” Layer)

### 🧠 Problem

In SQL:

```sql
SELECT * FROM todos WHERE completed = false;
```

---

### 🤔 Rails:

```ruby
Todo.where(completed: false)
```

---

### ⚠️ What is this?

This is:

> Ruby code → converted into SQL → executed in database

---

### 🧠 More Examples

```ruby
Todo.all
Todo.find(1)
Todo.create(title: "Task")
Todo.update(completed: true)
Todo.destroy
```

---

### 🧠 JS Comparison

In JS backend (without ORM):

```js
db.query("SELECT * FROM todos")
```

Rails removes SQL writing.

---

### 🔥 Why this matters

This is what backend engineers mean when they say:

```id="terms"
query
model
ORM
```

---

# 🧩 Scene 5 — Symbols Everywhere (`:something`)

You saw:

```ruby
completed: false
```

That is actually:

```ruby
:completed => false
```

---

### 🧠 JS Equivalent

```js
{ completed: false }
```

---

### ⚠️ Why Rails uses symbols?

* faster
* immutable
* used as keys internally

---

### 🧠 Where you’ll see this

```ruby
order(created_at: :desc)
```

Means:

```id="translate"
sort by created_at descending
```

---

# 🧩 Scene 6 — Before Actions (Middleware Thinking)

### 🧠 Problem

In Express (JS):

```js
app.use((req, res, next) => {
  console.log("middleware")
  next()
})
```

---

### 🤔 Rails Equivalent

```ruby
before_action :set_todo, only: [:show, :update, :destroy]
```

---

### ⚠️ What is this?

Before running:

```ruby
show
update
destroy
```

Run:

```ruby
set_todo
```

---

### 🧠 Example

```ruby
def set_todo
  @todo = Todo.find(params[:id])
end
```

---

### 🔥 Why this matters

This is Rails version of:

```id="middleware-mental"
middleware
pre-processing
shared logic
```

---

# 🧩 Scene 7 — Instance Variables (`@todo`)

### 🧠 Problem

You see:

```ruby
@todo = Todo.find(params[:id])
```

Why `@`?

---

### 🤔 Meaning

`@todo` = instance variable

Accessible across methods.

---

### 🧠 Example

```ruby
def show
  render json: @todo
end
```

---

### ⚠️ JS Comparison

JS doesn’t use this pattern directly.

Closest:

```js
this.todo
```

---

### 🔥 Why Rails uses it

To share data between methods.

---

# 🧩 Scene 8 — Render JSON (Response)

### 🧠 Problem

In JS:

```js
res.json(todo)
```

---

### 🤔 Rails:

```ruby
render json: todo
```

---

### 🧠 That’s it.

Same concept.

---

# 🧩 Scene 9 — The Full Real Controller (Now You Can Read It)

Now look again:

```ruby
class TodosController < ApplicationController
  before_action :set_todo, only: [:show, :update, :destroy]

  def index
    todos = Todo.all
    render json: todos
  end

  def show
    render json: @todo
  end

  def create
    todo = Todo.create(todo_params)
    render json: todo
  end

  def update
    @todo.update(todo_params)
    render json: @todo
  end

  def destroy
    @todo.destroy
    head :no_content
  end

  private

  def set_todo
    @todo = Todo.find(params[:id])
  end

  def todo_params
    params.require(:todo).permit(:title, :completed)
  end
end
```

---

# 🧠 Now Translate Everything (Your Brain Should Do This)

```id="mental-flow"
request comes in
→ route matches
→ controller method runs
→ maybe before_action runs
→ database query via model
→ result returned
→ JSON response sent
```

---

# 🔁 Final Recap (What You Actually Need)

You now understand the **core Rails + Ruby concepts needed for CRUD work**:

```id="final-recap"
method chaining (where, order)
blocks (each do)
strong params (permit)
ActiveRecord queries
symbols (:key)
before_action (middleware)
instance variables (@todo)
render json
```

---

