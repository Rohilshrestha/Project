# CRUD
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="css/style.css">

<style>
	body{
		background: white;
		font-family: new times roman;
		text-align: justify;
	}
	label{
		width: 120px;
		display: inline-block;	
	}
	
</style>
	
</head>
<form>
	<fieldset>
		<form action="add.php" method="post" name="form1">

<div class="Registration form">
<h1> CREATE ACCOUNT</h1>
<p>Please fill in this form to create an account.</p>

<label for="Name"><b>Name</b></label>
<input type="text" placeholder="Name" name="Name"><br>
<br>

<label for="Age"><b>Age</b></label>
<input type="nuber" placeholder="Age" name="Age"><br>
<br>

<label for="Email"><b>Email</b></label>
<input type="text" placeholder="Enter Email" name="Email"><br>
<br>

<button type="submit"class="create account "><strong>Create</strong></button>
</div>
<div class="container signin">

</div>
</form>
</fieldset>
</html>

Add.php
<html>
<head>
<title>Add Data</title>
</head>
<body>
<?php
include_once("db.php");
if(isset($_POST['Submit'])) {
$name = mysqli_real_escape_string($mysqli, $_POST['name']);
$age = mysqli_real_escape_string($mysqli, $_POST['age']);
$email = mysqli_real_escape_string($mysqli, $_POST['email']);
if(empty($name) || empty($age) || empty($email)) {
if(empty($name)) {
echo "<font color='red'>Name field is empty.</font><br><br>
";
}
if(empty($age)) {
echo "<font color='red'>Age field is empty.</font><br><br>
";
}
if(empty($email)) {
echo "<font color='red'>Email field is empty.</font><br><br>
";
}
echo "<br/><a href='javascript:self.history.back();'>Go
Back</a>";
} else {
$result = mysqli_query($mysqli, "INSERT INTO users(name,age,email,) VALUES('$name','$age','$email')");
echo "<font color='green'>Data added successfully.";
echo "<br/><a href='index.php'>View Result</a>";
}
}
?>
</body>
</html>

db.php
<?php
$databaseHost = 'localhost';
$databaseName = 'test';
$databaseUsername = '';
$databasePassword = '';
$mysqli = mysqli_connect($databaseHost, $databaseUsername, $databasePassword, $databaseName);
?>

Delete.php
<?php
include("db.php");
$id = $_GET['id'];
$result = mysqli_query($mysqli, "DELETE FROM users WHERE
id=$id");
header("Location:index.php");
?>

Edit.php
<?php
include_once("db.php");
if(isset($_POST['update']))
{
$id = mysqli_real_escape_string($mysqli, $_POST['id']);
$name = mysqli_real_escape_string($mysqli, $_POST['name']);
$age = mysqli_real_escape_string($mysqli, $_POST['age']);
$email = mysqli_real_escape_string($mysqli, $_POST['email']);

if(empty($name) || empty($age) || empty($email)) {
if(empty($name)) {
echo "<font color='red'>Name field is empty.</font><br/>";
}
if(empty($age)) {
echo "<font color='red'>Age field is empty.</font><br/>";
}
if(empty($email)) {
echo "<font color='red'>Email field is empty.</font><br/>";
} else {
$result = mysqli_query($mysqli, "UPDATE users SET
name='$name',age='$age',email='$email', WHERE id=$id");
header("Location: index.php");
}
}
?>
<?php
$id = $_GET['id'];
$result = mysqli_query($mysqli, "SELECT * FROM users WHERE
id=$id");
while($res = mysqli_fetch_array($result))
{
$name = $res['name'];
$age = $res['age'];
$email = $res['email'];
}
?>
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="css/style.css">
<title>Edit Data</title>
<style>
	body{
		background: white;
		font-family: new times roman;
		text-align: justify;
	}
	label{
		width: 120px;
		display: inline-block;	
	}
	
</style>
	
</head>
<form>
	<fieldset>
		<form action="add.php" method="post" name="form1">

<div class="Registration form">
<h1> CREATE ACCOUNT</h1>
<p>Please fill in this form to create an account.</p>

<label for="Name"><b>Name</b></label>
<input type="text" placeholder="Name" name="Name"><br>
<br>

<label for="Age"><b>Age</b></label>
<input type="nuber" placeholder="Age" name="Age"><br>
<br>

<label for="Email"><b>Email</b></label>
<input type="text" placeholder="Enter Email" name="Email"><br>
<br>

<button type="submit"class="create account "><strong>Create</strong></button>
</div>
<div class="container signin">

</div>
</form>
</fieldset>
</html>

Index.php
<?php
include_once("db.php");
$result = mysqli_query($mysqli, "SELECT * FROM users ORDER BY
id DESC");
?>
<html>
<head>
<title>Homepage</title>
</head>
<body>
<a href="add.html">Add New User</a><br/><br/>
<table width='80%' border=0>
<tr bgcolor='#CCCCCC'>
<td>Name</td>
<td>Age</td>
<td>Email</td>
<td>Update</td>
</tr>
<?php
while($res = mysqli_fetch_array($result)) {
echo "<tr>";
echo "<td>".$res['name']."</td>";
echo "<td>".$res['age']."</td>";
echo "<td>".$res['email']."</td>";
echo "<td><a href=\"edit.php?id=$res[id]\">Edit</a> | <a
href=\"delete.php?id=$res[id]\" onClick=\"return confirm('Are you sure
you want to delete?')\">Delete</a></td>";
}
?>
</table>
</body>
</html>

Php code
<?php
session_start();
$db = mysqli_connect('localhost', 'root', '', 'crud');
// initialize variables
$name = "";
$address = "";
$id = 0;
$update = false;
if (isset($_POST['save'])) {
$name = $_POST['name'];
$address = $_POST['address'];
mysqli_query($db, "INSERT INTO info (name, address)
VALUES ('$name', '$address')");
$_SESSION['message'] = "Address saved";
header('location: index.php');
}
