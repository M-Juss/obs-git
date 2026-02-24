```java
holder.itemView.setOnClickListener(v ->{  
    Intent intent = new Intent(context, ShowMenuDetailsActivity.class); //putting
    intent.putExtra("MENU_ID", cart.id); // first id, second vaue
    context.startActivity(intent);  
  
    Toast.makeText(context, "Clicked: " + cart.name, Toast.LENGTH_SHORT).show();  
});
```

```java
int menuId = getIntent().getIntExtra("MENU_ID", -1); // accessing, -1 serves as false / default val when theres no val.
```