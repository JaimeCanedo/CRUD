# CRUD en PHP
> [!NOTE]
> Crud Clientes

**Connection**

Este fragmento de código se encarga de establecer la conexión entre nuestra base de datos en phpMyAdmin y nuestra página desarrollada en PHP. Esto se realiza estableciendo la IP del servidor, el nombre de usuario y la contraseña requeridos en función de las operaciones que se requieran realizar en la base de datos seleccionada.

**Código de la conexión:**
```php
<?php
$servername = "192.168.11.137";
$username = "rootPrueba";
$password = "123";

try {
  $conn = new PDO("mysql:host=$servername;dbname=crudp", $username, $password);
  // establecer el modo de error PDO a excepción
  $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
  // echo "Connected successfully";
} catch(PDOException $e) {
  echo "Connection failed: " . $e->getMessage();
}
?>
```

**Header**

Este fragmento de código se encarga de establecer el formato basico de un HTML5, donde tiene solo el inicio del html, el head, la hoja de vuelo del bootstrap en nuestro caso y el titulo.

**Código del header:**
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="stylesheet" href="Bootstrap/css/bootstrap.min.css" />
  <link rel="stylesheet" href="Bootstrap/icons/bootstrap-icons.min.css">
  <title>Sistema web</title>
</head>
<body>
  <div class="container">
```



