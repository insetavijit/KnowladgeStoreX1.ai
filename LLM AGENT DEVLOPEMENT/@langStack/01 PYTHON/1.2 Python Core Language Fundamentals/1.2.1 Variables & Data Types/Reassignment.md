**Reassignment** in Python means **rebinding an existing name to a different object**. The key point is that **the original object is not modified or overwritten**—only the name’s association changes.

When you reassign a variable, Python:

1. Evaluates the right-hand side to produce an object.
    
2. Updates the name to reference that new object.
    
3. Leaves the previously referenced object completely unchanged.
    

Example:

```python
x = 10      # x → int(10)
x = 20      # x → int(20)
```

Here, `int(10)` is not altered or replaced. The name `x` is simply rebound to a new object, `int(20)`.

---

### **Why reassignment is not mutation**

A common misconception is to equate reassignment with “changing a value.” In Python, **changing a value** only happens through **mutation**, and only for **mutable objects**.

Compare:

```python
# Reassignment
x = [1, 2, 3]
x = [1, 2, 3, 4]   # new list, x rebound
```

vs

```python
# Mutation
x = [1, 2, 3]
x.append(4)        # same list object mutated
```

- Reassignment → name changes target
    
- Mutation → object changes state
    

These are fundamentally different operations.

---

### **What happens to the old object?**

After reassignment:

- If **no other names reference the old object**, it becomes **eligible for garbage collection**
    
- If **other names still reference it**, it remains alive and unchanged
    

Example:

```python
a = [1, 2]
b = a
a = [3, 4]

print(b)  # [1, 2]
```

- `a` was rebound to a new list
    
- `b` still references the original list
    

This clearly demonstrates that reassignment does not affect existing objects.

---

### **Concept & Clarification**

#### Reassignment

- Uses the same operator: `=`
    
- Always results in **rebinding**
    
- Never mutates objects
    
- Applies uniformly to all types
    

#### Mutation

- Changes an object’s internal state
    
- Only possible for mutable types (`list`, `dict`, `set`)
    
- Visible through all references to that object
    

---

### **Reassignment vs Mutation — Comparison**

|Aspect|Reassignment|Mutation|
|---|---|---|
|What changes|Name → object binding|Object’s internal state|
|Affects other references|No|Yes|
|Uses `=` operator|Yes|No (method calls, item assignment)|
|Works on immutable types|Yes|No|
|Creates new object|Yes|No|

---

### **Immutability Implication (Critical Insight)**

For immutable objects like `int`, `str`, or `tuple`, **reassignment is the only possible change**:

```python
s = "hello"
s = s + " world"   # new string object
```

The original string `"hello"` is untouched. This reinforces that reassignment never mutates immutable objects—it can only rebind names.

---

### **Interview One-Liner**

> _Reassignment in Python rebinds a name to a new object; it never changes the original object._

This phrasing demonstrates precise understanding of Python’s object model and cleanly distinguishes reassignment from mutation.

When you’re ready, we can proceed **one-by-one** with the next item: **Dynamic Typing**.