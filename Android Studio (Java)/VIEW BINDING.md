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

Binding in Fragment
```java
import com.example.project2.databinding.FragmentAdminOrderBinding;  
  
  
public class AdminOrderFragment extends Fragment {  
    FragmentAdminOrderBinding binding;  
  
    @Override  
    public View onCreateView(LayoutInflater inflater, ViewGroup container,  
                             Bundle savedInstanceState) {  
      binding = FragmentAdminOrderBinding.inflate(inflater, container, false);  
  
        RecyclerView recyclerView = binding.recyclerView;  
        ArrayList<OrderModel> model = new ArrayList<>();  
        model.add(new OrderModel(1, "ORD-439943", "pending"));  
        OrderModelAdapter adapter = new OrderModelAdapter(getContext(), model);  
        recyclerView.setLayoutManager(new LinearLayoutManager(getContext()));  
        recyclerView.setAdapter(adapter);  
  
        return binding.getRoot();  
    }  
}
```