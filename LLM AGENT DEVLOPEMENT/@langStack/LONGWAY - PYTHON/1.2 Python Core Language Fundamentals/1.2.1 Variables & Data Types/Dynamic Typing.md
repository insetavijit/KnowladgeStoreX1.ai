**Dynamic typing** in Python means that **types are associated with objects, not with variable names**. A single variable name can therefore be **rebound to objects of different types over its lifetime** without any prior declaration or type constraint.

In other words, Python determines an object’s type **at runtime**, and names simply reference whatever object they are currently bound to.

Example:

```python
x = 10        # x → int
x = "ten"     # x → str
x = [10]      # x → list
```

The name `x` itself never has a fixed type. Only the objects it references do.

---

### **How dynamic typing works internally**

At runtime:

1. The right-hand side expression is evaluated.
    
2. An object is produced, with a concrete type (`int`, `str`, `list`, etc.).
    
3. The name is bound to that object.
    

Rebinding does **not** require type compatibility checks between the old and new objects, because the name carries no type information.

---

### **Why this is different from statically typed languages**

In statically typed languages (e.g., Java, C++):

- Variables have fixed types
    
- Rebinding to a different type is illegal
    
- Types are checked at compile time
    

In Python:

- Names are untyped
    
- Objects are strongly typed
    
- Type errors surface **only when invalid operations are attempted**
    

Example:

```python
x = 10
x = "ten"
x + 1   # TypeError at runtime
```

The error occurs because the **operation** is invalid for the object type, not because reassignment was forbidden.

---

### **Concept & Clarification**

#### Dynamic Typing

- Type checking happens at **runtime**
    
- Names can be rebound to any object
    
- Enables flexible, expressive code
    
- Shifts some error detection from compile time to execution time
    

#### Strong Typing (Important distinction)

Python is **dynamically typed but strongly typed**:

- You cannot implicitly mix incompatible types
    
- Python does not silently coerce unrelated types
    

```python
"10" + 1  # TypeError (no implicit coercion)
```

---

### **Benefits of dynamic typing**

- **Rapid prototyping** and concise code
    
- Less boilerplate (no type declarations)
    
- Natural fit for polymorphic behavior
    
- Easier refactoring during early development
    

---

### **Trade-offs and risks**

- Errors discovered later (at runtime)
    
- Harder to reason about large codebases without discipline
    
- Tooling needs help (linters, type checkers)
    

This is why modern Python often pairs dynamic typing with **type hints**:

```python
def add(x: int, y: int) -> int:
    return x + y
```

Type hints improve readability and tooling but do **not** change runtime behavior.

---

### **Dynamic Typing vs Static Typing — Comparison**

|Aspect|Dynamic Typing (Python)|Static Typing (e.g., Java)|
|---|---|---|
|When types are checked|Runtime|Compile time|
|Variable type|None (names are untyped)|Fixed|
|Rebinding to new type|Allowed|Disallowed|
|Error detection|Later|Earlier|
|Flexibility|High|Lower|

---

### **Interview One-Liner**

> _Python is dynamically typed because types belong to objects, not variable names; names can be rebound to any type at runtime._

This answer shows clarity on Python’s typing model and avoids the common misconception that “Python has weak typing.”

Next, we proceed to **Multiple Assignment (`a = b = 10`)** when you’re ready.