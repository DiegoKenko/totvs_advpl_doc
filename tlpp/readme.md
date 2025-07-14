# TLPP Header Files Documentation

This document provides comprehensive documentation for TLPP (TOTVS Language Plus Plus) header files (.th) found in the decompressed TOTVS include files. These headers define modern language features, annotations, and advanced object-oriented constructs for TLPP development.

## Overview

TLPP Header files (.th) contain:

- **Modern Language Features** - Enhanced syntax and constructs beyond traditional AdvPL
- **Annotation System** - Decorators for REST endpoints, documentation, and metadata
- **Advanced Object-Oriented Programming** - Interfaces, inheritance, and method overriding
- **Framework Integration** - Integration with TOTVS Framework components
- **REST API Annotations** - Built-in support for RESTful web service development

---

## Table of Contents

1. [Core TLPP Features](#core-tlpp-features)
2. [Object-Oriented Programming](#object-oriented-programming)
3. [REST API Annotations](#rest-api-annotations)
4. [Framework Integration](#framework-integration)
5. [Documentation System](#documentation-system)
6. [Internationalization](#internationalization)
7. [Probat System](#probat-system)
8. [Authentication & Authorization](#authentication--authorization)
9. [Environment Management](#environment-management)
10. [Best Practices](#best-practices)

---

## Core TLPP Features

**Source:** `tlpp-core.th`, `fw-tlpp-core.th`

### Main TLPP Core Includes
```tlpp
#include "tlpp-object.th"
#include "tlpp-rest.th"
```

**Purpose:** Central header that includes TLPP framework components.

---

## Object-Oriented Programming

**Source:** `tlpp-object.th`, `fw-tlpp-object.th`

### Enhanced Class Definition

#### CLASS with Inheritance and Interfaces
```tlpp
CLASS MyClass INHERIT FROM BaseClass IMPLEMENTS IInterface  
ENDCLASS
```

#### CLASS with Multiple Interfaces
```tlpp
CLASS MyClass 
    INHERIT FROM BaseClass 
    IMPLEMENTS IInterface1, IInterface2, IInterface3
ENDCLASS
```

#### INTERFACE Definition
```tlpp
INTERFACE IMyInterface
    METHOD DoSomething()
    METHOD GetValue() AS Numeric
ENDINTERFACE
```

### Advanced Data Members

#### Variable Declaration with Scope
```tlpp
    VAR cProperty AS Character PUBLIC DEFAULT ""
    VAR nValue AS Numeric  
    DATA lFlag AS Logical 
    DATA oObject AS Object 
    INSTVAR aList AS Array 
    VAR aList1 AS Array 
```

### Enhanced Default Values

#### BYNAME Assignment
```tlpp
BYNAME cName, nAge, lActive
BYNAME cEmail DEFAULT "default@email.com"
BYNAME oObject IFNONIL
```

#### BYDEFAULT Function
```tlpp
cValue := BYDEFAULT cParameter, "default_value"
```

---

## REST API Annotations

**Source:** `tlpp-rest.th`, `fw-tlpp-rest.th`


---

## Framework Integration

**Source:** `fw-tlpp-*.th`

### Framework Object Extensions
```tlpp
CLASS MyFrameworkClass INHERIT FROM FWClass
    DATA cVersion AS Character DEFAULT "1.0"
    
    METHOD Initialize() CONSTRUCTOR
    METHOD Process() AS Logical
ENDCLASS
```

### Framework REST Integration
```tlpp
CLASS MyRestService INHERIT FROM FWRestService
    @Get(endpoint="/endpoint/get")
    @Post(endpoint="/endpoint/post")
    METHOD GetStatus() AS Object
ENDCLASS
```

### HTTP Method Annotations

#### @Get Annotation
```tlpp
@Get(endpoint="/api/customers/:id", 
     description="Get customer by ID",
     title="Customer Details",
     params="id:path:Customer ID",
     responses="200:Customer object")
METHOD GetCustomer(cId AS Character) AS Object
```

#### @Post Annotation
```tlpp
@Post(endpoint="/api/customers",
      description="Create new customer",
      requestBody="Customer object",
      responses="201:Created customer")
METHOD CreateCustomer(oCustomer AS Object) AS Object
```

#### @Put Annotation
```tlpp
@Put(endpoint="/api/customers/:id",
     description="Update customer",
     params="id:path:Customer ID",
     requestBody="Customer object")
METHOD UpdateCustomer(cId AS Character, oCustomer AS Object) AS Object
```

#### @Delete Annotation
```tlpp
@Delete(endpoint="/api/customers/:id",
        description="Delete customer",
        params="id:path:Customer ID",
        responses="204:No content")
METHOD DeleteCustomer(cId AS Character) AS Logical
```

#### @Patch Annotation
```tlpp
@Patch(endpoint="/api/customers/:id",
       description="Partial customer update",
       params="id:path:Customer ID",
       requestBody="Partial customer object")
METHOD PatchCustomer(cId AS Character, oData AS Object) AS Object
```

#### Annotation Properties

```
- **endpoint** - API endpoint URL pattern
- **description** - Method description for documentation
- **title** - Display title for the endpoint
- **params** - Parameter definitions (format: "name:type:description")
- **requestBody** - Request body schema description
- **responses** - Response codes and descriptions
- **id** - Numeric identifier for the endpoint
- **language** - Language code (default: "BRA")
```
---

## Internationalization

**Source:** `tlpp-i18n.th`, `fw-tlpp-i18n.th`

### I18N Support

#### Language Resources
```tlpp
@I18N(key="msg.welcome", 
      default="Welcome",
      languages={"pt":"Bem-vindo", "en":"Welcome", "es":"Bienvenido"})

@I18N(key="error.validation",
      default="Validation error",
      languages={"pt":"Erro de validação", "en":"Validation error"})
```

#### Runtime I18N Usage
```tlpp
cMessage := GetI18NText("msg.welcome", cLanguage)
cError := GetI18NText("error.validation", "pt")
```

---

## Probat System

**Source:** `tlpp-probat.th`, `fw-tlpp-probat.th`

### Test Annotations

#### @Test Annotation
```tlpp
@Test(description="Test customer creation",
      group="CustomerTests",
      timeout=5000)
METHOD TestCreateCustomer() AS Logical
```

#### @TestSetup and @TestTeardown
```tlpp
@TestSetup
METHOD SetupTest() AS Nil

@TestTeardown  
METHOD CleanupTest() AS Nil
```

#### Test Assertions
```tlpp
@Test
METHOD TestValidation() AS Logical
    Local oCustomer := CreateCustomer()
    Local lResult := ValidateCustomer(oCustomer)
    
    AssertTrue(lResult, "Customer should be valid")
    AssertEquals(oCustomer:cName, "Test Customer")
RETURN .T.
```

---

## Authentication & Authorization

**Source:** `framework.authentication.oidc.th`

### OIDC Authentication

#### Authentication Configuration
```tlpp
@Auth(type="OIDC",
      provider="https://auth.company.com",
      clientId="app-client-id",
      scopes={"read", "write", "admin"})
CLASS SecureService
```

#### Method Security
```tlpp
@RequireAuth(scopes={"admin"})
@Delete(endpoint="/api/admin/users/:id")
METHOD DeleteUser(cUserId AS Character) AS Logical
```

---

## Environment Management

**Source:** `framework.environment.type.th`

### Environment Types

#### Environment Annotations
```tlpp
@Environment(type="PRODUCTION", 
             config="prod-config.json")
@Environment(type="DEVELOPMENT",
             config="dev-config.json")
CLASS ConfigurableService
```

#### Conditional Compilation
```tlpp
#ifdef PRODUCTION
    @Log(level="ERROR")
#else
    @Log(level="DEBUG")
#endif
METHOD ProcessData() AS Logical
```

---

## Model & Structure Integration

**Source:** `totvs.framework.*.th`

### Framework Model Integration

#### Model Events
```tlpp
@ModelEvent(event="BeforeInsert")
METHOD OnBeforeInsert(oModel AS Object) AS Logical

@ModelEvent(event="AfterUpdate") 
METHOD OnAfterUpdate(oModel AS Object) AS Nil
```

#### Structure Interfaces
```tlpp
INTERFACE IModelStructure
    METHOD GetFields() AS Array
    METHOD Validate() AS Logical
    METHOD Serialize() AS Character
ENDINTERFACE
```


---

## Usage Examples

### Complete REST Service Example
```tlpp

CLASS CustomerAPI INHERIT FROM FWRestService

    @Get(endpoint="/", description="List all customers")
    METHOD ListCustomers() AS Array
        Local aCustomers := {}
        // Implementation
    RETURN aCustomers

    @Post(endpoint="/", description="Create customer")
    METHOD CreateCustomer(oCustomer AS Object) AS Object
        Local oResult := {}
        // Validation and creation logic
    RETURN oResult

    @Get(endpoint="/:id", description="Get customer by ID")
    METHOD GetCustomer(cId AS Character) AS Object
        Local oCustomer := {}
        // Fetch customer logic
    RETURN oCustomer

ENDCLASS
```

### Advanced OOP Example
```tlpp

INTERFACE ICustomerService
    METHOD Create(oCustomer AS Object) AS Object
    METHOD Update(cId AS Character, oCustomer AS Object) AS Object
    METHOD Delete(cId AS Character) AS Logical
ENDINTERFACE

CLASS CustomerService IMPLEMENTS ICustomerService
    DATA oRepository AS Object 
    DATA oValidator AS Object 
    
    METHOD New() CONSTRUCTOR
        ::oRepository := CustomerRepository():New()
        ::oValidator := CustomerValidator():New()
    RETURN Self
    
    METHOD Create(oCustomer AS Object) AS Object
        Local oResult := {}
        
        If ::oValidator:Validate(oCustomer)
            oResult := ::oRepository:Save(oCustomer)
        Else
            oResult:lError := .T.
            oResult:cMessage := "Validation failed"
        EndIf
        
    RETURN oResult

    METHOD Delete(cId AS Character) AS Logical
        Local lSuccess := .F.
        
        If !Empty(cId)
            lSuccess := ::oRepository:Delete(cId)
        EndIf
    RETURN

    METHOD Update(cId AS Character, oCustomer AS Object) AS Object
        Local oResult := {}
        
        If ::oValidator:Validate(oCustomer)
            oResult := ::oRepository:Update(cId, oCustomer)
        Else
            oResult:lError := .T.
            oResult:cMessage := "Validation failed"
        EndIf
    RETURN

ENDCLASS
```

---

## File Reference Index

- **tlpp-core.th** - Main TLPP framework includes
- **tlpp-object.th** - Enhanced object-oriented programming
- **tlpp-rest.th** - REST API annotations and definitions
- **tlpp-doc.th** - Documentation system annotations
- **tlpp-i18n.th** - Internationalization support
- **tlpp-probat.th** - Testing framework annotations
- **fw-tlpp-*.th** - Framework-specific TLPP extensions
- **framework.authentication.oidc.th** - OIDC authentication
- **framework.environment.type.th** - Environment management
- **totvs.framework.*.th** - TOTVS framework integration
