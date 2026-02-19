# Arrays - collection of elements

```php
`$foods = ("banana", "apple", "orange");`

array_push($foods, "pineapple") //adds an item at the element
array_pop($foods) // the removes the last element
array_reverse($foods) // reverse it

foreach($foods as $food){ // to iterate in each element
	echo $food . "<br>";
}
```

# Associative Array - (key-value pairs)

```php
$users = array(
	"Jus" => "pogi",
	"Kim" => "ganda"
);

foreach($users as $key => value){
	echo "{$key} = {$value}"
}
```

`isset() // returns true if the variable is not null` 
`empty() // return true if the variable is false, null, empty string`

# Function - block of code with of behavior

```php
function Greetings($name) { // u can also add type like string $name
	return "happy birthday ${name}!
}
```

# String functions - manipulates text or data

`strtplower`
`strtoupper`
`trim`
`str_pad($name, 20, "-") // adding 20 char of -`
`str_replace("-", "/", $phoneNumber) change - to / in number`
`strrev`
`str_shuffle`
`strcmp($name, "Jus) if equal 0 if not -1`
`strlen`
`strpos`
`substr`
`explode - get string and combine it as an array the basis are the spaces`
`implode - get the array and display it as a string the basis are per elementee`

# Sanitize  - clean the data

# Validate - evaluate the data to its type

```php
$email = filter_input (INPUT_POST, "email", FILTER_SANITIZE_EMAIL); 
// the first and 3rd params are default the 2nd is the name of the input
//For number it will  only get number ex. khfakjl23aslk the value will be 23

$age = filter_input(INPUT_POST, "age", FILTER_VALIDATE_INT); 
//ex. the value is jbjkbf231. this will return as empty  u can use if else to display message

if(empty($age)){
	echo "This one is not valid for age"
}
```

`include() - this function wil take a component and display it whenever it is called`

# Cookies - Information about user stored preferences, ads, and other non sensitive data. 

```php
//can find cookie under inspect then application

setcookie("key", "value", "time_of_expire", "file_path") // is an associative array. The third argument is the time of  expiration. the fourth argument is the file path

setcookie("fav_food", "Lumpiang Shanghai", time() + (86400 * 2), "/") // the 86400 is seconds in day
setcookie("fav_movie", "Stranger Things", time() + (86400 * 3), "/")
setcookie("fav_color", "Black", time() + (86400 * 4), "/")
setcookie("fav_song", "Toronto 2014", time() + (86400 * 5), "/")

$_COOKIE - to call all datas in cookies

foreach($_COOKIE as $key => $value){ // this will loop in the key and values in cookies
	echo "{$key} = {$value} <br>"
}

For specific cookie calling - $_COOKIE["fav_food"] // this will display pizza
```

# Session - Used to store information on user most commonly in there log in credentials to be used across multiple pages using session-id

```php
session_start() // this starts a session.  U need  to use this in each pages ure going to access the session

$_SESSION // a super global variable for session.

//To create sessions:

$_SESSION["username"] = "jusqt" // most commonly  sessions are the unique id of users
$_SESSION["password"] = "pogi"
```

# Server - contains, headers, paths, and scripts locations. Entries are key value pairs and are created by the web server. Show everything need to know about the web page environment.

```php
$_SERVER["PHP_SELF"] // value of the current file path. When using enclose it with htmlspecialchars() for sanitation and cross site script.
 
$_SERVER["REQUES_METHOD"] // this gets request method, this can be $_GET or $_POST
```

# Password Hashing - transforming sensitive data into something unreadable through mathematical process.  to hide it from 3rd parties.


```php
$password = "poginijuswuhu"

$hashed_password = password_hash($password, PASSWORD_DEFAULT)

// to verify password and hashed passoword

if(password_verify($password, $hashed_password)){
	echo "Same password!"
}

```
