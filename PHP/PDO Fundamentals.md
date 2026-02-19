### Prerequisite [[PHP Basics]]

PHP PDO (PHP DATA OBJECT)
- more flexible than mysqli
- can work with multiple database
- has multiple safe features
- can handle error smoothly
- more consistend na object oriented

MAIN PDO CLASSES
PDO - Represents a connection between PHP and DB
PDO STATEMENT - Represents a prepared statement and after executed an associated result
PDO EXCEPTION - Represents errors raised by PDO

```php
//First create database connection
$host = 'localhost'
$user = 'root'
$password = '';
$dbname = 'practicephppdo'

//Second set DSN. Data source name is a string that has associated data structucture to connect to db

$dsn = 'mysql:host=' . $host . ';dbname=' . $dbname;

//Third Create PDO Instance
$pdo = new PDO($dsn, $user, $password);

// $pdo-> setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_OBJ); use this to that u wont fill arguments in feth()
```

# 2 Types of query
##### PDO QUERY METHOD

```php
PDO QUERY METHOD:
$stmt = $pdo->query('SELECT * FROM users');

// to display the result
while($row = $stmt->fetch(PDO::FETCH_ASSOC)){ 
	echo $row['email'] . "<br>";
}

while($row = $stmt->fetch(PDO::FETCH_OBJ)){ 
	echo $row->email . "<br>";
}

/* whats inside the fetch is the method how the data will fetch. 
There are 2 common PDO::FETCH_ASSOC AND PDO::FETCH_OBJ

for PDO::FETCH_ASSOC  the usage is $row['email']; // whats inside the bracket is column in db

for PDO::FETCH_OBJ  the usage is $row->email; // whats pointed by arrow is column in db

for this not to be redundant u can set it in global. 

// $pdo-> setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_OBJ); */
```
##### PDO PREPARED STATEMENT

```php
PDO PREPARED STATEMENT METHOD:

1. Positional Params
   
$sql 'SELECT * FROM users WHERE created_at = ?'
$stmt = $pdo->prepare($sql);
$stmt ->execute([$date;]) // lets say $date comes from forms. if there are multiple ? this should align in the array inside execute.
$datesFilter = $stmt->fetchAll(); //fetch all if the result is more than one other wise fetch()

2. Named Params 
   
$date = "08/28/2005";
$is_active = true;

$sql 'SELECT * FROM users WHERE created_at = :date && is_active = :is_active';
$stmt = $pdo->prepare($sql);
$stmt ->execute(['date' => $date, 'is_active' => $is_active;]) // lets say $date comes from forms. if there are multiple : this should align in the array inside execute.
$datesFilter = $stmt->fetchAll(); //fetch all if the result is more than one other wise fetch()

var_dump($datesFilter); // show us what the results in raw
foreach($datesFilter as $dates){
	echo $dates->email  . "<br>";
} 
```


# TO GET ROW COUNT 

```php
$stmt = $pdo->prepare('SELECT * FROM users');
$stmt->execute();
$rows = $stmt->rowCount();
echo $rows;
```

# INSERT DATA 

```php
$id = 1;
$email = "jussayson@gmail.com;
$password = "pogi";
$is_active =  true;
$created_at = "08/28/2009";

$stmt = $pdo->prepared('INSERT INTO  users (id, email, password, $is_active, created_at) VALUES (?, ?, ?, ?)');
$stmt->execute([$id, $email, $password, $is_active, $created_at]);
echo "Insert success!"
```

# UPDATE DATA 

```php
$id = 1;
$email = "jussayson@gmail.com;

$stmt = $pdo->prepared('UPDATE users SET email = ? WHERE id = ?');
$stmt->execute([$email, $id]);
echo "Update success!"
```
# DELETE DATA 

```php
$id = 1;

$stmt = $pdo->prepared('DELETE FROM users WHERE id = ?');
$stmt->execute([$id]);
echo "Delete success!"
```

# SEARCH DATA with limitation

``` php
$searchedWord = "%a%; // will get result that has a before and after it with limitation
$limit = 5

$stmt = $pdo->prepare('SELECT * FROM  users WHERE email LIKE ?  LIMIT ?')
$stmt ->execute([$searchedWord, $limit]);
$word = $stmt->fetchAll();
```