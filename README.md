# 7b
 Follow the simple step-by-step instructions, and watch as the ingredients transform into a delectable masterpiece that will tantalize your taste buds and leave you craving for more. Perfect for gatherings, family meals, or a cozy night in, this recipe is bound to become a favorite in your repertoire."
<!-- Database connectivity-->
<?php 
    
    $dbname = "xml";
    $servername = "localhost";
    $username = "root";
    $password = "";
    
    $conn = mysqli_connect($servername,$username,$password,$dbname);
    if(!$conn) {
        echo "Sorry unable to connect to database ".mysqli_connect_error();
    }
?>
<!-- Database connectivity Ends-->

             Save it in C:\xampp\htdocs as searchxml.html

<?php include 'dbconnect.php'; ?>

<!DOCTYPE html>
<html>
<head>
    <title>XML Data Search</title>
    <!--  The styling goes here...  -->
    <style type="text/css">
        input {
            width: 40%;
            padding: 12px;
            margin: 7px 1px;
        }
        input[type=submit] {
            width: 20%;
            margin-left: 10%;
        }
    </style>
    <!--  End of styling  -->
</head>
<body>
<h2> Fetch Data</h2>
<form action="searchxml.php" method="POST">
    <input type="text" name="search" placeholder="Enter the data to search">
    <input type="submit" name="submit" value="search">
</form>
</body>
</html>

               Save it in C:\xampp\htdocs as readxml.php

<?php include 'dbconnect.php' ; ?>
<!-- XML Load File function-->
<?php
    
    $xml = simplexml_load_file('samplefile.xml');

    foreach ($xml->student as $student) {
        $id =  $student->id;
        $name =  $student->name;
        $age =  $student->age;
        $query = mysqli_query($conn, "INSERT INTO mca values('$name',$age')");
    }
?>
<!-- XML loadfile function Ends-->

                      Save it in C:\xampp\htdocs as searchxml.php
<?php include 'dbconnect.php' ; ?>
<?php   
if(isset($_POST['submit'])) {
        $key = isset($_POST['search'])?$_POST['search']:'';
        $find_name = mysqli_query($conn, "SELECT * FROM mca WHERE name LIKE '%$key%'");
        $count = mysqli_num_rows($find_name);

        if($count == 0) {
            echo "Sorry, No such name exist in the database..";
        } else if ($count==1){
            echo "<table border='1' width='500'><tr><th>Name</th><th>Age</th></tr>";
            while ($row = mysqli_fetch_assoc($find_name)) {
                echo "<tr>
                    <td>$row[name]</td>
                    <td>$row[age]</td>
                    </tr></table>";
            }           
        } else{
            echo "state 1";
        }
    }
$conn->close();
?>
              save it in c:\xampp\htdocs as samplefile.xml
<Students>
	<student>
		<name>daiwik</name>
		<age>20</age>
	</student>
	<student>
		<name>soham</name>
		<age>22</age>
	</student>
	
	<student>
		<name>himani</name>
		<age>21</age>
	</student>
	<student>
		<name>deetya</name>
		<age>20</age>
	</student>
	
</Students>

OUTPUT:              
•	Run the XAMPP server.
•	Create the database.
•	Open the browser and execute the readxml.php
•	Open the browser and execute the searchxml.php, searchxml.html

 

