# Jquery endless scrolling with JSON data

## Server side json.php page

```
<?php
header('content-type:text/html;charset=utf-8');
header("Cache-Control: no-store, no-cache, must-revalidate, max-age=0");
header("Cache-Control: post-check=0, pre-check=0", false);
header("Pragma: no-cache");
error_reporting(0);

//Initialize database connection
include_once "config.php";	

//DO PAGINATION
$page = 1; //Default page = 1

if(!empty($_GET['page'])) {
    $page = filter_input(INPUT_GET, 'page', FILTER_VALIDATE_INT);
    if(false === $page) {
        $page = 1;
    }
}

$limit = 10;

$offset = ($page - 1) * $limit;
$qry = "SELECT * FROM table_name LIMIT " . $offset . "," . $limit;

//MySQL, MySQLi, PDO whatever

$sql = mysql_query($qry);

if(mysql_num_rows($sql)>0){
	while ($res = mysql_fetch_assoc($sql)) {
		$rows[] = $res;
	}
}

echo json_encode($rows, JSON_UNESCAPED_UNICODE|JSON_UNESCAPED_SLASHES);
?>
```
