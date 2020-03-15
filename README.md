# Core PHP Admin panel


A Simple Admin Pannel written in core PHP. It contains an implementation of general features you might need in your website admin panel like :

  - Record management (CRUD)
  - Bootstrap based HTML template.
  - Secure Authentication
  - Pagination
  - Filters

### Live Demo :
simply add file field.

if(isset($_FILES['image'])){
  $img = $_FILES["image"]["tmp_name"]; // file tem name
  $image = $_FILES['image']['name']; //Get file name
  $target = "uploads/".basename($image); // create File directory
  $imageFileType = strtolower(pathinfo($target,PATHINFO_EXTENSION)); //Get file extension
  if($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg" && $imageFileType != "gif" ){
    echo 'Insert failed: FILE IS NOT IMAGE ' // here we are checking for valid image
  } 
  else 
  {
    move_uploaded_file($_FILES['image']['tmp_name'], $target); //moving file to the target directory
    $data = array_filter($_POST); // assigning fields data to $DATA Variable
    $data['created_by'] = $_SESSION['user_id']; // adding user id
    $data['image'] = $target; // adding image path to data
    $data['created_at'] = date('Y-m-d H:i:s'); // adding current time to data
    $db = getDbInstance();
    $last_id = $db->insert('groups', $data);
    if ($last_id)
    {
    $_SESSION['success'] = 'Group added successfully!';
    header('Location: groups.php');
    exit();
    }
    else
    {
    echo 'Insert failed: ' . $db->getLastError();
    exit();
    }
  }
}
else
{
  echo 'Insert failed: Image not uploaded '
}





### Live Demo :
http://freecs9.epizy.com/core-php-admin
Credentials :  
**username** : admin
**password** : admin


### Libraries used : 
  - MysqliDb (https://github.com/ThingEngineer/PHP-MySQLi-Database-Class)
