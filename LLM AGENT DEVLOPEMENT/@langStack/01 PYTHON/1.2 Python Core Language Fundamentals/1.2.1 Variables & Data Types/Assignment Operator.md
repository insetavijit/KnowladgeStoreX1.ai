In Python, the **assignment operator (`=`)** **binds a name to an object**; it does **not copy the value**. Its role is to establish or update a **name → object** relationship in the current scope.

When you write:

```python
x = 42
```

Python does **not** copy `42` into a variable `x`. Instead:

1. An integer object `42` exists (or is created).
    
2. The name `x` is **bound** to that object’s identity.
    

This is why assignment in Python is better read as **“bind”**, not “assign a value into a container.”

---

### **What Assignment Actually Does (Step-by-Step)**

```python
a = [1, 2, 3]
b = a
```

Internally:

- A list object `[1, 2, 3]` is created.
    
- `a` → that list object
    
- `b` → the **same** list object
    

No copying occurs. Both names reference the same object.

This behavior is uniform across Python, regardless of object type.

---

### **Why “assignment copies values” is a wrong mental model**

If assignment copied values, this would be true:

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)  # would remain [1, 2, 3]
```

But in Python, the actual output is:

```text
[1, 2, 3, 4]
```

Because:

- `=` created another **binding**
    
- Mutation affects the shared object
    
- Both names observe the same state
    

---

### **Assignment vs Copying**

Copying is **explicit** in Python and uses different mechanisms:

```python
b = a.copy()        # shallow copy
b = copy.deepcopy(a)
```

Assignment (`=`) never performs a copy.

---

### **Concept & Clarification**

#### Assignment Operator (`=`)

- Creates or updates a **name binding**
    
- Does **not** duplicate objects
    
- Operates within a **scope** (local, enclosing, global)
    
- Works identically for all object types
    

#### Reassignment

- Uses the same operator (`=`)
    
- Simply **rebinds** the name to a new object
    

```python
x = 10     # x → int(10)
x = 20     # x → int(20); old object unchanged
```

#### Mutation vs Assignment

- **Assignment** changes what the name points to
    
- **Mutation** changes the object itself
    

---

### **Assignment Operator vs Value Copy — Comparison**

|Aspect|Assignment (`=`)|Copying (explicit)|
|---|---|---|
|What happens|Name bound to object|New object created|
|Object identity|Shared|Different|
|Default behavior|Yes|No|
|Memory cost|Low|Higher|
|Mutation side effects|Visible through all references|Isolated to the copy|
|How to trigger|`=`|`.copy()`, `copy.copy`, `deepcopy`|

---

### **Code Illustration (Common Pitfall)**

```python
a = [[1, 2], [3, 4]]
b = a

b[0].append(99)
print(a)  # [[1, 2, 99], [3, 4]]
```

To avoid shared mutation:

```python
import copy
b = copy.deepcopy(a)
```

---

### **Interview One-Liner**

> _In Python, the assignment operator binds names to objects; it never copies values. Any copying must be explicit._

This answer demonstrates clear understanding of Python’s object model and immediately distinguishes Python from value-copy languages.

If you want, I can continue with:

- **Reassignment vs mutation**
    
- **Multiple assignment (`a = b = 10`)**
    
- **Assignment and scope rules**
    
- Or a **memory diagram walkthrough**