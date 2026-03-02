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

FOR STORING 
values.put("image_path", binding.image.getTag().toString());  

