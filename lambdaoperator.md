# => Operator (C# Reference) #
The => token is called the lambda operator. It is used in lambda expressions to separate the input variables on the left side from the lambda body on the right side.


The => operator is read as "goes to." In the previous example, the expression is read as "Min w goes to w dot Length".

The => operator has the same precedence as the assignment operator (=) and is right-associative.

```
string[] digits = { "zero", "one", "two", "three", "four", "five", 
                    "six", "seven", "eight", "nine" };
var shortDigits = digits.Where((digit, index) => digit.Length < index);
foreach (var sD in shortDigits)
{
    Console.WriteLine(sD);
}
// Output:
// five
// six
// seven
// eight
// nine
```