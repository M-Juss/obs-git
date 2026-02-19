### Set up DataBinding for much easier and clean binding
- Go to build.gradle (module:app)
- inside the android {} put this
```java
buildFeatures {  
    viewBinding true  
}
```
- by this u wont use findById and initialize  components 2 or more times 
- After adding in gradle,  set up the Activities u need to use example activity who uses binding.
```java

import  com.example.codefest.databinding.ActivitySigninBinding; // imports

ActivitySigninBinding binding;  // global

binding = ActivitySigninBinding.inflate(getLayoutInflater());  
setContentView(binding.getRoot()); //inside onCreate()

//usage
binding.loginButton.setOnClickListener(v -> {  
    String email = binding.emailInput.getText().toString().trim();  
    String password = binding.passwordInput.getText().toString().trim();  
    Boolean checkCredentials = databaseHelper.checkEmailPassword(email, password);  
  
    if(TextUtils.isEmpty(email) || TextUtils.isEmpty(password)){  
        Toast.makeText(this, "All Fields are required!", Toast.LENGTH_SHORT).show();  
        return;  
    }  
    if (checkCredentials){  
        Toast.makeText(this, "Sign in Successful!", Toast.LENGTH_SHORT).show();  
        startActivity(new Intent(this, MainActivity.class));  
        finish();  
    } else {  
        Toast.makeText(this, "Wrong Credentials!", Toast.LENGTH_SHORT).show();  
        return;  
    }  
});

```

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

### Creating Methods SQL Query  
- datatype must be in boolean so that its much easier to validate
- uses SQLiteDatabase for database initialization
- uses ContentValues for passing datas from frontend to db
- db.insert
-
```java
public Boolean insertSomething(String name){
	SQLiteDatabase db = this.getWritableDatabase();
	ContentValues cv = new ContentValues();
	cv.("column_name", parameter);
	long resut = db.insert("table", null, cv);
	
	return != -1; // this will return true if the inserting is sucessfull
}
```

### Reading Methods SQL Query
- datatype must be in boolean so that its much easier to validate
- uses SQLiteDatabase for database initialization
-  uses Cursor to point out rows in a table 
- db.rawQuery
```java
public Boolean checkEmail(String email){  
    SQLiteDatabase db = this.getReadableDatabase();  
    try (Cursor cursor = db.rawQuery(  
            "SELECT 1 FROM users WHERE email = ?",  
            new String[]{email})) {  
  
        return cursor.moveToFirst(); // if true email has been used.  
    }  
    catch (Exception exception){  
        System.out.println("Error:" + exception);  
        return false;  
    }  
}
```

```java
public Boolean checkEmailPassword(String email, String password){  
    SQLiteDatabase db = this.getReadableDatabase();  
    try (Cursor cursor = db.rawQuery(  
            "SELECT 1 FROM users WHERE email = ? and password = ?",  
            new String[]{email, password})) {  
  
        return cursor.moveToFirst(); //If true there credentials are correct  
    }  
    catch (Exception exception){  
        System.out.println("Error:" + exception);  
        return false;  
    }  
}
```

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
-  id INTEGER AUTOINCREMENT PRIMARY KEY