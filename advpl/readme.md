# AdvPL/TLPP Commands Documentation

## Overview
AdvPL (Advanced Protheus Language) and TLPP (TOTVS Language Plus Plus) are proprietary programming languages developed by TOTVS for building applications in the Protheus ERP ecosystem. This documentation covers the complete command set available in these languages.

## Table of Contents
- [Variable Declarations](#variable-declarations)
- [Control Flow Statements](#control-flow-statements)
- [Loop Structures](#loop-structures)
- [Function and Method Declarations](#function-and-method-declarations)
- [Object-Oriented Programming](#object-oriented-programming)
- [Web Services](#web-services)
- [Embedded Content](#embedded-content)
- [Preprocessor Directives](#preprocessor-directives)
- [Operators](#operators)
- [Data Types](#data-types)

---

## Variable Declarations

### Local Variables
Declares variables with local scope (function level).
```advpl
Local cVariable := "Hello"
Local nNumber := 10
Local lLogical := .T.
Local aArray := {}
Local dDate := Date()
```

### Private Variables
Declares variables with private scope (file level).
```advpl
Private cGlobal := "Global Value"
Private nCounter := 0
```

### Static Variables
Declares variables that maintain their value between function calls.
```advpl
Static nCallCount := 0
Static cLastUser := ""
```

### Public Variables
Declares variables with global scope across the entire application.
```advpl
Public cCompany := "01"
Public cBranch := "01"
```

### Typed Variable Declarations
Variables can be explicitly typed using the `AS` keyword.
```advpl
Local cName AS Character
Local nValue AS Numeric
Local lFlag AS Logical
Local dToday AS Date
Local aList AS Array
Local oObject AS Object
Local bBlock AS CodeBlock
Local jJson AS Json
Local vVariant AS Variant
```

---

## Control Flow Statements

### If Statement
Basic conditional execution.
```advpl
If lCondition
    // Code block
ElseIf lOtherCondition
    // Alternative code block
Else
    // Default code block
EndIf
```

### Do Case Statement
Multi-way conditional branching.
```advpl
Do Case
    Case nValue == 1
        // Code for case 1
    Case nValue == 2
        // Code for case 2
    Case nValue >= 10
        // Code for range
    Otherwise
        // Default case
EndCase
```

---

## Loop Structures

### For Loop
Numeric iteration loop.
```advpl
For nI := 1 To 10
    // Loop body
Next nI

// With step
For nI := 1 To 100 Step 5
    // Loop body
Next nI
```

### While Loop
Condition-based loop.
```advpl
While lCondition
    // Loop body
    // Update condition
End
```

### Loop Control
```advpl
Loop    // Continue to next iteration
Exit    // Break out of loop
```

---

## Function and Method Declarations

### Function Declaration
```advpl
Function MyFunction(cParam1, nParam2, lParam3)
    Local cResult := ""
    
    // Function body
    
Return cResult
```

### Static Function Declaration
```advpl
Static Function MyStaticFunction(cParam)
    Local cResult := ""
    
    // Function body
    
Return cResult
```

### Main Function
Entry point for applications.
```advpl
Function Main()
    // Application entry point
Return
```

### User Function
User-defined functions (legacy format).
```advpl
User Function MyUserFunc()
    // User function body
Return
```

---

## Object-Oriented Programming

### Class Declaration
```advpl
Class MyClass
    Data cProperty
    Data nValue
    
    Method New() Constructor
    Method SetValue(nNewValue)
    Method GetValue()
EndClass
```

### Method Implementation
```advpl
Method New() Class MyClass
    ::cProperty := ""
    ::nValue := 0
Return Self

Method SetValue(nNewValue) Class MyClass
    ::nValue := nNewValue
Return Nil

Method GetValue() Class MyClass
Return ::nValue
```

### Class Inheritance
```advpl
Class MyDerivedClass From MyClass
    Data cNewProperty
    
    Method New() Constructor
    Method SpecialMethod()
EndClass
```

---

## Web Services

### WSService Declaration
```advpl
WSService MyService Description "My Web Service"
    WSData cParam AS String
    WSData nValue AS Integer
    
    WSMethod MyMethod Description "Method Description"
EndWSService
```

### WSMethod Implementation
```advpl
WSMethod MyMethod WSReceive cParam, nValue WSService MyService
    // Method implementation
Return .T.
```

### WSStruct Declaration
```advpl
WSStruct MyStruct
    WSData cField1 AS String
    WSData nField2 AS Integer
    WSData lField3 AS Boolean Optional
    WSData aField4 AS Array Of String
EndWSStruct
```

### WSClient and WSRestful
```advpl
WSClient MyClient
WSRestful MyRestful
```

---

## Embedded Content

### JavaScript Content
```advpl
BeginContent Var cJSCode As JavaScript
    function myFunction() {
        console.log("Hello from JavaScript");
        return %cAdvPLVariable%;
    }
EndContent
```

### TypeScript Content
```advpl
BeginContent Var cTSCode As TypeScript
    interface MyInterface {
        name: string;
        value: number;
    }
    
    function processData(data: MyInterface): string {
        return `${data.name}: ${data.value}`;
    }
EndContent
```

### HTML Content
```advpl
BeginContent Var cHTMLCode As HTML
    <div class="container">
        <h1>%cTitle%</h1>
        <p>%cContent%</p>
    </div>
EndContent
```

### CSS Content
```advpl
BeginContent Var cCSSCode As CSS
    .my-class {
        color: %cTextColor%;
        font-size: 14px;
    }
EndContent
```

### JSON Content
```advpl
BeginContent Var cJSONCode As JSON
    {
        "name": "%cName%",
        "value": %nValue%,
        "active": %lActive%
    }
EndContent
```

### XML Content
```advpl
BeginContent Var cXMLCode As XML
    <root>
        <item name="%cName%" value="%nValue%" />
    </root>
EndContent
```

---

## Preprocessor Directives

### Include Directive
```advpl
#Include "protheus.ch"
#Include "fileio.ch"
```

### Define Directive
```advpl
#Define MY_CONSTANT 100
#Define CRLF Chr(13) + Chr(10)
```

### Conditional Compilation
```advpl
#IfDef DEBUG
    // Debug code
#Else
    // Release code
#EndIf

#IfNDef PRODUCTION
    // Development code
#EndIf
```

### Command Translation
```advpl
#XCommand DEFAULT <var> TO <value> => If(<var> == Nil, <var> := <value>, Nil)
#XTranslate UPPER(<string>) => Upper(<string>)
```

---

## Operators

### Assignment Operators
```advpl
:=      // Assignment
+=      // Add and assign
-=      // Subtract and assign
*=      // Multiply and assign
/=      // Divide and assign
%=      // Modulo and assign
++      // Increment
--      // Decrement
```

### Comparison Operators
```advpl
==      // Equal
!=      // Not equal
<>      // Not equal (alternative)
<       // Less than
<=      // Less than or equal
>       // Greater than
>=      // Greater than or equal
```

### Logical Operators
```advpl
.AND.   // Logical AND
.OR.    // Logical OR
.NOT.   // Logical NOT
AND     // Alternative AND
OR      // Alternative OR
```

### Arithmetic Operators
```advpl
+       // Addition
-       // Subtraction
*       // Multiplication
/       // Division
%       // Modulo
**      // Exponentiation
```

### String Operators
```advpl
+       // String concatenation
$       // Substring search
```

---

## Data Types

### Basic Data Types
- **Character/String**: Text data
- **Numeric**: Integer and floating-point numbers
- **Logical**: Boolean values (.T. or .F.)
- **Date**: Date values
- **Array**: Indexed collections
- **Object**: Object instances
- **CodeBlock**: Executable code blocks
- **Json**: JSON data structures
- **Variant**: Variable type that can hold any data type

### Special Constants
```advpl
.T.         // True
.F.         // False
Nil         // Null/undefined value
Space(n)    // String of n spaces
Replicate(c, n)  // Character c repeated n times
```

---

## Advanced Features

### Dialog and User Interface
```advpl
Activate Dialog oDlg Centered
Define Dialog oDlg Title "My Dialog" From 0,0 To 200,300 Pixel
```

### Database Operations
```advpl
Select Area
Use Table
From Table
Where Condition
```

### Special Keywords
```advpl
Default     // Default parameter values
Optional    // Optional parameters
Pixel       // UI measurement unit
Centered    // UI positioning
Get         // Input controls
```

---

## Best Practices

1. **Variable Naming**: Use Hungarian notation (c for Character, n for Numeric, l for Logical, etc.)
2. **Function Documentation**: Use Protheus.doc format for function documentation
3. **Error Handling**: Implement proper error handling in functions
4. **Code Organization**: Use static functions for internal operations
5. **Memory Management**: Be mindful of array and object creation

---

## Example: Complete Function with Documentation

```advpl
/*/{Protheus.doc} CalculateTotal
    Calculates the total value including taxes
    @type  Function
    @author Developer Name
    @since 01/01/2025
    @version 1.0
    @param nValue, Numeric, Base value for calculation
    @param nTaxRate, Numeric, Tax rate percentage
    @return nTotal, Numeric, Total value including taxes
    @example
    nResult := CalculateTotal(100, 10) // Returns 110
    @see (related_functions)
/*/
Function CalculateTotal(nValue, nTaxRate)
    Local nTotal := 0
    
    Default nValue   := 0
    Default nTaxRate := 0
    
    If nValue > 0 .And. nTaxRate >= 0
        nTotal := nValue + (nValue * nTaxRate / 100)
    EndIf
    
Return nTotal
```

This documentation provides a comprehensive overview of AdvPL/TLPP commands and syntax. The language supports both procedural and object-oriented programming paradigms, with special features for ERP development and web services integration.
