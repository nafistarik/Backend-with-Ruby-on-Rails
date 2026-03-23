# 1️⃣ Variables, puts / print, object_id, scopes, data types

### Practice 1.1 — Variable & data type

**Concepts:** variable, data types, `.class`

```ruby
x = 10
y = "10"
z = 10.0

puts x.class
puts y.class
puts z.class

```

✅ **Answer**

```
Integer
String
Float

```

---

### Practice 1.2 — puts vs print

**Concepts:** puts, print

```ruby
print "Hello"
print "World"

puts "Hello"
puts "World"

```

✅ **Answer**

```
HelloWorld
Hello
World

```

📌 `print` → same line

📌 `puts` → new line

---

### Practice 1.3 — object_id

**Concepts:** object_id

```ruby
a = "ruby"
b = "ruby"

puts a.object_id
puts b.object_id

```

✅ **Answer**

- Different `object_id`s
  Because **strings are different objects**, even with same value.

---

### Practice 1.4 — Variable scope

**Concepts:** local, global, instance, class variable, constant

```ruby
$global_var = 10

class Test
  @@class_var = 20
  CONST = 30

  def initialize
    @instance_var = 40
  end

  def show
    puts $global_var
    puts @@class_var
    puts CONST
    puts @instance_var
  end
end

Test.new.show

```

✅ **Answer**

```
10
20
30
40

```

---

# 2️⃣ Conditions: if / else / elsif / unless / inline / case

### Practice 2.1 — if / elsif / else

**Concepts:** if, elsif, else

```ruby
age = 18

if age < 18
  puts "Minor"
elsif age == 18
  puts "Just adult"
else
  puts "Adult"
end

```

✅ **Answer**

```
Just adult

```

---

### Practice 2.2 — unless

**Concepts:** unless

```ruby
logged_in = false

unless logged_in
  puts "Please login"
end

```

✅ **Answer**

```
Please login

```

---

### Practice 2.3 — Inline conditional

**Concepts:** inline if

```ruby
puts "Allowed" if 5 > 3

```

✅ **Answer**

```
Allowed

```

---

### Practice 2.4 — case

**Concepts:** case

```ruby
day = "Mon"

case day
when "Mon"
  puts "Work day"
when "Sun"
  puts "Holiday"
else
  puts "Unknown"
end

```

✅ **Answer**

```
Work day

```

---

# 3️⃣ Methods, parameters, defaults, return behavior

### Practice 3.1 — Method & implicit return

**Concepts:** method, no return keyword

```ruby
def add(a, b)
  a + b
end

puts add(2, 3)

```

✅ **Answer**

```
5

```

📌 Ruby returns **last evaluated expression**

---

### Practice 3.2 — Default parameter

**Concepts:** default parameter

```ruby
def greet(name = "Guest")
  "Hello #{name}"
end

puts greet
puts greet("Nafis")

```

✅ **Answer**

```
Hello Guest
Hello Nafis

```

---

### Practice 3.3 — Multiple arguments

**Concepts:** parameters vs arguments

```ruby
def multiply(x, y)
  x * y
end

puts multiply(3, 4)

```

✅ **Answer**

```
12

```

---

# 4️⃣ Array & Hash operations

### Practice 4.1 — Array access

**Concepts:** array, index

```ruby
arr = ["a", "b", "c"]

puts arr[0]
puts arr[2]

```

✅ **Answer**

```
a
c

```

---

### Practice 4.2 — push / pop / shift / unshift

**Concepts:** array mutation

```ruby
arr = [1, 2]

arr.push(3)
arr.unshift(0)
arr.pop
arr.shift

p arr

```

✅ **Answer**

```
[1, 2]

```

---

### Practice 4.3 — each vs map

**Concepts:** each, map

```ruby
nums = [1, 2, 3]

result = nums.map { |n| n * 2 }
p result

```

✅ **Answer**

```
[2, 4, 6]

```

📌 `map` → returns new array

📌 `each` → returns original array

---

### Practice 4.4 — select / reject

**Concepts:** select, reject

```ruby
nums = [1, 2, 3, 4]

p nums.select { |n| n.even? }
p nums.reject { |n| n.even? }

```

✅ **Answer**

```
[2, 4]
[1, 3]

```

---

### Practice 4.5 — includes / any / all / none

**Concepts:** enumerable methods

```ruby
arr = [2, 4, 6]

p arr.include?(4)
p arr.any? { |n| n > 5 }
p arr.all? { |n| n.even? }
p arr.none? { |n| n < 0 }

```

✅ **Answer**

```
true
true
true
true

```

---

### Practice 4.6 — Hash access & merge

**Concepts:** hash, merge

```ruby
h1 = { name: "Nafis" }
h2 = { age: 25 }

p h1.merge(h2)

```

✅ **Answer**

```
{:name=>"Nafis", :age=>25}

```

---

# 5️⃣ Loops: times, while, until, break, next

### Practice 5.1 — times

**Concepts:** times

```ruby
3.times do |i|
  puts i
end

```

✅ **Answer**

```
0
1
2

```

---

### Practice 5.2 — while

**Concepts:** while

```ruby
i = 0

while i < 3
  puts i
  i += 1
end

```

✅ **Answer**

```
0
1
2

```

---

### Practice 5.3 — until

**Concepts:** until

```ruby
i = 0

until i == 3
  puts i
  i += 1
end

```

✅ **Answer**

```
0
1
2

```

---

### Practice 5.4 — break & next

**Concepts:** break, next

```ruby
(1..5).each do |n|
  next if n == 3
  break if n == 5
  puts n
end

```

✅ **Answer**

```
1
2
4
```

---
