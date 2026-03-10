public ArrayList<UserModel> searchUsers(String keyword){

    ArrayList<UserModel> list = new ArrayList<>();
    SQLiteDatabase db = this.getReadableDatabase();

    Cursor cursor = db.rawQuery(
            "SELECT * FROM users WHERE name LIKE ? OR email LIKE ? OR phone LIKE ?",
            new String[]{
                    "%" + keyword + "%",
                    "%" + keyword + "%",
                    "%" + keyword + "%"
            }
    );

    while(cursor.moveToNext()){

        UserModel user = new UserModel(
        cursor.getInt(0), 
        cursor.getString(1), 
        cursor.getString(2) ;
        
        list.add(user);
    }

    cursor.close();
    db.close();

    return list;
}