# ?? Operator (C# Reference) #
The ?? operator is called the null-coalescing operator and is used to define a default value for nullable value types or reference types. It returns the left-hand operand if the operand is not null; otherwise it returns the right operand.


Instead of doing:
```
int? number = null;
int result = number == null ? 0 : number;
```
You can now just do:
```
int result = number ?? 0;
```


Ref: http://msdn.microsoft.com/en-us/library/ms173224.aspx


# Nullable Types (C# Programming Guide) #
Nullable types are instances of the `System.Nullable<T>` struct. A nullable type can represent the correct range of values for its underlying value type, plus an additional null value. For example, a `Nullable<Int32>`, pronounced "Nullable of Int32," can be assigned any value from -2147483648 to 2147483647, or it can be assigned the null value. A `Nullable<bool>` can be assigned the values true false, or null. The ability to assign null to numeric and Boolean types is especially useful when you are dealing with databases and other data types that contain elements that may not be assigned a value. For example, a Boolean field in a database can store the values true or false, or it may be undefined.

Ref: http://msdn.microsoft.com/en-us/library/1t3y8s4s%28v=vs.100%29.aspx