# Jquery endless scrolling with JSON data

# Server side json.php page


header('content-type:text/html;charset=utf-8');
header("Cache-Control: no-store, no-cache, must-revalidate, max-age=0");
header("Cache-Control: post-check=0, pre-check=0", false);
header("Pragma: no-cache");
error_reporting(0);
include_once "config.php";	

$sql = mysql_query("select * from table_name");
if(mysql_num_rows($sql)>0){
	while ($res = mysql_fetch_assoc($sql)) {
		$rows[] = $res;
	}
}

echo json_encode($rows, JSON_UNESCAPED_UNICODE|JSON_UNESCAPED_SLASHES);

