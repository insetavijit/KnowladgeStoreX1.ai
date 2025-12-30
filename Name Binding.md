### **Name Binding (Expanded Explanation)**

**Purpose**  
Name binding explains **how Python associates identifiers (names) with objects**. When you assign a variable, Python does not allocate a fixed memory box; instead, it **binds a name to an existing object** in memory.

**Core Idea**

- A **name** is an identifier stored in a namespace.
    
- An **object** is a value residing somewhere in memory.
    
- **Binding** is the association between a name and an object.
    

Python programs operate by creating, updating, and resolving these bindings.

**Key Concepts**

- **Binding operations**  
    Occur through:
    
    - Assignment (`=`)
        
    - Function and class definitions
        
    - Imports
        
    - Parameter passing in function calls
        
- **Rebinding**  
    A name can be reassigned to a different object at any time.
    
- **Multiple bindings**  
    Multiple names may reference the same object simultaneously.
    
- **Namespaces & scope**  
    Bindings live inside namespaces (local, enclosing, global, built-in), and name resolution follows the LEGB rule.
    

**Example**

```python
a = 5
b = a      # b is bound to the same object as a
a = 10     # a is rebound to a new object; b still refers to 5
```

At no point is the object `5` modified. Only the **binding of `a` changes**.

**Important Implications**

- Variables are **references**, not storage containers.
    
- Rebinding a name does **not** affect other names bound to the same object.
    
- This model explains:
    
    - Why integers and strings behave as immutable
        
    - How function arguments are passed (object references)
        
    - Why side effects occur with mutable objects (lists, dicts)
        

A correct mental model of name binding prevents confusion around copying, mutation, and unexpected behavior.