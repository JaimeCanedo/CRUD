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

**Create:**

Este fragmento de código maneja la inserción de nuevos artículos en la base de datos cuando se envía el formulario desde el modal. Además, proporciona una interfaz gráfica para que los usuarios introduzcan los detalles del nuevo artículo.

**Código del create:**
```php
<?php
include "connection.php";
if ($_POST) {
    $nombre = isset($_POST['nombre']) ? $_POST['nombre'] : "";
    $descripcion = isset($_POST['descripcion']) ? $_POST['descripcion'] : "";
    $costo = isset($_POST['costo']) ? $_POST['costo'] : "";
    $precio = isset($_POST['precio']) ? $_POST['precio'] : "";
    $cantidad = isset($_POST['cantidad']) ? $_POST['cantidad'] : "";

    $imagen_temporal = isset($_FILES['imagen']['tmp_name']) ? $_FILES['imagen']['tmp_name'] : "";
    $imagen_contenido = file_get_contents($imagen_temporal);

    $stmt = $conn->prepare("INSERT INTO articulos (nombre, descripcion, costo, precio, cantidad, imagen) VALUES (:nombre, :descripcion, :costo, :precio, :cantidad, :imagen)");
    $stmt->bindValue(":nombre", $nombre);
    $stmt->bindValue(":descripcion", $descripcion);
    $stmt->bindValue(":costo", $costo);
    $stmt->bindValue(":precio", $precio);
    $stmt->bindValue(":cantidad", $cantidad);
    $stmt->bindValue(":imagen", $imagen_contenido, PDO::PARAM_LOB);
    $stmt->execute();

    echo '<script type="text/javascript">';
    echo 'window.location.href = "index_articulos.php";';
    echo '</script>';
}
?>

<!-- Modal para crear articulo -->
<div class="modal" id="create_articulos" tabindex="-1" aria-labelledby="modallabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel" >Nuevo articulo</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form action="" method="post" enctype="multipart/form-data">
                    <div class="mb-3">
                        <label for="nombre" class="form-label">Nombre</label>
                        <input type="text" class="form-control" name="nombre" id="inputnombre" placeholder="Ingresa el nombre del producto" required>
                    </div>
                    <div class="mb-3">
                        <label for="descripcion" class="form-label">Descripcion</label>
                        <input type="text" class="form-control" name="descripcion" id="inputdescripcion" placeholder="Es un producto lacteo" required>
                    </div>
                    <div class="mb-3">
                        <label for="costo" class="form-label">Costo</label>
                        <input type="number" class="form-control" name="costo" id="inputcosto" placeholder="120.00" required>
                    </div>
                    <div class="mb-3">
                        <label for="precio" class="form-label">Precio</label>
                        <input type="number" class="form-control" name="precio" id="inputprecio" placeholder="140.00" required>
                    </div>
                    <div class="mb-3">
                        <label for="cantidad" class="form-label">Cantidad</label>
                        <input type="number" class="form-control" name="cantidad" id="inputcantidad" placeholder="50: piezas" required>
                    </div>
                    <div class="mb-3">
                        <label for="imagen" class="form-label">Imagen</label>
                        <input type="file" class="form-control" name="imagen" id="inputimagen" accept="image/*" required>
                    </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
                <button type="submit" class="btn btn-primary">Guardar</button>
            </div>
        </div>
        </form>
    </div>
</div>
```

**Update:**

Este fragmento de código maneja la actualización de detalles de un artículo en la base de datos y proporciona una interfaz gráfica para que los usuarios realicen esta operación.

