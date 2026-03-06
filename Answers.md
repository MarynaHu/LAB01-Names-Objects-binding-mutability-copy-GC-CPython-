**Answers**

**A) Binding / Rebinding** 

When we do a \= 2, the name a is rebind to a new object with the value 2\. Since names in Python are just bindings, the name b continues to refer to the original object (3), which has not been changed.

**B) Mutation vs Rebinding** 

Both names a and b refer to the same list object in memory. Mutating (append) changes the contents of the object itself, so the changes are visible through both references. With rebinding, we would simply force one of the names to point to the other object.

**C) Function arguments** 

When an object is passed to a function, it is bound, not copied, meaning the function does not receive a duplicate of the object, but a reference to the original. Inside a function, parameters are new local names that point to the same object in memory as the caller's variable. Since both the local parameter and the external variable refer to the same object, any change to the internal state of the object will be visible outside, so mutation inside the function affects the caller. However, if we assign a completely new value to the parameter, we only change what the local name points to, without touching the original object, and so rebinding inside the function does not affect the caller.

**D) Default argument behavior**

The list keeps growing because in Python, default values are evaluated once when the function is defined, not each time the function is called. When def f2(x \= \[\]): is executed, a single list object is created in memory and stored as the default value. Because lists are mutable, calling .append(1) modifies this specific list object in place. On subsequent calls to the function without arguments, a new list is not created; instead, the same object is reused across calls. Therefore, every call simply adds another element to the single, shared list object, causing it to grow.

**E) Copy semantics** 

A shallow copy creates a new top-level object, but inserts references (bindings) to the exact same nested objects found in the original. Because the nested objects are shared, modifying a mutable nested object through the shallow copy will also change the original.  
A deep copy creates a new top-level object and recursively creates full copies of all nested objects. This breaks all references to the original data, meaning the new compound object and its nested objects are completely independent. Modifications to the deep copy will not affect the original.

**F) Reference counting / GC**

The reference count for the integer 5 looks unusually high because of a specific CPython optimization. Small integers (typically from \-5 to 256\) are used so frequently that CPython pre-allocates them at startup to save memory and improve performance. CPython introduced immortal objects for such deeply cached values, giving them an artificially huge reference count so the garbage collector never attempts to delete them. However, it is important to note that this behavior is strictly an implementation detail (not guaranteed by Python language specification). Other Python implementations, like PyPy, might handle memory for integers completely differently.  
