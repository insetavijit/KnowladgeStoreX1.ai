In Python, **reassignment never mutates immutable objects** such as `int`, `float`, `str`, or `tuple`. Any operation that appears to “change” an immutable value actually **creates a new object** and **rebinds the name** to that new object.

Immutability means the object’s internal state **cannot be altered after creation**. Therefore, the only way a variable associated with an immutable object can “change” is through **rebinding**, not mutation.

Example:

```python
x = 10
x = x + 1
```

What happens:

- `int(10)` remains unchanged
    
- A new object `int(11)` is created
    
- `x` is rebound to `int(11)`
    

---

### **Why immutability matters for reasoning about code**

Immutability guarantees:

- **No hidden side effects**
    
- **Safe sharing** of objects
    
- **Predictable behavior** across references
    

Example:

```python
a = "hello"
b = a

a = a.upper()

print(a)  # "HELLO"
print(b)  # "hello"
```

Because strings are immutable:

- `a.upper()` creates a new string
    
- `b` still references the original object
    

---

### **Immutability vs Mutation (Core Contrast)**

```python
# Immutable
x = 5
x += 1    # rebinding

# Mutable
lst = [1, 2]
lst += [3]  # mutation
```

Same syntax, different semantics:

- Immutable → new object
    
- Mutable → same object modified
    

---

### **Concept & Clarification**

#### Immutable Objects

- Cannot be changed after creation
    
- Examples: `int`, `float`, `str`, `tuple`, `frozenset`
    
- Operations produce new objects
    

#### Mutable Objects

- Can be changed in place
    
- Examples: `list`, `dict`, `set`
    
- Operations may mutate the object
    

---

### **Immutability and Shared References**

With immutables, shared references are safe:

```python
a = b = 100
a = 200

print(b)  # 100
```

With mutables, shared references are dangerous:

```python
a = b = []
a.append(1)

print(b)  # [1]
```

The difference exists solely because of mutability, not assignment.

---

### **Immutability Implication — Comparison**

|Aspect|Immutable Objects|Mutable Objects|
|---|---|---|
|Can be changed in place|No|Yes|
|Effect of reassignment|Name rebinds|Name may stay bound|
|Shared reference safety|Safe|Risky|
|Performance trade-off|More object creation|Less allocation, more caution|
|Common misconception|“Value changed”|“Name changed”|

---

### **Interview One-Liner**

> _Because immutable objects cannot be mutated, any apparent change in Python is actually name rebinding to a new object._

This demonstrates clear understanding of Python’s immutability model and its interaction with assignment.

Next in order: **Scope-Aware Binding**.