**Código del update:**
```php
<?php
include "connection.php";

if (isset($_GET['id'])) {
    $id = (isset($_GET['id']) ? $_GET['id'] : '');
    $stmt = $conn->prepare("SELECT * FROM articulos WHERE id=:id");
    $stmt->bindValue(":id", $id);
    $stmt->execute();
    $result = $stmt->fetch(PDO::FETCH_LAZY);
    $nombre = $result['nombre'];
    $descripcion = $result['descripcion'];
    $costo = $result['costo'];
    $precio = $result['precio'];
    $cantidad = $result['cantidad'];
    $imagen = $result['imagen'];
}

if ($_POST) {
    $id = (isset($_POST['id']) ? $_POST['id'] : '');
    $nombre = (isset($_POST['nombre']) ? $_POST['nombre'] : '');
    $descripcion = (isset($_POST['descripcion']) ? $_POST['descripcion'] : '');
    $costo = (isset($_POST['costo']) ? $_POST['costo'] : '');
    $precio = (isset($_POST['precio']) ? $_POST['precio'] : '');
    $cantidad = (isset($_POST['cantidad']) ? $_POST['cantidad'] : '');
    $imagen_temporal = isset($_FILES['imagen']['tmp_name']) ? $_FILES['imagen']['tmp_name'] : "";
    $imagen_contenido = file_get_contents($imagen_temporal);
    $stmt = $conn->prepare("UPDATE `articulos` SET `id`=:id, `nombre`=:nombre, `descripcion`=:descripcion, `costo`=:costo, 
        `precio`=:precio, `cantidad`=:cantidad ,`imagen`=:imagen WHERE `articulos`.`id`=:id");
    $stmt->bindValue(":id", $id);
    $stmt->bindValue(":nombre", $nombre);
    $stmt->bindValue(":descripcion", $descripcion);
    $stmt->bindValue(":costo", $costo);
    $stmt->bindValue(":precio", $precio);
    $stmt->bindValue(":cantidad", $cantidad);
    $stmt->bindValue(":imagen", $imagen_contenido, PDO::PARAM_LOB);
    $stmt->execute();
    if ($stmt) {
?>
        <div class="alert alert-succes alert-dismissible fade show" role="altert">
            <strong>Correcto!</strong> Se actualizo el articulo.
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
        </div>
    <?php
        header('location: index_articulos.php');
    } else {
    ?>
        <div class="alert alert-danger alert-dismissible fade show" role="alert">
            <strong>Error!</strong> No se pudo actualizar el articulo.
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
        </div>
<?php
    }
}
include "header.php";
?>

<!-- Formulario de actualizar articulos -->
<div class="row">
    <div class="col-md-8">
        <h2>Actualizar Articulos</h2>
        <form action="" method="post" enctype="multipart/form-data">
            <input type="hidden" id="id" name="id" value="<?php echo $id; ?>">
            <div class="mb-3">
                <label for="nombre" class="form-label">Nombre</label>
                <input type="text" class="form-control" name="nombre" id="inputnombre" placeholder="Ingresa el nombre del producto" required value="<?php echo $nombre ?>">
            </div>
            <div class="mb-3">
                <label for="descripcion" class="form-label">Descripcion</label>
                <input type="descripcion" class="form-control" name="descripcion" id="inputdescripcion" placeholder="Es un producto lacteo" required value="<?php echo $descripcion ?>">
            </div>
            <div class="mb-3">
                <label for="costo" class="form-label">Costo</label>
                <input type="number" class="form-control" name="costo" id="inputcosto" placeholder="120.00" required value="<?php echo $costo ?>">
            </div>
            <div class="mb-3">
                <label for="precio" class="form-label">Precio</label>
                <input type="number" class="form-control" name="precio" id="inputprecio" placeholder="140.00" required value="<?php echo $precio ?>">
            </div>
            <div class="mb-3">
                <label for="cantidad" class="form-label">Cantidad</label>
                <input type="number" class="form-control" name="cantidad" id="inputcantidad" placeholder="50: pzs" required value="<?php echo $cantidad ?>">
            </div>
            <div class="mb-3">
                <label for="imagen" class="form-label">Imagen</label>
                <input type="file" class="form-control" name="imagen" id="inputimagen" accept="image/*" required>
            </div>
    </div>
    <div class="row">
        <div class="col-md-2">
            <a href="index_articulos.php" class="btn btn-primary"><i class="bi bi-arrow-return-left"></i> Regresar</a>
        </div>
        <div class="col-md-2">
            <button type="submit" class="btn btn-primary"><i class="bi bi-pencil-fill"></i> Modificar</button>
        </div>
    </div>
    </form>
</div>

<?php
include "footer.php";
?>
```



