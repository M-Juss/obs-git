
#### INSERT (boolean)
- SQLiteDatabase
- ContentValues
- .insert("table_name', null, ContentValue);
- result - returns id of the inserted row

#### READ (boolean) / (int)
- SQLiteDatabase
- Cursor along with rawQuery()
- (uses moveToFist(), movetoNext())
- result - returns boolean if there is value on first or next. You can access its result table created by cursor.getColumn_type(column_number)

#### UPDATE (boolean)
- SQLiteDatabase
- ContentValues
- .update("table_name", cv, where_clause, args)
- result - return 0 if fail 1 if success

#### DELETE (boolean)
- SQLiteDatabase
- int result = db.delete("table_name", "where_clause", args);
- result - return 0 if fail 1 if success