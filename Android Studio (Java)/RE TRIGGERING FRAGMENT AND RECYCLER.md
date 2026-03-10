
OnCartUpdated listener;  
  
public interface OnCartUpdated{  
    void onCartUpdated();  
}  
  
public CartItemModelAdapter(Context context, ArrayList<CartItemModel> arrayList, OnCartUpdated listener) {  
    this.context = context;  
    this.arrayList = arrayList;  
    this.listener = listener;  
}

holder.binding.increment.setOnClickListener(v -> {  
    cart.quantity++;  
  
    updateQuantity(cart.cartId, cart.quantity);  
      
  
    holder.binding.quantity.setText(String.valueOf(cart.quantity));  
  
    notifyItemChanged(holder.getBindingAdapterPosition());  
    listener.onCartUpdated();  
  
});  

CartItemModelAdapter adapter = new CartItemModelAdapter(getContext(), model, () -> {  
    binding.totalAmount.setText(String.valueOf(getTotalPrice(model)));  
});
  
holder.binding.decrement.setOnClickListener(v -> {  
    if(cart.quantity > 1){  
        cart.quantity--;  
    }  
  
    updateQuantity(cart.cartId, cart.quantity);  
  
    holder.binding.quantity.setText(String.valueOf(cart.quantity));  
    notifyItemChanged(holder.getBindingAdapterPosition());  
    listener.onCartUpdated();  
});

holder.binding.remove.setOnClickListener(v -> {  
    Log.d("CLICKING", "click");  
    removeItem(cart.cartId);  
    arrayList.remove(holder.getBindingAdapterPosition());  
    notifyItemRemoved(holder.getBindingAdapterPosition());  
    listener.onCartUpdated();  
});

public void updateQuantity(int cartId, int quantity){  
    SQLiteDatabase db = new DatabaseHelper(context.getApplicationContext()).getWritableDatabase();  
    ContentValues cv = new ContentValues();  
    cv.put("quantity", quantity);  
    db.update("cart", cv, "id = ?", new String[]{String.valueOf(cartId)});  
}  

  
public void removeItem(int cartId){  
    SQLiteDatabase db = new DatabaseHelper(context.getApplicationContext()).getReadableDatabase();  
    db.delete("cart", "id = ?", new String[]{String.valueOf(cartId)});  
}

public double getTotalPrice(ArrayList<CartItemModel> cart){  
    double total = 0;  
    for (CartItemModel model : cart){  
        total += model.quantity * model.price;  
    }  
    return total;  
}
