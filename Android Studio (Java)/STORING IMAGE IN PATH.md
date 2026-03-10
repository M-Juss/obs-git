ActivityResultLauncher<Intent> pickImage = registerForActivityResult(  
        new ActivityResultContracts.StartActivityForResult(), result -> {  
            if (result.getResultCode() == RESULT_OK){  
                Uri uri = result.getData().getData();  
                getContentResolver().takePersistableUriPermission(uri, Intent.FLAG_GRANT_READ_URI_PERMISSION);  
                binding.image.setImageURI(uri);  
                binding.image.setTag(uri.toString());  
            }  
        });  
        
// Launcher 
// pickImage
// register
// startActivity
// result ->
// reulst == ok
// uri
// get content resolver
// persistablepermission(uri, intent.flag readpermission)
// binding setImageUri (uri)
// binding setTag(uri.toString())

// Intent -> action.getcont
// intent.setType("image/*")

  
binding.image.setOnClickListener(v -> {  
    pickImage.launch(new Intent(Intent.ACTION_GET_CONTENT). setType("image/*");  
});

FOR STORING 
values.put("image_path", binding.image.getTag().toString());  

