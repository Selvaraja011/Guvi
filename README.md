<!DOCTYPE html>
<html>
<head>
	<title>Signup</title>
</head>
<body>
	<h2>Signup</h2>
	<form action="register.php" method="POST">
		<label for="username">Username:</label>
		<input type="text" name="username" id="username" required><br>
		<label for="password">Password:</label>
		<input type="password" name="password" id="password" required><br>
		<label for="email">Email:</label>
		<input type="email" name="email" id="email" required><br>
		<input type="submit" value="Register">
	</form>
</body>
</html>
<?php
	// Get form data
	$username = $_POST['username'];
	$password = $_POST['password'];
	$email = $_POST['email'];

	// Connect to database
	$conn = mysqli_connect("localhost", "username", "password", "database");

	// Check if username is taken
	$query = "SELECT * FROM users WHERE username = '$username'";
	$result = mysqli_query($conn, $query);
	if (mysqli_num_rows($result) > 0) {
		echo "Username already taken.";
		exit();
	}

	// Insert user into database
	$query = "INSERT INTO users (username, password, email) VALUES ('$username', '$password', '$email')";
	mysqli_query($conn, $query);

	// Redirect to login page
	header("Location: login.php");
	exit();
?>


