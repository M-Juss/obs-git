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