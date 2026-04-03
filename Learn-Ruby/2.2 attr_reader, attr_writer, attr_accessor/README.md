# 1️⃣ The problem Ruby wanted to solve

## ❌ Life without `attr_*`

You already wrote this:

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

Now imagine you add more data:

```ruby
@email
@age
@role
```

You must write:

```ruby
def email
  @email
end

def age
  @age
end

def role
  @role
end
```

😵 Boilerplate. No logic. Just repetition.

Ruby hates repetition.

---

# 2️⃣ What Ruby noticed

Ruby saw a **pattern**:

```ruby
def something
  @something
end

```

And also:

```ruby
def something=(value)
  @something = value
end

```

So Ruby said:

> “Let’s generate these methods automatically.”

That’s exactly what `attr_*` does.

---

# 3️⃣ `attr_reader` — read-only access

## 🧠 What it means

> “Create a getter method for me.”

---

### Step-by-step thinking

We want:

```ruby
user.name

```

But we **do not want**:

```ruby
user.name = "other"

```

---

### Manual version

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

---

### Ruby shortcut

```ruby
class User
  attr_reader :name

  def initialize(name)
    @name = name
  end
end

```

✅ Same behavior

✅ Less code

✅ Clear intent

---

### Try in IRB

```ruby
user = User.new("nafis")
user.name        # ✅ works
user.name = "x"  # ❌ error

```

---

# 4️⃣ `attr_writer` — write-only access

## 🧠 What it means

> “Allow setting value, but not reading.”

---

### Manual version

```ruby
class User
  def name=(value)
    @name = value
  end
end

```

---

### Ruby shortcut

```ruby
class User
  attr_writer :name
end

```

---

### Try

```ruby
user = User.new("nafis")
user.name = "tarik"  # ✅ works
user.name            # ❌ error

```

📌 Rare but useful for:

- passwords
- secrets
- tokens

---

# 5️⃣ `attr_accessor` — read + write (MOST COMMON)

## 🧠 What it means

> “Create both getter and setter.”

---

### Manual version

```ruby
class User
  def name
    @name
  end

  def name=(value)
    @name = value
  end
end

```

---

### Ruby shortcut

```ruby
class User
  attr_accessor :name

  def initialize(name)
    @name = name
  end
end

```

---

### Try

```ruby
user = User.new("nafis")
user.name = "tarik"
puts user.name

```

✅ Output:

```
tarik

```

---

# 6️⃣ Important Ruby syntax detail (INTERVIEW GOLD)

Setter must use `=` **method name**:

```ruby
def name=(value)

```

And call it like:

```ruby
user.name = "new"

```

NOT:

```ruby
user.name=("new") # works but ugly

```

---

# 7️⃣ attr\_\* does NOT expose data directly

Very important:

```ruby
attr_accessor :name

```

❌ Does NOT make `@name` public

✔️ Still accessed via methods

---

# 8️⃣ You can add logic even with attr_accessor

## ❌ Common beginner fear

> “If I use attr_accessor, I lose control.”

Wrong.

---

### Override setter safely

```ruby
class User
  attr_reader :name

  def name=(value)
    @name = value.strip.capitalize
  end
end

```

---

### Try

```ruby
user.name = "  nafis  "
puts user.name

```

✅ Output:

```
Nafis

```

---

# 9️⃣ Multiple attributes at once

```ruby
attr_accessor :name, :email, :age

```

Ruby creates **6 methods** instantly.

---

# 🔥 Most important rule (MEMORIZE)

| Use             | When               |
| --------------- | ------------------ |
| `attr_reader`   | expose data safely |
| `attr_writer`   | accept input only  |
| `attr_accessor` | normal properties  |

---

# 🧠 Final mental model

```
Instance variable → private data
attr_*           → public interface

```

Or your JS analogy:

```
attr_* ≈ auto-generated getter/setter functions

```

---

# 🟢 Summary (lock it)

- Objects store data privately
- Methods expose behavior
- `attr_*` saves boilerplate
- Access is ALWAYS via methods
- Ruby enforces encapsulation
