
### Creating DatabaseHelper
 - Create folder database
 - Inside Create DatabaseHelper.java

### Setting up Database Helper
- extend the class to SQLITEOpenHelper
- import onCreate and onUpgrade
- make constructor of the class and use the params of Context
- in follow this format super(context, database_name, null, version);

### Using DatabaseHelper in Other activities
- import the Databasehelper from its pacakge
- initialize it 

```java
import com.example.codefest.database.DatabaseHelper; // import

DatabaseHelper databaseHelper; // global

databaseHelper = new DatabaseHelper(this); onCreate

```
### onCreate vs onUpgrade
- onCreate triggers when the application has been freshly installed or run in the  device. Meaning all  function or queries in the onCreate will execute all at once. After that it wont run again. This is where onUpgrade appears.
- db.execSQL("CREATE TABLE users(username TEXT));

```java
@Override  
public void onCreate(SQLiteDatabase db) {  
    db.execSQL("CREATE TABLE users(username TEXT, email TEXT PRIMARY KEY, password TEXT, role TEXT)");  
  
    db.execSQL("CREATE TABLE menu(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, description TEXT, price INTEGER, image BLOB )");  
  
    ContentValues cv = new ContentValues();  
    cv.put("username", "Admin");  
    cv.put("email", "email@gmail.com");  
    cv.put("password", "admin123");  
    cv.put("role", "admin");  
  
    db.insert("users", null, cv);  
  
}
```


- onUpgrade is used to modify the existing methods installed when the onCreate triggers. since onCreate run only once, onnUpgrade is used to modify with the use of versioning.  The version that indicatee in the constructor will run with the same version indicates in the onUpgade.

```java
@Override  
public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {  
    
    // cleaning of version and recreate DB.
    db.execSQL("DROP TABLE IF EXISTS users");  
    db.execSQL("DROP TABLE IF EXISTS menu");  
  
    onCreate(db);  
    
    // versioning
    if(oldVerion < 2){modify or add here}
}
```

--- WHEN CHANGIN ONUPGRADE, ONCREATE SHOULD ALSO BE CHANGED SINCE WE HAVE TO   CONSIDER OTHER USERS WHO WILL INSTALL ON ANOTHER APP. WE SHOULD MAKE SURE ITS READY ON ONCREATE

WHEN EDITING / INSERTING  use getWriteableDatabase();
WHEN READING / CHECKING  user getReadableDatabase();


### Install  SimpleSQLiteBrowser
- Go to settings
- plugins
- find the SimpleSQLiteBrowser. Apply and OK

#### To view data base go to
- Device Manger
- 3 dots
- Open Device Explorer
- Click Data folder
- Inside data folder again
- check ctrl +f and get the package name and find it inside the 2nd data folder
- check database and open the .db
- U wont see the table when getWritable or getReadble hasnt been triggered yet.


### Debugging
- When expected error Goto Log Cat (Alt + 6)
- FIND FATAL EXCEPTION that will pin point ur error
- WHEN THE aCTIVITY IS RETURNING BACK TO PREVIOUS IT MEANS THERES AN ERROR IN THE CURRENT.


### SQLite data types 
- INTEGER  - int / long
- REAL - double / float
- TEXT - strig
- BLOB - byte
- INTEGER/NUMERIC (0 = FALSE 1 = TRUE) EX. isActive INTEGER
- REAL  - big decimal
- DATETIME - for date
-  id INTEGER AUTOINCREMENT PRIMARY KEY
- created_at DATE DEFAULT CURRENT_DATE


