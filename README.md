<h2 align="center">A repo for my university homework on software design patterns<br><br></h2>

<p align="center">Диаграмма классов</p>

```mermaid
classDiagram
    direction LR
    StudentBase <|-- Student
    StudentBase <|-- StudentShort
    DataListStudentShort <|-- DataList
    StudentListFile o-- FormatStrategy
    FormatStrategy <|.. TXTFormatStrategy
    FormatStrategy <|.. JSONFormatStrategy
    FormatStrategy <|.. YAMLFormatStrategy
    StudentListFile ..> Student
    StudentListFile ..> StudentSerializable
    StudentSerializable ..> Student
    StudentListDB ..> Student
    StudentListDB ..> Database
    StudentListDB ..|> StudentListInterface
    StudentListFileAdapter ..|> StudentListInterface
    StudentListFileAdapter ..> StudentListFile
    StudentList o-- StudentListInterface
    class StudentBase{
        <<abstract>>
        +id : Int*
        +git : String?*
        #nameRegex : Regex$
        #phoneRegex : Regex$
        #telegramRegex : Regex$
        #emailRegex : Regex$
        #gitRegex : Regex$
        +toString() String*
        +show()
        #isValidName(value : String) Boolean$
        #isValidPatronym(value : String) Boolean$
        #isValidPhoneNumber(value : String) Boolean$
        #isValidTelegram(value : String) Boolean$
        #isValidEmail(value : String) Boolean$
        #isValidGit(value : String) Boolean$
    }
    class Student{
        +id : Int
        +surname : String
        +name : String
        +patronym : String
        +phone : String?
        +telegram : String?
        +email : String?
        +git : String?
        +Student(id : Int, surname : String, name : String, patronym : String, phone : String? = null, telegram : String? = null, email : String? = null, git : String? = null)
        +constructor(hashMap : Map~String, Any~)
        +constructor(row : String)
        -constructor(row: List~String~)
        +getInfo() String
        -getInitials() String
        -getContact() Pair~String, String?~?
        +toString() String
        +toStringRow() String
        +checkGit() Boolean
        +checkContact() Boolean
        +setContacts(hashMap : Map~String, String?~)
        +copyWithChangedId(newId : Int) Student
    }
    class StudentShort{
        +id : Int
        +surnameWithInitials : String
        +git : String?
        +contact : String?
        +constructor(id : Int, info : String)
        +constructor(student : Student)
        +toString() String
    }
    class DataTable{
        -array : List~List~Any?~~
        +constructor(array : List~List~Any?~~)
        +get(row : Int, col : Int) Any?
        +getRowCount() Int
        +getColCount() Int
    }
    class DataList{
        <<abstract>>
        #array : List~Any?~
        +constructor(array : List~Any?~)
        +select(number : Int)
        +getSelected() List~Int~
        +getNames() List~String~*
        +getData() DataTable*
    }
    class DataListStudentShort{
        +constructor(studentShortArray : List~StudentShort~)
        +getNames() List~String~
        +getData() DataTable
    }
    class StudentListFile{
        #students : MutableMap~Int, Student~
        #autoIncrementNextId : Int
        +formatStrategy : FormatStrategy
        +constructor(formatStrategy : FormatStrategy)
        +load(filepath : String)
        +save(filepath : String)
        +getStudentById(id : Int) Student
        +getStudentShortList(k : Int, n : Int) DataListStudentShort
        +sortByStudentName()
        +add(student : Student)
        +replace(id : Int, newStudent : Student)
        +remove(id : Int)
        +getStudentShortCount() Int
    }
    class StudentSerializable{
        <<data class>>
        +id : Int
        +surname : String
        +name : String
        +patronym : String
        +phone : String?
        +telegram : String?
        +email : String?
        +git : String?
        +constructor(student : Student)
    }
    class FormatStrategy{
        <<interface>>
        +load(file : File) MutableMap~Int, Student~
        +save(file : File, students : MutableMap~Int, Student~)
    }
    class TXTFormatStrategy{
        +load(file : File) MutableMap~Int, Student~
        +save(file : File, students : MutableMap~Int, Student~)
    }
    class JSONFormatStrategy{
        +load(file : File) MutableMap~Int, Student~
        +save(file : File, students : MutableMap~Int, Student~)
    }
    class YAMLFormatStrategy{
        +load(file : File) MutableMap~Int, Student~
        +save(file : File, students : MutableMap~Int, Student~)
    }
    class StudentListDB {
        +getStudentById(id : Int) Student?
        +getStudentShortList(k : Int, n : Int) DataListStudentShort
        +add(student : Student) Boolean
        +replace(id : Int, newStudent : Student) Boolean
        +remove(id : Int) Boolean
        +getStudentShortCount() Int
    }
    class Database {
        <<object>>
        -conn : Connection
        +connect()
        +disconnect()
        +isConnected() Boolean
        +checkConnection()
        +executeQuery(sql : String) ResultSet
        +executeQuery(sql : String, statementFunction : (PreparedStatement) -> Unit) ResultSet
        +executeUpdate(sql : String) Int
        +executeUpdate(sql : String, statementFunction : (PreparedStatement) -> Unit) Int
    }
    class Config {
        <<object>>
        +DB_URL : String
        +DB_USER : String
        +DB_PASS : String
    }
    class StudentListInterface {
        <<interface>>
        +getStudentById(id : Int) Student?
        +getStudentShortList(k : Int, n : Int) DataListStudentShort
        +add(student : Student) Boolean
        +replace(id : Int, newStudent : Student) Boolean
        +remove(id : Int) Boolean
        +getStudentShortCount() Int
    }
    class StudentListFileAdapter {
        +studentListFileObject : StudentListFile
        +constructor(studentListFileObject : StudentListFile)
        +getStudentById(id : Int) Student?
        +getStudentShortList(k : Int, n : Int) DataListStudentShort
        +add(student : Student) Boolean
        +replace(id : Int, newStudent : Student) Boolean
        +remove(id : Int) Boolean
        +getStudentShortCount() Int
    }
    class StudentList {
        +dataSource : StudentListInterface
        +constructor(dataSource : StudentListInterface)
        +getStudentById(id : Int) Student?
        +getStudentShortList(k : Int, n : Int) DataListStudentShort
        +add(student : Student) Boolean
        +replace(id : Int, newStudent : Student) Boolean
        +remove(id : Int) Boolean
        +getStudentShortCount() Int
    }
```

##
<p align="center">ER-диаграмма базы данных</p>

```mermaid
erDiagram 
    Student {
        INTEGER id PK
        TEXT surname
        TEXT name
        TEXT patronym
        TEXT phone
        TEXT telegram
        TEXT email
        TEXT git
    }
```

##
<h3><br></h3>
<p align="center"><a href="https://youtu.be/bUh2W3jjapA"><img src="https://github.com/user-attachments/assets/423df8af-babc-4bf4-af76-1e2d7c0ab0e9" height=360 alt="ATARAXIA - Patterns"></img></a></p>
