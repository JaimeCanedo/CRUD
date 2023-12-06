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

**Index:**

Este fragmento de código es la base de nuestro CRUD, donde aqui se mostraran todos los registros actuales de artículos en una tabla, los cuales desde aqui estara la opcion de editar y eliminar, además de agregar nuevos artículos.

**Código del index:**
```php
<?php
include "header.php";
include "connection.php";
$stmt = $conn->prepare("SELECT * FROM articulos");
$stmt->execute();
$results = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>

<div class="row">
  <div class="col-md-8">
    <h1>Lista de Articulos en el Sistema</h1>
  </div>
  <div class="col-md-2">
    <h1>
      <a class="btn btn-primary data" href="index.php">
        <i class="bi bi-arrow-return-left"></i> Regresar
      </a>
    </h1>
  </div>
  <div class="col-md-2">
    <h1>
      <button class="btn btn-primary data" data-bs-toggle="modal" data-bs-target="#create_articulos">
        <i class="bi bi-database-add"></i> Nuevo Articulo

    </h1>
  </div>
</div>
<table class="table table-bordered border-white table-dark table-striped">
  <thead>
    <tr>
      <th width="20">ID</th>
      <th width="200">Nombre</th>
      <th width="400">Descripcion</th>
      <th width="20">Costo</th>
      <th width="20">Precio</th>
      <th width="20">Cantidad</th>
      <th width="200">Imagen</th>
      <th width="100">Acciones</th>
    </tr>
  </thead>
  <tbody>
    <?php
    foreach ($results as $result) {
    ?>
      <tr>
        <td><?php echo $result['id']; ?></td>
        <td><?php echo $result['nombre']; ?></td>
        <td><?php echo $result['descripcion']; ?></td>
        <td><?php echo $result['costo']; ?></td>
        <td><?php echo $result['precio']; ?></td>
        <td><?php echo $result['cantidad']; ?></td>
        <td>
          <?php
          if (!empty($result['imagen'])) {
            echo '<img src="data:image/jpeg;base64,' . base64_encode($result['imagen']) . '" alt="Imagen del artículo" style="max-width: 200px; max-height: 200px;">';
          } else {
            echo 'No se encontró la imagen';
          }
          ?>
        </td>
        <td>
          <a href="update_articulos.php?id=<?php echo $result['id']; ?>" class="btn btn-warning btn-sm"><i class="bi bi-pencil-fill"></i></a>
          <a onclick="return confirm_delete()" href="delete_articulos.php?id=<?php echo $result['id']; ?>" class="btn btn-danger btn-sm">
            <i class="bi bi-trash-fill"></i> </a>
        </td>
      </tr>
    <?php } ?>
    <script type="text/javascript">
      function confirm_delete() {
        return window.confirm('¿Estás seguro de eliminar el siguiente artículo?');
      }
    </script>
  </tbody>
</table>
<?php
include "create_articulos.php";
include "footer.php";
?>
```



