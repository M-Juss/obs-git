![[Pasted image 20260115211654.png]]

#### **2 main folders (App, Config and Public )**

##### App Folder
- Controllers - There is where you take inputs from the form and passed it to your SQL Functions or methods
- Helpers - this basically has a method that helps to get use http codes and messages within it.
- Models - This is where you SQL Functions resides, it takes params and queries inside it
- Routes - This is where your different api routes resides

##### Config Folder
-  This where your database.php resides. In which you will connect and set up its connection

##### Public Folder
- This is where index.php resides. Wherein this is what the backend first read. it contains different headers and require the routes on it.