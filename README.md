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
