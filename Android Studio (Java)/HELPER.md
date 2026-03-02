### FOR IMAGE CONVERSION
  ```java
import android.graphics.Bitmap;  
import android.graphics.BitmapFactory;  
import android.util.Base64;  
  
import java.io.ByteArrayOutputStream;  
public class ImageHelper {  
  
    public static String bitmapToString(Bitmap bitmap) { // store image  
        if (bitmap == null) return null;  
  
        ByteArrayOutputStream baos = new ByteArrayOutputStream();  
        bitmap.compress(Bitmap.CompressFormat.JPEG, 70, baos);  
        byte[] bytes = baos.toByteArray();  
        return Base64.encodeToString(bytes, Base64.DEFAULT);  
    }  
  
    public static Bitmap stringToBitmap(String encodedString) { // read image  
        if (encodedString == null) return null;  
  
        byte[] bytes = Base64.decode(encodedString, Base64.DEFAULT);  
        return BitmapFactory.decodeByteArray(bytes, 0, bytes.length);  
    }  
}
  
  ```


### FOR NAVIGATING
```java
public class NavHelper {  
  
    public static void navigate(Context context, Class<?> destination){  
        context.startActivity(new Intent(context, destination));  
    }  
    public static void toMainDashboard(Context context){  
        navigate(context, MainActivity.class);  
    }  
}
```

### FOR SESSION
```java
package com.example.project2.helpers;  
  
import android.content.Context;  
import android.content.SharedPreferences;  
  
import com.example.project2.models.UserModel;  
  
import org.json.JSONException;  
import org.json.JSONObject;  
  
public class SessionHelper {  
    public  static  final  String USER_FOLDER = "user_session";  
    public  static  final  String KEY_USER = "KEY_USER";  
  
    public  static void setUser(Context context, UserModel user){  
        JSONObject json = new JSONObject();  
        try {  
            json.put("id", user.getId());  
            json.put("fullname", user.getFullname());  
            json.put("email", user.getEmail());  
            json.put("password", user.getPassword());  
            json.put("role", user.getRole());  
  
            SharedPreferences sharedPreferences = context.getSharedPreferences(USER_FOLDER, Context.MODE_PRIVATE);  
            sharedPreferences.edit().putString(KEY_USER, json.toString()).apply();  
        } catch (JSONException e) {  
            throw new RuntimeException(e);  
        }  
    }  
  
    public static UserModel getUser(Context context){  
        SharedPreferences sharedPreferences = context.getSharedPreferences(USER_FOLDER, Context.MODE_PRIVATE);  
        String jsonString = sharedPreferences.getString(KEY_USER, null);  
  
        try {  
            JSONObject json = new JSONObject(jsonString);  
                return new UserModel(  
                        json.getInt("id"),  
                        json.getString("fullname"),  
                        json.getString("email"),  
                        json.getString("password"),  
                        json.getString("role")  
                );  
  
        } catch (JSONException e) {  
            throw new RuntimeException(e);  
        }  
  
    }  
  
}  
  
%%   STORING
Cursor cursor = db.rawQuery("SELECT * FROM  users WHERE email = ? and password = ?", new String[]{email, password});  
  
if (cursor.moveToFirst()){  
    UserModel user = new UserModel(  
            cursor.getInt(0),  
            cursor.getString(1),  
            cursor.getString(2),  
            cursor.getString(4),  
            cursor.getString(5)  
    );  
  
    SessionHelper.setUser(this, user);
    
    RETRIEVING
    UserModel user = Session.getUser(this); %%
    
    
```