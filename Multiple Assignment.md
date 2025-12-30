**Multiple assignment** in Python allows **multiple names to be bound to the same object in a single statement**. The assignment operator evaluates the right-hand side **once** and then binds **each name** on the left-hand side to that **same object**.

Example:

```python
a = b = 10
```

Here:

- The integer object `10` is created (or reused).
    
- Both `a` and `b` are bound to the **same object identity**.
    

No copies are made.

---

### **What actually happens internally**

Execution order:

1. Evaluate the right-hand expression (`10`).
    
2. Bind `a` to that object.
    
3. Bind `b` to that same object.
    

This is equivalent to:

```python
tmp = 10
a = tmp
b = tmp
```

The critical point is that the object is shared.

---

### **Why multiple assignment is safe for immutables**

With immutable objects (`int`, `str`, `tuple`), sharing is harmless:

```python
a = b = 10
a = a + 1

print(a)  # 11
print(b)  # 10
```

Because:

- `a = a + 1` creates a new `int` object
    
- `a` is rebound
    
- `b` still points to the original object
    

No side effects occur.

---

### **The hidden danger with mutable objects**

With mutable objects, shared references can cause **unintended coupling**:

```python
a = b = []
a.append(1)

print(a)  # [1]
print(b)  # [1]
```

This surprises many developers because:

- Both names reference the **same list**
    
- Mutation via one name is visible through the other
    

---

### **Correct pattern for independent objects**

If you want separate objects, you must create them explicitly:

```python
a, b = [], []     # two distinct list objects
```

or

```python
a = []
b = []
```

---

### **Concept & Clarification**

#### Multiple Assignment

- RHS evaluated once
    
- LHS names all bind to the same object
    
- No implicit copying
    
- Behavior depends on object mutability
    

#### Multiple Assignment vs Tuple Unpacking

Do not confuse:

```python
a = b = [1, 2]    # shared object
```

with:

```python
a, b = [1, 2], [1, 2]  # two different objects
```

---

### **Multiple Assignment vs Independent Binding — Comparison**

|Aspect|Multiple Assignment (`a = b = x`)|Separate Assignment (`a, b = x, y`)|
|---|---|---|
|RHS evaluation|Once|Once per expression|
|Object identity|Shared|Distinct|
|Safe for immutables|Yes|Yes|
|Safe for mutables|Risky|Yes|
|Common pitfall|Accidental shared mutation|None|

---

### **Interview One-Liner**

> _Multiple assignment binds multiple names to the same object; with mutable objects, this can lead to shared-state bugs._

This answer signals awareness of Python’s object model and one of its most common real-world pitfalls.

Next in sequence: **Object Identity**.