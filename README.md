# How-to-Upload-File-in-PHP
How to Upload File in PHP


## HTML Form for file upload
```html
<form action="upload-file.php" method="POST" enctype="multipart/form-data">
    Select File to Upload:
    <input type="file" name="file">
    <input type="submit" name="submit" value="Upload">
</form>
```

## PHP logic
```php
<?php
$statusMsg = '';

//file upload path dont forget 777
$targetDir = realpath("uploads/");
//get file name
$fileName = basename($_FILES["file"]["name"]);

//full path and filename.ext
$targetFilePath = $targetDir . "/" . $fileName;

//get file .EXT 
$fileType = pathinfo($targetFilePath,PATHINFO_EXTENSION);

//validate with POST and FILES
if(isset($_POST["submit"]) && !empty($_FILES["file"]["name"])) {
    //allow certain file formats
    $allowTypes = array('jpg','png','jpeg','gif','pdf');
    //looking for Match
    if(in_array($fileType, $allowTypes)){
        //upload file to server
        if(move_uploaded_file($_FILES["file"]["tmp_name"], $targetFilePath)){
            $statusMsg = "The file ".$fileName. " has been uploaded.";
        }else{
            $statusMsg = "Sorry, there was an error uploading your file.";
        }
    }else{
        $statusMsg = 'Sorry, only JPG, JPEG, PNG, GIF, & PDF files are allowed to upload.';
    }
}else{
    $statusMsg = 'Please select a file to upload.';
}

//display status message
echo $statusMsg;
?>
```
