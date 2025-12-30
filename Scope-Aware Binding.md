**Scope-aware binding** means that **name binding in Python always occurs within a specific scope**, and the scope determines **which name is bound, accessed, or rebound**. The same name can exist simultaneously in multiple scopes, each bound to a different object.

Python resolves names using the **LEGB rule**:

- **L**ocal
    
- **E**nclosing
    
- **G**lobal
    
- **B**uilt-in
    

Assignment (`=`) binds a name **in the current scope by default**, unless explicitly directed otherwise.

---

### **How scope affects assignment**

```python
x = 10  # global scope

def f():
    x = 20  # local scope
    print(x)

f()
print(x)
```

Output:

```text
20
10
```

Explanation:

- `x = 20` binds a **new local name**
    
- It does not affect the global `x`
    
- Names are resolved by scope, not by proximity
    

---

### **Why assignment creates a local binding**

Inside a function, **any assignment to a name makes it local**, unless declared otherwise.

```python
x = 10

def f():
    x = x + 1  # UnboundLocalError
```

Why this fails:

- Python sees `x =` and treats `x` as local
    
- The local `x` is referenced before being bound
    

This is not a runtime ambiguity—it is a **compile-time scope decision**.

---

### **Explicit scope control: `global` and `nonlocal`**

#### `global`

Binds the name to the module-level scope:

```python
x = 10

def f():
    global x
    x = 20
```

#### `nonlocal`

Binds the name to the nearest enclosing (non-global) scope:

```python
def outer():
    x = 10
    def inner():
        nonlocal x
        x = 20
    inner()
    print(x)

outer()  # 20
```

---

### **Concept & Clarification**

#### Scope-Aware Binding

- Assignment binds names in the **current scope**
    
- Lookup follows LEGB
    
- Rebinding does not “search upward” unless told to
    
- Prevents accidental mutation of outer scopes
    

#### Name Resolution vs Name Binding

- **Resolution**: reading a name → LEGB lookup
    
- **Binding**: assigning a name → current scope
    

---

### **Scope-Aware Binding — Comparison**

|Aspect|Name Resolution (Read)|Name Binding (Write)|
|---|---|---|
|Rule used|LEGB|Current scope only|
|Affected by assignment|No|Yes|
|Needs keyword|No|`global`, `nonlocal`|
|Common error|Rare|`UnboundLocalError`|

---

### **Why Python enforces this model**

- **Predictability** – no implicit upward rebinding
    
- **Safety** – avoids accidental global mutations
    
- **Readability** – scope behavior is explicit
    
- **Static analysis** – scope can be determined at compile time
    

---

### **Interview One-Liner**

> _In Python, assignment always binds names in the current scope, and name lookup follows the LEGB rule unless `global` or `nonlocal` is explicitly declared._

This signals strong understanding of Python’s scoping and binding rules.

Next and final item in this sequence: **Garbage Collection**.