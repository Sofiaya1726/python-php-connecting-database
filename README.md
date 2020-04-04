# python-php-connecting-database

#### 一、使用php连接MariaDB，并执行简单查询并打印返回结果
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
<?php
$conn = new mysqli("localhost", "root", " ");
if($conn -> connect_error)
{
    die("连接失败：". $conn->connect_error);
}
mysqli_select_db($conn,"test");
$sql = "select * from e1";

$obj = mysqli_query($conn,$sql);

echo "<center>";
    echo "<table border = 1>";
        echo "<th>编号</th><th>姓名</th><th>密码</th>";
        while($row = mysqli_fetch_assoc($obj)){
        echo "<tr>";
            echo '<td>'.$row['a1'].'</td>';
            echo '<td>'.$row['a2'].'</td>';
            echo '<td>'.$row['a3'].'</td>';

            echo "</tr>";
        }

        echo "</table>";
    echo "</center>";
        mysqli_close($conn);
        ?>
</body>
</html>


#### 二、使用php连接Sqlite，并执行简单查询并打印返回结果

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
<?php
class SQLiteDB extends SQLite3
{
  function __construct()
  {
     $this->open('test.db');
  }
}
$db = new SQLiteDB();
if(!$db){
  echo "failed to open<br/>";
} else {
  echo "Opened database successfully<br/>";
}

echo "<b> Select Data from company table :</b><hr/>";

$sql =<<<EOF
  SELECT * from company;
EOF;

$ret = $db->query($sql);
while($row = $ret->fetchArray(SQLITE3_ASSOC) ){
  echo "ID = ". $row['ID'] . "<br/>\n";
  echo "NAME = ". $row['NAME'] ."<br/>\n";
  echo "AGE = ". $row['AGE'] ."<br/>\n";
  echo '----------------------------------<br/>';
}

$db->close();
?>
</body>
</html>
