# TOTVS Framework XCommand Documentation

This document provides a comprehensive overview of the xcommand macros found in the decompressed TOTVS include files. These xcommands provide syntactic sugar and simplified syntax for complex TOTVS/Protheus operations.

## Overview

XCommands in TOTVS are preprocessor directives that expand into native Protheus/AdvPL code, providing:

- Simplified syntax for complex operations
- Object-oriented pattern simplification
- Database operation shortcuts
- UI component creation helpers
- Web service and REST API definitions

---

## Table of Contents

1. [Mail Operations (ap5mail.ch)](#mail-operations)
2. [User Interface Components](#ui-components)
3. [Database Operations](#database-operations)
4. [Web Services & REST APIs](#web-services--rest-apis)
5. [Framework Components](#framework-components)
6. [Object-Oriented Programming](#object-oriented-programming)
7. [Report & Print Operations](#report--print-operations)
8. [Transaction Management](#transaction-management)
9. [XML Operations](#xml-operations)
10. [Timer and Events](#timer-and-events)
11. [Parameter Validation](#parameter-validation)
12. [Function Declaration Shortcuts](#function-declaration-shortcuts)
13. [Debugging Utilities](#debugging-utilities)
14. [Microsoft Office Integration](#microsoft-office-integration)
15. [Graphics and Charts](#graphics-and-charts)
16. [TLPP Framework Extensions](#tlpp-framework-extensions)
17. [Advanced UI Components](#advanced-ui-components)
18. [Connection Management](#connection-management)
19. [System Constants and Definitions](#system-constants-and-definitions)

---

## Mail Operations

**Source:** `decompressed_ap5mail.ch.txt`

### SMTP Connection Management

#### CONNECT SMTP SERVER

```advpl
CONNECT SMTP SERVER <server> 
    ACCOUNT <user> 
    PASSWORD <password> 
    [TIMEOUT <timeout>] 
    [IN SERVER <rpcserver>] 
    [RESULT <result>] 
    [TLS] 
    [SSL]
```

**Purpose:** Establishes connection to SMTP server for sending emails.

#### DISCONNECT SMTP SERVER

```advpl
DISCONNECT SMTP SERVER 
    [IN SERVER <rpcserver>] 
    [RESULT <result>]
```

**Purpose:** Closes SMTP server connection.

### POP3 Connection Management

#### CONNECT POP SERVER

```advpl
CONNECT POP SERVER <server> 
    ACCOUNT <user> 
    PASSWORD <password> 
    [TIMEOUT <timeout>] 
    [IN SERVER <rpcserver>] 
    [RESULT <result>] 
    [TLS] 
    [SSL]
```

**Purpose:** Establishes connection to POP3 server for receiving emails.

#### DISCONNECT POP SERVER

```advpl
DISCONNECT POP SERVER 
    [IN SERVER <rpcserver>] 
    [RESULT <result>]
```

**Purpose:** Closes POP3 server connection.

### Email Operations

#### SEND MAIL

```advpl
SEND MAIL FROM <from_address> 
    TO <to_addresses> 
    [CC <cc_addresses>] 
    [BCC <bcc_addresses>] 
    SUBJECT <subject> 
    BODY <body> 
    [FORMAT TEXT] 
    [ATTACHMENT <files>] 
    [IN SERVER <rpcserver>] 
    [RESULT <result>] 
    [TLS] 
    [SSL]
```

**Purpose:** Sends email message with optional attachments.

#### RECEIVE MAIL MESSAGE

```advpl
RECEIVE MAIL MESSAGE <message_number> 
    [FROM <from_var>] 
    [TO <to_var>] 
    [CC <cc_var>] 
    [BCC <bcc_var>] 
    [SUBJECT <subject_var>] 
    [BODY <body_var>] 
    [ATTACHMENT <files_var> [SAVE IN <path>]] 
    [DELETE] 
    [IN SERVER <rpcserver>] 
    [RESULT <result>] 
    [TLS] 
    [SSL]
```

**Purpose:** Retrieves specific email message from POP3 server.

#### POP MESSAGE COUNT

```advpl
POP MESSAGE COUNT <count_var> 
    [IN SERVER <rpcserver>] 
    [RESULT <result>]
```

**Purpose:** Gets the number of messages in POP3 mailbox.

#### GET MAIL ERROR

```advpl
GET MAIL ERROR <error_msg> 
    [IN SERVER <rpcserver>]
```

**Purpose:** Retrieves last mail operation error message.

---

## UI Components

### Dialog Management

**Source:** `decompressed_sigawin.ch.txt`, `decompressed_protheus.ch.txt`

#### DEFINE MSDIALOG

```advpl
DEFINE MSDIALOG <dialog_obj> 
    [TITLE <title>] 
    [FROM <row1>,<col1> TO <row2>,<col2>] 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [PIXEL] 
    [STYLE <style>] 
    [COLOR <forecolor>,<backcolor>]
```

**Purpose:** Creates a modal dialog window.

#### ACTIVATE MSDIALOG

```advpl
ACTIVATE MSDIALOG <dialog_obj> 
    [CENTERED] 
    [ON INIT <init_block>] 
    [VALID <valid_block>]
```

**Purpose:** Displays and activates the dialog.

### Button Controls

#### BUTTON

```advpl
@ <row>,<col> BUTTON [<button_obj>] 
    PROMPT <caption> 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [ACTION <action_block>] 
    [WHEN <when_block>] 
    [PIXEL]
```

**Purpose:** Creates a standard button control.

#### BTNBMP (Bitmap Button)

```advpl
@ <row>,<col> BTNBMP [<button_obj>] 
    [RESOURCE <bitmap_name>] 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [ACTION <action_block>] 
    [WHEN <when_block>]
```

**Purpose:** Creates a button with bitmap image.

### Input Controls

#### MSGET (Get Control)
```advpl
REDEFINE MSGET [<get_obj> VAR] <variable> 
    [ID <id>] 
    [OF <parent>] 
    [WHEN <when_block>] 
    [VALID <valid_block>] 
    [PICTURE <picture>]
```
**Purpose:** Creates an input field for data entry.

#### MSCOMBOBOX
```advpl
@ <row>,<col> MSCOMBOBOX [<combo_obj> VAR] <variable> 
    [ITEMS <items_array>] 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [WHEN <when_block>] 
    [VALID <valid_block>]
```
**Purpose:** Creates a combobox (dropdown) control.

#### CHECKBOX
```advpl
@ <row>,<col> CHECKBOX [<checkbox_obj> VAR] <logical_var> 
    [PROMPT <caption>] 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [WHEN <when_block>] 
    [VALID <valid_block>]
```
**Purpose:** Creates a checkbox control.

### List Controls

#### LISTBOX
```advpl
@ <row>,<col> LISTBOX [<listbox_obj>] 
    FIELDS [<field_list>] 
    [SIZE <width>,<height>] 
    [OF <parent>] 
    [ON CHANGE <change_block>] 
    [ON DBLCLICK <dblclick_block>]
```
**Purpose:** Creates a listbox for data display and selection.

#### BROWSE
```advpl
@ <row>,<col> [COLUMN] BROWSE <browse_obj> 
    [SIZE <width>,<height>] 
    [OF <parent>]
```
**Purpose:** Creates a browse control for database navigation.

### Framework Browse Components
**Source:** `decompressed_fwbrowse.ch.txt`, `decompressed_fwmbrowse.ch.txt`

#### DEFINE FWBROWSE
```advpl
DEFINE FWBROWSE <browse_obj> 
    [DATA QUERY <query>] 
    [DATA TABLE <table>] 
    [DATA ARRAY <array>] 
    [ALIAS <alias>] 
    [OF <parent>]
```
**Purpose:** Creates a Framework Browse component.

#### ACTIVATE FWBROWSE
```advpl
ACTIVATE FWBROWSE <browse_obj>
```
**Purpose:** Activates the Framework Browse.

#### ADD COLUMN
```advpl
ADD COLUMN <column_obj> 
    DATA <data_block> 
    [TITLE <title>] 
    [SIZE <size>] 
    [PICTURE <picture>] 
    [ALIGN <alignment>] 
    TO <browse_obj>
```
**Purpose:** Adds a column to Framework Browse.

---

## Database Operations
**Source:** `decompressed_topconn.ch.txt`, `decompressed_tbiconn.ch.txt`

### Query Operations

#### TCQUERY
```advpl
TCQUERY <sql_expression> 
    [NEW] 
    [ALIAS <alias>] 
    [VIA <connection>]
```
**Purpose:** Executes SQL query using TopConnect.

### Remote Connection Management

#### CREATE RPCCONN
```advpl
CREATE RPCCONN <server_obj> 
    SERVER <server_name> 
    [PORT <port>] 
    [ENVIRONMENT <env>] 
    [USER <user>] 
    [PASSWORD <password>]
```
**Purpose:** Creates RPC connection to remote server.

#### CLOSE RPCCONN
```advpl
CLOSE RPCCONN <server_obj>
```
**Purpose:** Closes RPC connection.

#### PREPARE ENVIRONMENT
```advpl
PREPARE ENVIRONMENT 
    [IN SERVER <server_obj>] 
    [COMPANY <company>] 
    [BRANCH <branch>] 
    [MODULE <module>] 
    [USER <user>] 
    [TABLES <tables>]
```
**Purpose:** Prepares execution environment on remote server.

#### RESET ENVIRONMENT
```advpl
RESET ENVIRONMENT 
    [IN SERVER <server_obj>]
```
**Purpose:** Resets remote server environment.

### Transaction Management

#### OPEN REMOTE TRANSACTION
```advpl
OPEN REMOTE TRANSACTION <transaction_id> 
    IN <server_obj> 
    BY NAME <process_name> 
    PARAMETERS [<parameters>]
```
**Purpose:** Opens remote transaction.

#### CLOSE REMOTE TRANSACTION
```advpl
CLOSE REMOTE TRANSACTION <transaction_id> 
    CHECKSUM <checksum> 
    IN <server_obj>
```
**Purpose:** Closes remote transaction.

---

## Web Services & REST APIs
**Source:** `decompressed_restful.ch.txt`, `decompressed_apwebsrv.ch.txt`

### RESTful Services

#### WSRESTFUL Class Definition
```advpl
WSRESTFUL <class_name> 
    DESCRIPTION <description> 
    [SECURITY <resource>] 
    [FORMAT <format>] 
    [SSL ONLY]
```
**Purpose:** Defines a RESTful web service class.

#### WSMETHOD HTTP Methods
```advpl
WSMETHOD GET [<method_id>] 
    DESCRIPTION <description> 
    [WSSYNTAX <syntax>] 
    [PATH <path>]

WSMETHOD POST [<method_id>] 
    DESCRIPTION <description> 
    [WSSYNTAX <syntax>] 
    [PATH <path>]

WSMETHOD PUT [<method_id>] 
    DESCRIPTION <description> 
    [WSSYNTAX <syntax>] 
    [PATH <path>]

WSMETHOD DELETE [<method_id>] 
    DESCRIPTION <description> 
    [WSSYNTAX <syntax>] 
    [PATH <path>]
```
**Purpose:** Defines HTTP method handlers for RESTful services.

#### WSDATA
```advpl
WSDATA <variable> [AS <type>] [OPTIONAL]
```
**Purpose:** Defines data members for web service classes.

### SOAP Web Services

#### WSSERVICE
```advpl
WSSERVICE <class_name> 
    [DESCRIPTION <description>] 
    [NAMESPACE <namespace>] 
    [RUNTIME]
```
**Purpose:** Defines a SOAP web service class.

#### WSSTRUCT
```advpl
WSSTRUCT <class_name>
```
**Purpose:** Defines a structure for web service data exchange.

#### WSCLIENT
```advpl
WSCLIENT <class_name>
```
**Purpose:** Defines a web service client class.

---

## Framework Components
**Source:** `decompressed_fwmvcdef.ch.txt`

### MVC Pattern Support

#### NEW MODEL
```advpl
NEW MODEL 
    [SOURCE <source>] 
    [FIELDS <fields>] 
    [DESCRIPTION <description>]
```
**Purpose:** Creates a new MVC model.

#### PUBLISH MODEL REST
```advpl
PUBLISH MODEL REST NAME <name> 
    [SOURCE <source>] 
    [RESOURCE OBJECT <resource_object>]
```
**Purpose:** Publishes model as REST service.

### Toolbar Management

#### ADD FWTOOLBUTTON
```advpl
ADD FWTOOLBUTTON <toolbar> 
    ACTION <action> 
    [TOOLTIP <tooltip>] 
    [IMAGE <image>] 
    [TEXT <text>]
```
**Purpose:** Adds button to Framework toolbar.

---

## Object-Oriented Programming
**Source:** `decompressed_msobject.ch.txt`

### Class Definition

#### CLASS
```advpl
CLASS <class_name> 
    [FROM <parent_class>] 
    [CAMELCASE] 
    [NAME <serial_name>]
```
**Purpose:** Defines a new class.

#### DATA Members
```advpl
DATA <variable> [AS <type>]
PUBLIC DATA <variable> [AS <type>]
PRIVATE DATA <variable> [AS <type>]
PROTECTED DATA <variable> [AS <type>]
CLASSDATA <variable> [AS <type>]
```
**Purpose:** Defines class data members with visibility.

#### METHOD Definition
```advpl
METHOD <method_name> 
    [PUBLIC|PRIVATE|PROTECTED] 
    [CONSTRUCTOR] 
    [VIRTUAL]
```
**Purpose:** Defines class methods.

#### ERROR HANDLER
```advpl
ERROR HANDLER <function_name> 
    [EXTERN|CFUNC|CMETHOD]
```
**Purpose:** Defines error handling for undefined methods.

#### ENDCLASS
```advpl
ENDCLASS
```
**Purpose:** Ends class definition.

---

## Report & Print Operations
**Source:** `decompressed_report.ch.txt`, `decompressed_print.ch.txt`

### Report Definition

#### DEFINE REPORT
```advpl
DEFINE REPORT [<report_obj>] 
    NAME <report_name> 
    [TITLE <title>] 
    [PREVIEW] 
    [TO PRINTER]
```
**Purpose:** Defines a new report.

#### DEFINE SECTION
```advpl
DEFINE SECTION [<section_obj>] 
    OF <parent> 
    [TITLE <title>] 
    [SIZE <size>] 
    [HEADER] 
    [FOOTER]
```
**Purpose:** Defines report section.

#### DEFINE CELL
```advpl
DEFINE CELL [<cell_obj>] 
    NAME <cell_name> 
    OF <parent> 
    [TITLE <title>] 
    [SIZE <size>] 
    [PICTURE <picture>]
```
**Purpose:** Defines report cell.

### Print Operations

#### PRINT/PRINTER
```advpl
PRINT [<print_obj>] 
    [NAME <name>] 
    [TO FILE <filename>] 
    [PREVIEW]

PRINTER [<print_obj>] 
    [NAME <name>] 
    [TO FILE <filename>] 
    [PREVIEW]
```
**Purpose:** Initializes print job.

#### Page Control
```advpl
PAGE => PageBegin()
ENDPAGE => PageEnd()
ENDPRINT => PrintEnd()
```
**Purpose:** Controls page breaks and print job termination.

---

## Transaction Management
**Source:** `decompressed_sigawin.ch.txt`

#### BEGIN TRANSACTION
```advpl
BEGIN TRANSACTION
BEGIN TRANSACTION EXTENDED
```
**Purpose:** Starts database transaction.

#### CLOSETRANSACTION
```advpl
CLOSETRANSACTION LOCKIN <alias_list>
```
**Purpose:** Commits transaction and unlocks specified tables.

---

## XML Operations
**Source:** `decompressed_xmlxfun.ch.txt`

### XML Document Management

#### CREATE XML
```advpl
CREATE <xml_obj> XMLSTRING <xml_string> 
    [ONLYFIRSTNODE] 
    [SETASARRAY <array_list>] 
    [OPTIONAL <optional_list>"

CREATE <xml_obj> XMLFILE <xml_file> 
    [ONLYFIRSTNODE] 
    [SETASARRAY <array_list>] 
    [OPTIONAL <optional_list>]
```
**Purpose:** Creates XML object from string or file.

#### SAVE XML
```advpl
SAVE <xml_obj> XMLSTRING <string_var> [NEWLINE]
SAVE <xml_obj> XMLFILE <filename> [NEWLINE]
```
**Purpose:** Saves XML object to string or file.

### XML Manipulation

#### ADDITEM
```advpl
ADDITEM <where_obj> TAG <tag_name> 
    ON <xml_obj> 
    [ASARRAY] 
    [TEXT <text_content>]
```
**Purpose:** Adds XML tag/item.

#### ADDNODE
```advpl
ADDNODE <where_obj> NODE <node_name> 
    ON <xml_obj> 
    [SETASARRAY <children>]
```
**Purpose:** Adds XML node.

#### DELETENODE
```advpl
DELETENODE <node_name> ON <xml_obj>
```
**Purpose:** Deletes XML node.

---

## Timer and Events
**Source:** `decompressed_protheus.ch.txt`, `decompressed_rwmake.ch.txt`

### Timer Management

#### DEFINE TIMER
```advpl
DEFINE TIMER [<timer_obj>] 
    [INTERVAL <interval>] 
    [ACTION <action_block>] 
    [OF <parent>]
```
**Purpose:** Creates a timer object.

#### ACTIVATE TIMER
```advpl
ACTIVATE TIMER <timer_obj>
```
**Purpose:** Starts the timer.

---

## Parameter Validation
**Source:** `decompressed_parmtype.ch.txt`

### Parameter Type Checking

#### PARAMTYPE
```advpl
PARAMTYPE [<param> VAR] <variable> 
    AS <type> 
    [DEFAULT <default_value>] 
    [MESSAGE <error_message>]
```
**Purpose:** Validates parameter types at runtime.

**Supported Types:**
- ARRAY
- BLOCK  
- CHARACTER
- DATE
- NUMERIC
- LOGICAL
- OBJECT
- JSON

#### PARAMEXCEPTION
```advpl
PARAMEXCEPTION [PARAM <param> VAR] <variable> 
    TEXT <error_text> 
    [MESSAGE <error_message>]
```
**Purpose:** Throws parameter validation exception.

---

## Function Declaration Shortcuts
**Source:** `decompressed_sigawin.ch.txt`, `decompressed_rwmake.ch.txt`

### Function Type Prefixes

#### Function Prefixes
```advpl
User Function <name> => Function U_<name>
Project Function <name> => Function P_<name>
Web Function <name> => Function W_<name>
HTML Function <name> => Function H_<name>
USERHTML Function <name> => Function L_<name>
Template Function <name> => Function T_<name>
```
**Purpose:** Automatically adds appropriate prefixes to function names.

---

## Debugging Utilities

#### Debug Command
```advpl
Debug <fields,...> => MsgDbg({<fields>})
```
**Purpose:** Quick debugging output for multiple fields.

---

## Usage Examples

### Complete Email Example
```advpl
// Connect to SMTP server
CONNECT SMTP SERVER "smtp.gmail.com" ;
    ACCOUNT "user@gmail.com" ;
    PASSWORD "password" ;
    TIMEOUT 30 ;
    RESULT lResult ;
    SSL

// Send email
If lResult
    SEND MAIL FROM "sender@company.com" ;
        TO "recipient@company.com" ;
        SUBJECT "Test Message" ;
        BODY "This is a test message" ;
        RESULT lSent
EndIf

// Disconnect
DISCONNECT SMTP SERVER RESULT lDisconnected
```

### MVC Model Example
```advpl
// Create new model
NEW MODEL ;
    SOURCE "CUSTOMER" ;
    FIELDS {"CUS_CODE", "CUS_NAME", "CUS_EMAIL"} ;
    DESCRIPTION "Customer Management Model"

// Publish as REST service
PUBLISH MODEL REST NAME "customers" ;
    SOURCE "CUSTOMER" ;
    RESOURCE OBJECT oCustomerResource
```

### Dialog with Controls Example
```advpl
Local oDlg, oGet, cName := Space(30)

DEFINE MSDIALOG oDlg ;
    TITLE "Customer Entry" ;
    FROM 0,0 TO 200,400 ;
    PIXEL

@ 20,10 SAY "Name:" OF oDlg PIXEL
@ 18,50 MSGET oGet VAR cName SIZE 100,12 OF oDlg PIXEL

@ 60,120 BUTTON "OK" SIZE 40,12 OF oDlg PIXEL ;
    ACTION oDlg:End()

@ 60,170 BUTTON "Cancel" SIZE 40,12 OF oDlg PIXEL ;
    ACTION oDlg:End()

ACTIVATE MSDIALOG oDlg CENTERED
```

---

## Microsoft Office Integration

**Source:** `decompressed_msexcel.ch.txt`, `decompressed_msproject.ch.txt`, `decompressed_msole.ch.txt`

### Excel Integration

#### Excel Object Management
```advpl
// Excel application constants
#define MSEXCEL_NEW         1
#define MSEXCEL_DESTROY     2
```
#### Excel Caption and Property Management
```advpl
// Caption manipulation
:Caption => :GetCaption()
:Caption := <value> => :SetCaption(<value>)

// Visibility control
:Visible => :GetVisible()
:Visible := <value> => :SetVisible(<value>)
```
**Purpose:** Simplified property access for Excel objects.

### Microsoft Project Integration

#### Project Management
```advpl
// Project constants
#define MSPROJECT_NEW       0001
#define MSPROJECT_DESTROY   0002

// Project navigation
ActiveProject:<property> => _GetPjApp():Projects():<property>
```
**Purpose:** Integration with Microsoft Project for project management.

#### Task and Resource Management
```advpl
// Task operations
#define _TASK_GETFIELD      4001
#define _TASK_SETFIELD      4002

// Resource operations  
#define _RESOURCE_GETFIELD  6001
#define _RESOURCE_SETFIELD  6002
```
**Purpose:** Manage project tasks and resources.

### OLE Integration

#### OLE Container
```advpl
@ <row>,<col> OLECONTAINER [<ole_obj>]
    SIZE <width>,<height>
    OF <parent>
```
**Purpose:** Embed OLE objects in applications.

#### OLE Constants
```advpl
#define oleOnError      "101"
#define oleWdLeft       "201"
#define oleWdTop        "202"
#define oleWdWidth      "203"
#define oleWdHeight     "204"
#define oleWdCaption    "205"
#define oleWdVisible    "206"
```
**Purpose:** OLE object property management.

---

## Graphics and Charts

**Source:** `decompressed_msgraphi.ch.txt`, `decompressed_jpeg.ch.txt`

### Chart Types
```advpl
#define GRP_LINE        1   // Line chart
#define GRP_AREA        2   // Area chart
#define GRP_POINT       3   // Point chart
#define GRP_BAR         4   // Bar chart
#define GRP_PYRAMID     5   // Pyramid chart
#define GRP_CILINDER    6   // Cylinder chart
#define GRP_HBAR        7   // Horizontal bar
#define GRP_HPYRAMID    8   // Horizontal pyramid
```
**Purpose:** Define chart types for graphical components.

### JPEG Image Display
```advpl
@ <row>,<col> JPEG [<jpeg_obj>]
    [NAME <resource_name>]
    [FILE <filename>]
```
**Purpose:** Display JPEG images in applications.

---

## TLPP Framework Extensions

**Source:** `decompressed_tlpp-*.th.txt`

### TLPP Core Features
```advpl
#include "tlpp-object.th"
#include "tlpp-rest.th"
```
**Purpose:** Core TLPP (TOTVS Language Plus Plus) functionality.

### REST Annotations
```advpl
@annotation Get
@end

@annotation Put  
@end

@annotation Patch
@end

@annotation Post
@end

@annotation Delete
@end
```
**Purpose:** REST API method annotations for TLPP.

### Component Documentation
```advpl
TLPP COMPONENT <name> <property> <type> <example>
@annotation t1p9_c0mp0n3n7
    property as char default ""
@end
```
**Purpose:** Document TLPP components with metadata.

### Internationalization
```advpl
// Idiom definition arrays
static _aDefinedIdiom := {} as Array
```
**Purpose:** Support for internationalization in TLPP.

### Framework Model Events
```advpl
@annotation beforeList
@end

@annotation onList  
@end

@annotation afterList
@end

@annotation beforeGetOne
@end
```
**Purpose:** Model lifecycle event handlers.

---

## Advanced UI Components

**Source:** `decompressed_scrollbx.ch.txt`, `decompressed_panelonline.ch.txt`

### ScrollBox Component
```advpl
@ <top>,<left> SCROLLBOX [<scrollbox_obj>]
    SIZE <height>,<width>
    OF <parent>
```
**Purpose:** Create scrollable container components.

### Panel Online Components
```advpl
DEFINE PANELONLINE <panel_obj>
=> <panel_obj> := TPanelOnLine():New()

PANELONLINE <panel_obj> ADDPANEL
    [NAME <id>]
    [TITLE <title>]
    [DESCR <description>]
    [TYPE <type>]
    [PARAMETERS <params>]
    [ONLOAD <process>]

ACTIVATE PANELONLINE <panel_obj>
```
**Purpose:** Create dynamic online panel components.

### Menu Management
```advpl
MENU [<menu_obj>]

MENUITEM [<menuitem_obj> PROMPT] [<caption>]

MRU <mru_obj>

SEPARATOR [<menuitem_obj>] => [<menuitem_obj>:=] MenuAddItem()

ENDMENU => MenuEnd()

DEFINE MENU <menu_obj>
```
**Purpose:** Menu and menu item creation.

---

## Connection Management

**Source:** `decompressed_tbiconn.ch.txt`, `decompressed_topconn.ch.txt`

### Remote Connection Management
```advpl
CREATE RPCCONN <server_obj>
    SERVER <server_name>
    [PORT <port>]
    [ENVIRONMENT <env>]
    [USER <user>]
    [PASSWORD <password>]

CLOSE RPCCONN <server_obj>

PREPARE ENVIRONMENT [IN SERVER <server_obj>]
    [COMPANY <company>]
    [BRANCH <branch>]
    [MODULE <module>]
    [USER <user>]
    [TABLES <tables>]

RESET ENVIRONMENT [IN SERVER <server_obj>]
```
**Purpose:** Manage remote server connections and environments.

### Database Query Operations
```advpl
TCQUERY <sql_expression>
    [ALIAS <alias>]
    [NEW]
    [VIA <connection>]
```
**Purpose:** Execute SQL queries using TopConnect.

---

## System Constants and Definitions

**Source:** Various `.ch` files

### Color Constants
```advpl
#define CLR_SCROLLBAR       -2147483648
#define CLR_BACKGROUND      -2147483647
```
**Purpose:** System color definitions.

### Print Constants
```advpl
#define DMPAPER_LETTER      1    // Letter 8.5 x 11 in
#define DMPAPER_LEGAL       5    // Legal 8.5 x 14 in
#define DMPAPER_TABLOID     3    // Tabloid 11 x 17 in
```
**Purpose:** Paper size constants for printing.

### Virtual Key Codes
```advpl
#define VK_LBUTTON          1    // Left mouse button
#define VK_RBUTTON          2    // Right mouse button
#define VK_CANCEL           3    // Cancel key
#define VK_BACK             8    // Backspace key
```
**Purpose:** Virtual key code definitions.

### Shell Window States
```advpl
#define SW_HIDE             0    // Hide window
#define SW_SHOWNORMAL       1    // Show normal
#define SW_SHOWMINIMIZED    2    // Show minimized
#define SW_SHOWMAXIMIZED    3    // Show maximized
```
**Purpose:** Window display state constants.

### Serial Communication
```advpl
#define pnCOM1              1    // COM port 1
#define pnCOM2              2    // COM port 2
#define pnCOM3              3    // COM port 3
#define pnCOM4              4    // COM port 4
```
**Purpose:** Serial port communication constants.

---

## Best Practices

1. **Error Handling**: Always check RESULT parameters when available
2. **Resource Management**: Always close connections and free resources
3. **Parameter Validation**: Use PARAMTYPE for robust function parameters
4. **Transaction Safety**: Use BEGIN/CLOSETRANSACTION for data integrity
5. **Memory Management**: Use RELEASE commands for object cleanup
6. **Code Organization**: Group related xcommands and maintain consistent indentation

---

## File Reference Index

- **ap5mail.ch** - Email operations (SMTP/POP3)
- **apwebsrv.ch** - SOAP Web Services  
- **restful.ch** - RESTful Web Services
- **protheus.ch** - Core framework components
- **sigawin.ch** - User interface components
- **fwbrowse.ch** - Framework browse controls
- **fwmvcdef.ch** - MVC pattern support
- **msobject.ch** - Object-oriented programming
- **report.ch** - Report generation
- **print.ch** - Print operations
- **xmlxfun.ch** - XML manipulation
- **topconn.ch** - Database connectivity
- **tbiconn.ch** - Remote connections
- **parmtype.ch** - Parameter validation
- **msexcel.ch** - Microsoft Excel integration
- **msproject.ch** - Microsoft Project integration
- **msole.ch** - OLE object integration
- **msgraphi.ch** - Graphics and chart components
- **jpeg.ch** - JPEG image display
- **tlpp-*.th** - TLPP framework extensions
- **scrollbx.ch** - ScrollBox UI components
- **panelonline.ch** - Online panel components
- **ptmenu.ch** - Menu management
- **mscolors.ch** - System color definitions
- **rptdef.ch** - Print and report definitions
- **vkey.ch** - Virtual key codes
- **shell.ch** - Shell and window management
- **msserial.ch** - Serial communication
- **set.ch** - System settings and constants
- **winapi.ch** - Windows API constants
- **ole.ch** - OLE integration constants
- **tcbrowse.ch** - Browse component definitions
- **stdwin.ch** - Standard window definitions

This documentation covers the major xcommand macros found in the TOTVS framework include files. Each xcommand provides simplified syntax for complex operations and follows consistent patterns for optional parameters and result handling.
