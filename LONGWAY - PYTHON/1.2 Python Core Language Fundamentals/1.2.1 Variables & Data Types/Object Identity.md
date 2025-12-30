In Python, **variables reference object identities, not raw values**. An object’s **identity** is its unique existence in memory, and variable names are simply **labels bound to that identity**.

This is why two variables can:

- Refer to the **same object** (shared identity), or
    
- Refer to **different objects with equal values**
    

Example:

```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]
```

- `a` and `b` → same object identity
    
- `c` → different object, same value
    

---

### **Identity vs Equality (Critical Distinction)**

Python exposes this distinction explicitly:

```python
a is b      # True  → same identity
a == b      # True  → same value

a is c      # False → different identity
a == c      # True  → same value
```

- `is` checks **identity**
    
- `==` checks **value equality**
    

Understanding this distinction is fundamental to reasoning about mutation, side effects, and performance.

---

### **Why Python uses identity-based referencing**

Python’s design emphasizes:

- **Efficiency** – objects can be shared without copying
    
- **Clarity** – mutation is explicit and observable
    
- **Consistency** – same rules apply to all objects
    

Names never store values. They store **references to identities**.

---

### **How identity affects mutation**

```python
x = {"a": 1}
y = x

y["b"] = 2
print(x)  # {'a': 1, 'b': 2}
```

Because `x` and `y` reference the same object identity, mutation through one name is visible through the other.

Rebinding breaks the identity relationship:

```python
y = {"c": 3}
print(x)  # {'a': 1, 'b': 2}
```

---

### **Concept & Clarification**

#### Object Identity

- Every object has a unique identity during its lifetime
    
- Identity does not change
    
- Can be inspected with `id(obj)`
    
- Names reference identities, not values
    

#### Equality (`==`)

- Compares object contents
    
- Can be overridden by classes
    
- Independent of identity
    

---

### **Object Identity vs Equality — Comparison**

|Aspect|Object Identity (`is`)|Value Equality (`==`)|
|---|---|---|
|What is compared|Memory identity|Object contents|
|Operator|`is`|`==`|
|Mutability relevance|Critical|Secondary|
|Overridable|No|Yes (`__eq__`)|
|Common misuse|Comparing strings/ints with `is`|Rare|

---

### **Common Pitfall (Interview Favorite)**

```python
a = 256
b = 256
a is b  # True (implementation detail: integer caching)

a = 257
b = 257
a is b  # False (not guaranteed)
```

**Key point**:  
Never rely on `is` for value comparison. Use `is` only for:

- Identity checks
    
- `None`, `True`, `False`
    

---

### **Interview One-Liner**

> _In Python, variables reference object identities, not values; identity determines sharing and mutation behavior._

This statement demonstrates deep understanding of Python’s memory and object model.

Next item: **Immutability Implication**.