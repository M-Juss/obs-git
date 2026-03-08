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

### Creating Methods

```java
public Boolean insertUser(String username, String email, String password, String role){
	SQLiteDatabase db = this.getWritableDatabase();
	ContentValues cv = new ContentValues();
	cv.put("username", username);
	cv.put("email", email);
	cv.put("password", password);
	cv.put("role", role);
	
	long result = db.insert("user", nulll, cv);
	
	return result != 1;
}
```

### Updating Methods
```java
public boolean updateUserByEmail(  
String oldEmail,  
String username,  
String newEmail,  
String password,  
String role  
) {  
  
SQLiteDatabase db = this.getWritableDatabase();  
  
ContentValues cv = new ContentValues();  
cv.put("username", username);  
cv.put("email", newEmail);  
cv.put("password", password);  
cv.put("role", role);  
  
int result = db.update(  
"users",  
cv,  
"email = ?",  
new String[]{oldEmail}  
);  
  
return result > 0;  
}
```

### Delete Methods

```java
public Boolean deleteUser(String id) {

    SQLiteDatabase db = this.getWritableDatabase();

    int rowsDeleted = db.delete(
            "users",              // table
            "id = ?",          // WHERE condition
            new String[]{id}   // WHERE arguments
    );

    return rowsDeleted > 0; // true if delete successful
}
```

### Returning Models
```java
public MenuModel getMenu()  
{  
    MenuModel menu = new MenuModel();  
    SQLiteDatabase db = new DatabaseHelper(getApplicationContext()).getReadableDatabase();  
    Cursor cursor = db.rawQuery("SELECT id, image_path, name, description, price FROM menu WHERE id = " + id, null);  
  
    if (cursor.moveToFirst()) {  
        return new MenuModel(  
                cursor.getInt(0),  
                cursor.getString(1),  
                cursor.getString(2),  
                cursor.getString(3),  
                cursor.getDouble(4)  
        );  
    }  
  
    return menu;  
}
```

### Returning Array of Models
```java
public ArrayList<Cart> getUserCartItem(){  
    SQLiteDatabase db = this.getReadableDatabase();  
    ArrayList<Cart> cartList = new ArrayList<>();  
  
    int userId = SessionHelper.getUserId(context);  
  
    Cursor cursor = db.rawQuery(  
            "SELECT m.id, m.name, m.price, c.quantity, m.image_path " +  
                    "FROM cart c " +  
                    "INNER JOIN menu m ON c.menuId = m.id " +  
                    "WHERE c.userId = ?",  
            new String[]{String.valueOf(userId)}  
    );  
  
    if (cursor != null && cursor.moveToFirst()){  
        do {  
            Cart cart = new Cart(  
                    cursor.getInt(0),  
                    cursor.getString(1),  
                    cursor.getInt(2),  
                    cursor.getInt(3),  
                    cursor.getString(4)  
            ); cartList.add(cart);  
        } while (cursor.moveToNext());  
    }  
    cursor.close();  
    return cartList;  
}
```