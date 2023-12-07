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

**Create:**

Esta seccion del gestiona la inserción de nuevos clientes en una base de datos, obteniendo la información del formulario HTML mediante el método POST. Luego, redirige a la página principal. El código HTML utiliza Bootstrap para crear un modal con un formulario que recopila nombre, email, teléfono y dirección del nuevo cliente. Este código facilita la interacción del usuario y la manipulación de la base de datos para la creación de clientes.

**Codigo del Create:**

```php
<?php
include "connection.php";
if ($_POST) {
    $nombre = (isset($_POST['nombre']) ? $_POST['nombre'] : "");
    $email = (isset($_POST['email']) ? $_POST['email'] : "");
    $telefono = (isset($_POST['telefono']) ? $_POST['telefono'] : "");
    $direccion = (isset($_POST['direccion']) ? $_POST['direccion'] : "");

    $stmt = $conn->prepare("INSERT INTO clientes (nombre,email,telefono,direccion) VALUES (:nombre,:email,:telefono,:direccion)");
    $stmt->bindValue(":nombre",$nombre);
    $stmt->bindValue(":email",$email);
    $stmt->bindValue(":telefono",$telefono);
    $stmt->bindValue(":direccion",$direccion);
    $stmt->execute();
    header("location:index.php");
}

?>

<!-- Modal para crear cliente -->
<div class="modal" id="create" tabindex="-1" aria-labelledby="modallabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel">Nuevo cliente</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form action="" method="post">
                    <div class="mb-3">
                        <label for="nombre" class="form-label">Nombre</label>
                        <input type="text" class="form-control" name="nombre" id="inputnombre" placeholder="Ingresa tu nombre" required>
                    </div>
                    <div class="mb-3">
                        <label for="email" class="form-label">Email</label>
                        <input type="email" class="form-control" name="email" id="inputemail" placeholder="name@example.com" required>
                    </div>
                    <div class="mb-3">
                        <label for="telefono" class="form-label">Telefono</label>
                        <input type="tel" class="form-control" name="telefono" id="inputtelefono" placeholder="123-456-7890" required>
                    </div>
                    <div class="mb-3">
                        <label for="direccion" class="form-label">Dirección</label>
                        <input type="text" class="form-control" name="direccion" id="inputdireccion" placeholder="Ingresa tu dirección" required>
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

**Delete**

Esta seccion de codigo se encarga de eliminar clientes de la base de datos. Verifica si se ha proporcionado un parámetro 'id' a través de la URL. Si existe, se utiliza para preparar y ejecutar una consulta SQL que elimina el cliente correspondiente. Después de la eliminación, redirige a la página principal. La funcionalidad de eliminacion depende enteramente de este bloque de codigo.

**Codigo de Delete**

```php
<?php
include "connection.php";
if (isset($_GET['id'])) {
    $id=(isset($_GET['id']) ? $_GET['id'] : "");
    $stmt = $conn->prepare("DELETE FROM clientes WHERE id=:id");
    $stmt->bindParam(":id",$id);
    $stmt->execute();
    header('location: index.php');
}
?>
```

**Index**
Este segmento de codigo una interfaz para gestionar clientes almacenados en la base de datos. Permite acceder a las opciones de ver, crear, actualizar y eliminar registros. Utiliza una tabla para mostrar la información de los clientes, con botones para la interacción del usuario. Se incluyen scripts y archivos adicionales para la creación de nuevos clientes y la gestión del diseño. El código constituye el entorno de gestión de clientes con funcionalidades esenciales de CRUD.
**Codigo del Index**

```php
<?php
include "header.php";
include "connection.php";

$stmt = $conn->prepare("SELECT * FROM clientes");
$stmt->execute();
$results = $stmt->fetchAll(PDO::FETCH_ASSOC);

?>
<!-- Contenido -->
<div class="row">
  <div class="col-md-10">
    <h1>Clientes</h1>
  </div>
  <div class="col-md-2">
    <h1>
      <button class="btn btn-primary data" data-bs-toggle="modal" data-bs-target="#create">
      <i class="bi bi-person-fill-add"></i> Nuevo
      </button>
    </h1>
  </div>
</div>
<table class="table table-bordered table-striped">
<thead>
  <tr>
    <th width="20">ID</th>
    <th>Nombre</th>
    <th>Email</th>
    <th>Telefono</th>
    <th>Dirección</th>
    <th width="100">Acciones</th>
  </tr>
</thead>
<tbody>
  <?php     
  foreach ($results as $result){
  ?>
  <tr>
    <td><?php echo $result['id']; ?></td>
    <td><?php echo $result['nombre']; ?></td>
    <td><?php echo $result['email']; ?></td>
    <td><?php echo $result['telefono']; ?></td>
    <td><?php echo $result['direccion']; ?></td>
    <td>
      <a href="update.php?id=<?php echo $result['id']; ?>" class="btn btn-warning btn-sm"><i class="bi bi-pencil-fill"></i></a>
      <a onclick="return confirm_delete()" href="delete.php?id=<?php echo $result['id']; ?>" class="btn btn-danger btn-sm">
      <i class="bi bi-trash-fill"></i></a>
  
  </tr>
  <?php } ?>
</tbody>
</table>
<script type="text/javascript">
 function confirm_delete(){
  return confirm('¿Estas seguro de eliminarlo?');
 }
