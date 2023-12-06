# CRUD en PHP
> [!NOTE]
> Crud Clientes

"Connection"

Este fragmento de codigo que encarga de establecer la coneccion entre nuestra base de datos en phpmyadmin con nuetra pagina desarrollada en PHP, esto se realiza mediante estableciendo la ip del servidor, el usuario y contraseña requeridos en funcion de que operaciones se requeiran realizar en la base de datos seleccioanda.

(Codigo de la conexion)

<?php
$servername = "192.168.11.137";
$username = "rootPrueba";
$password = "123";

try {
  $conn = new PDO("mysql:host=$servername;dbname=crudp", $username, $password);
  // set the PDO error mode to exception
  $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
  //echo "Connected successfully";
} catch(PDOException $e) {
  echo "Connection failed: " . $e->getMessage();
}
?>

Curd Articulos
