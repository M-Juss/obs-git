binding.save.setOnClickListener(v -> {  
    SQLiteDatabase db = new DatabaseHelper(this).getWritableDatabase();  
    ContentValues values = new ContentValues();  
    values.put("image_path", binding.image.getTag().toString());  
    values.put("name", binding.name.getText().toString());  
    values.put("description", binding.description.getText().toString());  
    values.put("price", Double.parseDouble(binding.price.getText().toString()));  
    values.put("quantity", Integer.parseInt(binding.quantity.getText().toString()));  
    long result = db.insert("menu", null, values);  
  
    if (result != -1 ){  
        Toast.makeText(this, "New menu added successfully", Toast.LENGTH_SHORT).show();  
        finish();  
    } else Toast.makeText(this, "Menu failed to add", Toast.LENGTH_SHORT).show();  
  
});  
  
ActivityResultLauncher<Intent> pickImage = registerForActivityResult(  
        new ActivityResultContracts.StartActivityForResult(), result -> {  
            if (result.getResultCode() == RESULT_OK){  
                Uri uri = result.getData().getData();  
                getContentResolver().takePersistableUriPermission(uri, Intent.FLAG_GRANT_READ_URI_PERMISSION);  
                binding.image.setImageURI(uri);  
                binding.image.setTag(uri.toString());  
            }  
        });  
  
binding.image.setOnClickListener(v -> {  
    Intent intent = new Intent(Intent.ACTION_GET_CONTENT);  
    intent.setType("image/*");  
    pickImage.launch(intent);  
});



binding.save.setOnClickListener(v -> {  
    SQLiteDatabase db = new DatabaseHelper(this).getWritableDatabase();  
    ContentValues values = new ContentValues();  
    values.put("image_path", "");  
    values.put("name", binding.name.getText().toString());  
    values.put("description", binding.description.getText().toString());  
    values.put("price", Double.parseDouble(binding.price.getText().toString()));  
    values.put("quantity", Integer.parseInt(binding.quantity.getText().toString()));  
    db.update("menu",  values, "id = ?", new String[]{String.valueOf(1)});  
    finish();  
});


public ArrayList<MenuModel> showMenu() {  
    SQLiteDatabase db = new DatabaseHelper(getContext()).getReadableDatabase();  
    ArrayList<MenuModel> menu = new ArrayList<>();  
    Cursor cursor = db.rawQuery("SELECT id, image_path, name, price FROM menu", null);  
  
    while(cursor.moveToNext()){  
        MenuModel menuModel = new MenuModel(  
                cursor.getInt(0),  
                cursor.getString(1),  
                cursor.getString(2),  
                cursor.getDouble(3)  
        );  
        menu.add(menuModel);  
    }  
  
    return menu;  
}

db.execSQL("CREATE TABLE menu (" +  
        "id INTEGER PRIMARY KEY AUTOINCREMENT," +  
        "image_path TEXT," +  
        "name TEXT," +  
        "description TEXT, " +  
        "price REAL, " +  
        "quantity INTEGER, " +  
        "created_at DATETIME DEFAULT CURRENT_TIMESTAMP)");  
  
ContentValues cvAdmin = new ContentValues();  
cvAdmin.put("fullname", "Admin Doe");  
cvAdmin.put("email", "admin@gmail.com");  
cvAdmin.put("password", "admin123");  
cvAdmin.put("role", "admin");  
  
db.insert("users", null, cvAdmin);  
  
ContentValues cvStaff = new ContentValues();  
cvAdmin.put("fullname", "Staff Doe");  
cvAdmin.put("email", "staff@gmail.com");  
cvAdmin.put("password", "staff123");  
cvAdmin.put("role", "staff");  
  
db.insert("users", null, cvStaff);  
  
ContentValues cvCustomer = new ContentValues();  
cvAdmin.put("fullname", "Customer Doe");  
cvAdmin.put("email", "customer@gmail.com");  
cvAdmin.put("password", "customer123");  
cvAdmin.put("role", "customer");  
  
db.insert("users", null, cvCustomer);


db.execSQL("DROP TABLE IF exists users");  
db.execSQL("DROP TABLE IF exists menu");  
onCreate(db);