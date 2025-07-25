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


# TLPP - Structure, Types, Modifiers and Features

Documentation prioritizing official TOTVS TLPP information:

## Index

1. TLPP Class Structure
2. Access Modifiers
3. Property Typing and Native Types
4. Interfaces
5. Operator Overloading
6. Calling Parent Class Constructor
7. Practical Examples

---

## 1. TLPP Class Structure

```tlpp
#include "tlpp-core.th"

Class MyClass
EndClass
```

### Properties and Methods

```tlpp
Class MyClass
    PUBLIC DATA cProperty AS Character 
    PUBLIC DATA nValue AS Numeric  
    PUBLIC DATA lFlag AS Logical 
    PUBLIC DATA oObject AS Object 
EndClass
```

---

## 2. Modificadores de Acesso

TLPP permite definir escopos para propriedades e métodos:

| Modificador | Descrição |
|---|---|
| PRIVATE | Acesso apenas dentro da classe |
| PROTECTED | Acesso dentro da classe e das herdeiras |
| PUBLIC | Acesso de qualquer lugar |

Se não informado, o padrão é PRIVATE.


---

## 3. Tipagem de Propriedades e Tipos Nativos

### Tipos Nativos TLPP

| Tipo      | Descrição                      | Exemplo |
|-----------|-------------------------------|---------|
| numeric   | Ponto flutuante                | data n as numeric |
| integer   | Inteiro                        | data i as integer |
| double    | Ponto flutuante                | data d as double |
| decimal   | Alta precisão (monetário)      | data f as decimal |
| character | Texto                          | data c as character |
| logical   | Booleano (.T./.F.)             | data l as logical |
| date      | Data                           | data d as date |
| array     | Matriz                         | data a as array |
| object    | Objeto                         | data o as object |
| json      | JSON                           | data j as json |
| codeblock | Bloco de código                | data b as codeblock |
| variant   | Tipo variante                  | data x as variant |

Obs: Se não tipar, será tratado como variant.

---

## 4. Interfaces

Interfaces definem apenas protótipos de métodos. Classes podem implementar uma ou mais interfaces:

```tlpp
Class MyTest implements ITeste

EndClass

```

Múltiplas interfaces:
```tlpp

Class MyTest2 implements I1, I2

EndClass
```

---

## Referências Oficiais

- [Estrutura TLPP](https://tdn.totvs.com/display/tec/Estrutura)
- [Modificadores de Acesso](https://tdn.totvs.com/display/tec/Modificadores+de+Acesso)
- [Tipando Propriedades](https://tdn.totvs.com/display/tec/Tipando+Propriedades)
- [Tipos Nativos](https://tdn.totvs.com/display/tec/Tipos+Nativos)
- [Interface](https://tdn.totvs.com/display/tec/Interface)
- [Sobrecarga de Operadores](https://tdn.totvs.com/display/tec/Sobrecarga+de+Operadores)
- [Chamando construtor da classe pai](https://tdn.totvs.com/display/tec/Chamando+construtor+da+classe+pai)

---

## Internationalization

**Includes:** `tlpp-i18n.th`, `fw-tlpp-i18n.th`

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
return
```

#### @TestSetup and @TestTeardown
```tlpp
@TestSetup
METHOD SetupTest() AS Nil
return

@TestTeardown  
METHOD CleanupTest() AS Nil
return
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
endclass
```

#### Method Security
```tlpp
@RequireAuth(scopes={"admin"})
@Delete(endpoint="/api/admin/users/:id")
METHOD DeleteUser(cUserId AS Character) AS Logical
return
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
endclass
```

#### Conditional Compilation
```tlpp
#ifdef PRODUCTION
    @Log(level="ERROR")
#else
    @Log(level="DEBUG")
#endif
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


ENDCLASS

@Get(endpoint="/", description="List all customers")
METHOD ListCustomers() AS Array class CustomerAPI
    Local aCustomers := {}
    // Implementation
RETURN aCustomers

@Post(endpoint="/", description="Create customer")
METHOD CreateCustomer(oCustomer AS Object) AS Object class CustomerAPI
    Local oResult := {}
    // Validation and creation logic
RETURN oResult

@Get(endpoint="/:id", description="Get customer by ID")
METHOD GetCustomer(cId AS Character) AS Object class CustomerAPI
    Local oCustomer := {}
    // Fetch customer logic
RETURN oCustomer
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
    
ENDCLASS

METHOD New() CONSTRUCTOR class CustomerService
    ::oRepository := CustomerRepository():New()
    ::oValidator := CustomerValidator():New()
RETURN Self

METHOD Create(oCustomer AS Object) AS Object class CustomerService
    Local oResult := {}
    
    If ::oValidator:Validate(oCustomer)
        oResult := ::oRepository:Save(oCustomer)
    Else
        oResult:lError := .T.
        oResult:cMessage := "Validation failed"
    EndIf
    
RETURN oResult

METHOD Delete(cId AS Character) AS Logical class CustomerService
    Local lSuccess := .F.
    
    If !Empty(cId)
        lSuccess := ::oRepository:Delete(cId)
    EndIf
RETURN

METHOD Update(cId AS Character, oCustomer AS Object) AS Object  class CustomerService
    Local oResult := {}
    
    If ::oValidator:Validate(oCustomer)
        oResult := ::oRepository:Update(cId, oCustomer)
    Else
        oResult:lError := .T.
        oResult:cMessage := "Validation failed"
    EndIf
RETURN
```

---

## Includes Reference Index

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
