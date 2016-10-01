<?php
$conn = mysqli_connect("localhost","root","","user_register_login");
?>












<?php
include("connection.php");
if(isset($_POST["submit"])){
	$name=$_POST["username"];
	$email=$_POST["email"];
	$password=(md5($_POST["password"]));
	$contact_no=$_POST["contact_no"];
	
	$query="select * from register where user_name='$name' or user_email='$email'";
	$run_query=mysqli_query($conn,$query);
	$check=mysqli_num_rows($run_query);
	if($check>=1){
		echo "<h3 style='color:red'>Username or Email you have entered already registred,Please try another</h3>";
	}
	else{
		$querry="insert into register(user_name,user_email,password,contact_no)values('$name','$email','$password','$contact_no')";
		$run_querry=mysqli_query($conn,$querry);
		if($run_querry){
			echo "<h3 style='color:green'>You have registered successfully!!!</h3>";
		}
	}
}
?>
<html>
<head>
</head>
<body>
<form action="" method="post">
<p>Username: <input type="text" name="username" id="user_name"/></p>
<p>Email: <input type="email" name="email" id="user_email"/></p>
<p>Password: <input type="password" name="password" id="user_pass"/></p>
<p>Contact: <input type="number" name="contact_no" id="contact_no"/></p>
<input type="submit" name="submit" value="Register" id="submit"/>If you have already registred,Please login here <a href="login.php"><input type="button"value="Login"/></a>
</form>
</body>
</html>














<?php
session_start();
include("connection.php");
if( isset($_SESSION['user_id']) ){
	header('Location:index.php');
}
if(isset($_POST["login"])){
	$email=$_POST["email"];
	$password=(md5($_POST["password"]));
	
	$query="select user_email,password from register where user_email='$email' and password='$password'";
	$run_query=mysqli_query($conn,$query);
	$check=mysqli_num_rows($run_query);
	if($check==1){
		header("location:index.php");
	}else{
		   echo "<h3>Invalid Login Credentials!!!</h3>";
		}
	}
?>
<html>
<head>
</head>
<body>
<form action="" method="post">
<p>Email: <input type="email" name="email" id="user_email"/></p>
<p>Password: <input type="password" name="password" id="user_pass"/></p>
<input type="submit" name="login" value="Login" id="login"/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Create Account here <a href="register.php"><input type="button"value="Register"/></a>
</form>
</body>
</html>












<?php
echo "Welcome";
?>











<?php
session_start();
session_destroy();
header('Location: login.php');
?>