</script>
<?php
include "create.php";
include "footer.php";
?>
```

**Update**
El bloque de codigo permite actualizar la información de clientes en la base de datos. Al recibir un ID, prellena el formulario con los detalles existentes del cliente. Después de enviar el formulario se actualiza la base de datos y mostrando un mensaje de éxito o error. Facilita gestionar los procesos de actualizacion de informacion directamente desde la pagina web.
**Codigo de Update**

```php
<?php
    include "connection.php";
    
    if (isset($_GET['id'])) {
        $id=(isset($_GET['id'])?$_GET['id']:'');
        $stmt = $conn->prepare("SELECT * FROM clientes WHERE id=:id");
        $stmt->bindValue(":id",$id);
        $stmt->execute();
        $result=$stmt->fetch(PDO::FETCH_LAZY);
        $nombre = $result['nombre'];
        $email = $result['email'];
        $telefono = $result['telefono'];
        $direccion = $result['direccion'];
    }

    if ($_POST) {
        $id=(isset($_POST['id']) ? $_POST['id']:'');
        $nombre=(isset($_POST['nombre']) ? $_POST['nombre']:'');
        $email=(isset($_POST['email']) ? $_POST['email']:'');
        $telefono=(isset($_POST['telefono']) ? $_POST['telefono']:'');
        $direccion=(isset($_POST['direccion']) ? $_POST['direccion']:'');

        $stmt = $conn->prepare("UPDATE `clientes` SET `id`=:id, `nombre`=:nombre, `email`=:email, `direccion`=:direccion, 
        `telefono`=:telefono  WHERE `clientes`.`id`=:id");
        $stmt->bindValue(":id",$id);
        $stmt->bindValue(":nombre",$nombre);
        $stmt->bindValue(":email",$email);
        $stmt->bindValue(":telefono",$telefono);
        $stmt->bindValue(":direccion",$direccion);
        $stmt->execute();
        if ($stmt) {
   ?>         
            <div class="alert alert-succes alert-dismissible fade show" role="altert">
            <strong>Correcto!</strong> Se actualizo el cliente.
            
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
            </div>
            <?php
            header('location: index.php');
        } else {
            ?>
            <div class="alert alert-danger alert-dismissible fade show" role="alert">
                <strong>Error!</strong> No se pudo actualizar el cliente.
                <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
            </div>
    <?php
       
    }
}
include "header.php";
?>
<!-- Formulario de actualizar cliente -->
<div class="row">
    <div class="col-md-10">
        <h2>Actualizar Cliente</h2>
    </div>
    <form action="" method="post">
                    <input type="hidden" id="id" name="id" value="<?php echo $id; ?>">
                    <div class="mb-3">
                        <label for="nombre" class="form-label">Nombre</label>
                        <input type="text" class="form-control" name="nombre" id="inputnombre" placeholder="Ingresa tu nombre" required value="<?php echo $nombre?>">
                    </div>
                    <div class="mb-3">
                        <label for="email" class="form-label">Email</label>
                        <input type="email" class="form-control" name="email" id="inputemail" placeholder="name@example.com" required value="<?php echo $email?>">
                    </div>
                    <div class="mb-3">
                        <label for="telefono" class="form-label">Telefono</label>
                        <input type="tel" class="form-control" name="telefono" id="inputtelefono" placeholder="123-456-7890" required value="<?php echo $telefono?>">
                    </div>
                    <div class="mb-3">
                        <label for="direccion" class="form-label">Dirección</label>
                        <input type="text" class="form-control" name="direccion" id="inputdireccion" placeholder="Ingresa tu dirección" required value="<?php echo $direccion?>">
                    </div>
                    <button type="submit" class="btn btn-primary">Modificar</button>
                    </form>
        </div>
<?php
    include "footer.php";
?>
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

Este fragmento de código constituye la columna vertebral de nuestro sistema CRUD (CREATE, READ, UPDATE, DELETE). Aquí, se presentan de manera organizada todos los registros actuales de artículos en una tabla. Desde esta interfaz, los usuarios tienen la opción de editar y eliminar registros existentes, así como de agregar nuevos artículos a la base de datos.

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

Este fragmento de código gestiona la inserción de nuevos artículos en la base de datos cuando se envía el formulario desde el modal correspondiente. Además de facilitar la inserción, proporciona una interfaz visualmente atractiva que permite a los usuarios ingresar los detalles del nuevo artículo de manera intuitiva y eficiente.

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

Este fragmento de código se encarga de gestionar la actualización de los detalles de un artículo en la base de datos. Además, ofrece a los usuarios una interfaz gráfica intuitiva que les permite realizar esta operación de manera sencilla y eficiente.

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

**Delete:**

Este fragmento de código está diseñado para eliminar un artículo específico de la base de datos, utilizando la identificación proporcionada en la URL. Después de completar la eliminación, redirige al usuario de manera fluida de vuelta al índice, donde se muestra la lista actualizada de artículos. Este proceso garantiza una gestión eficiente y coherente de los registros en la base de datos.

**Código del delete:**
```php
<?php
include "connection.php";
if (isset($_GET['id'])) {
    $id=(isset($_GET['id']) ? $_GET['id'] : "");
    $stmt = $conn->prepare("DELETE FROM articulos WHERE id=:id");
    $stmt->bindParam(":id",$id);
    $stmt->execute();
    header('location: index_articulos.php');
}
?>
```



