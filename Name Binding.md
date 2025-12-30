### **Name Binding (Expanded Explanation)**

**Purpose**  
Name binding explains **how Python associates identifiers with objects**. When a variable is assigned, Python binds the variable name to an object in memory rather than reserving a fixed storage location.

**Core Idea**

- A **name** is an entry in a namespace.
    
- An **object** is a value stored in memory.
    
- **Binding** links the name to the object.
    

**Key Concepts**

- **Binding operation:** Happens via assignment (`=`), function definitions, imports, and parameter passing.
    
- **Rebinding:** A name can later be bound to a different object.
    
- **Multiple bindings:** Multiple names can reference the same object.
    
- **Namespace scope:** Bindings exist within namespaces (local, global, built-in).
    

**Example**

```python
a = 5
b = a      # b is bound to the same object as a
a = 10     # a is rebound to a new object; b remains bound to 5
```

**Important Implications**

- Names are **references**, not containers.
    
- Changing a binding does not affect other names bound to the original object.
    
- Understanding name binding is essential to grasp **mutability**, **argument passing**, and **side effects** in Python.
    

**One-Line Recall**  
In Python, variables are names bound to objects, and rebinding changes the reference—not the underlying object.

---

Below are **additional, carefully chosen examples** that illustrate **name binding** in Python, each with a clear explanation of _what is bound_, _what changes_, and _why it matters_. These are the examples typically expected in interviews and real debugging scenarios.

---

## **Example 1 — Simple Binding and Rebinding**

```python
x = 100
x = 200
```

**Explanation**

- `x = 100` binds the name `x` to an integer object `100`.
    
- `x = 200` **rebinds** `x` to a new integer object `200`.
    
- The object `100` is unchanged and may be garbage-collected if unreferenced.
    

**Key Point**  
Reassignment does not modify objects; it changes which object the name points to.

---

## **Example 2 — Multiple Names Bound to One Object**

```python
a = 10
b = a
```

**Explanation**

- Both `a` and `b` are bound to the **same integer object** `10`.
    
- Integers are immutable, so no in-place modification is possible.
    

```python
a = 20
```

- `a` is rebound to a new object `20`.
    
- `b` remains bound to `10`.
    

**Key Point**  
Rebinding one name does not affect other names bound to the same object.

---

## **Example 3 — Mutable Object Binding**

```python
lst1 = [1, 2, 3]
lst2 = lst1
```

**Explanation**

- `lst1` and `lst2` are bound to the **same list object**.
    

```python
lst1.append(4)
```

- The list object is mutated.
    
- Both `lst1` and `lst2` now reference `[1, 2, 3, 4]`.
    

**Key Point**  
Mutation affects all names bound to the same mutable object.

---

## **Example 4 — Rebinding vs Mutation (Critical Distinction)**

```python
nums = [1, 2, 3]
nums = nums + [4]
```

**Explanation**

- `nums + [4]` creates a **new list object**.
    
- `nums` is rebound to this new object.
    
- The original list `[1, 2, 3]` remains unchanged.
    

```python
nums = [1, 2, 3]
nums += [4]
```

- `+=` mutates the existing list in place.
    

**Key Point**  
Operators can either **rebind** or **mutate**, depending on the object type.

---

## **Example 5 — Function Arguments and Name Binding**

```python
def add_item(items):
    items.append(99)

my_list = [1, 2]
add_item(my_list)
```

**Explanation**

- `items` is bound to the same list object as `my_list`.
    
- Mutation inside the function affects the original list.
    

```python
def reassign(items):
    items = [99]

reassign(my_list)
```

- `items` is rebound locally.
    
- `my_list` remains unchanged.
    

**Key Point**  
Function arguments are passed by **object reference (name binding)**, not by value.

---

## **Example 6 — Immutable Types in Functions**

```python
def increment(x):
    x += 1

n = 10
increment(n)
```

**Explanation**

- `x += 1` creates a new integer object.
    
- `x` is rebound locally.
    
- `n` is unchanged.
    

**Key Point**  
Immutability prevents accidental side effects.

---

## **Example 7 — Identity vs Equality**

```python
a = [1, 2]
b = [1, 2]
c = a
```

```python
a == b  # True
a is b  # False
a is c  # True
```

**Explanation**

- `==` compares values.
    
- `is` compares object identity (same binding).
    

**Key Point**  
Name binding explains why identical values may not be the same object.

---

## **Mental Model to Remember**

> **Python variables do not hold values.  
> They hold references to objects.**

Once this model is internalized, topics like **mutability**, **function side effects**, **copying**, and **debugging state bugs** become straightforward.

If you want, I can next:

- convert this into an **interview cheat sheet**, or
    
- add **common pitfalls & trick questions**, or
    
- extend this with **memory diagrams (conceptual, text-based)**