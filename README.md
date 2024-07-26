connection.php
<?php
$servername = "192.168.56.103";
$username = "user";
$password = "password";
$dbname = "webapp_db";
 
// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
 
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
 
__________________________
index.php

<?php
require 'connection.php';
 
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = $_POST['name'];
 
    $sql = "INSERT INTO user (name) VALUES ('$name')";
 
    if ($conn->query($sql) === TRUE) {
        echo "New record created successfully";
    } else {
        echo "Error: " . $sql . "<br>" . $conn->error;
    }
 
    $conn->close();
}
?>
 
<!DOCTYPE html>
<html>
<head>
    <title>Simple Form</title>
</head>
<body>
    <form method="POST" action="index.php">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <input type="submit" value="Submit">
    </form>
</body>
</html>

