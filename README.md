# CRUD en PHP
> [!NOTE]
> Crud Clientes

**Connection**

Este fragmento de código se encarga de establecer la conexión entre nuestra base de datos en phpMyAdmin y nuestra página desarrollada en PHP. Esto se realiza estableciendo la IP del servidor, el nombre de usuario y la contraseña requeridos en función de las operaciones que se requieran realizar en la base de datos seleccionada.

**Código de la conexión:**
```php
<?php
$servername = "192.168.11.138";
$username = "rootIP";
$password = "1234";

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

**Header:**

Este fragmento de código se encarga de establecer el formato basico de un HTML5, donde tiene solo el inicio del HTML, el inicio del HEAD, el TITLE de la pagina, las hojas de vuelo utilizadas, en nuestro caso se uso una hoja de vuelo CSS y una de ICONS, ambas de Bootstrap.

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

**Footer:**

Este fragmento de código se encarga de cerrar el formato basico del HTML5, donde solo se tiene el cierre del DIV, el JavaScript utilizado, en nuestro caso el de bootstrap.min.js, el cierre del BODY y por ultimo el cierre del HTML.

**Código del header:**
```php
</div> <!--Cierra la clase container-->
    <script src="Bootstrap/js/bootstrap.min.js"></script>
  </body>
</html>
```

> [!NOTE]
> Crud Articulos

**Connection**

Este fragmento de código se encarga de establecer la conexión entre nuestra base de datos en phpMyAdmin y nuestra página desarrollada en PHP. Esto se realiza estableciendo la IP del servidor, el nombre de usuario y la contraseña requeridos en función de las operaciones que se requieran realizar en la base de datos seleccionada.

**Código de la conexión:**
```php
<?php
$servername = "192.168.11.138";
$username = "rootIP";
$password = "1234";

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

**Header:**

Este fragmento de código se encarga de establecer el formato basico de un HTML5, donde tiene solo el inicio del HTML, el inicio del HEAD, el TITLE de la pagina, las hojas de vuelo utilizadas, en nuestro caso se uso una hoja de vuelo CSS y una de ICONS, ambas de Bootstrap.

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

**Footer:**

Este fragmento de código se encarga de cerrar el formato basico del HTML5, donde solo se tiene el cierre del DIV, el JavaScript utilizado, en nuestro caso el de bootstrap.min.js, el cierre del BODY y por ultimo el cierre del HTML.

**Código del header:**
```php
</div> <!--Cierra la clase container-->
    <script src="Bootstrap/js/bootstrap.min.js"></script>
  </body>
</html>
```



