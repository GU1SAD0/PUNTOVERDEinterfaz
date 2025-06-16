<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Punto Verde | Menú</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f0f5f0;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #7BAE7F;
      color: white;
      text-align: center;
      padding: 1.5rem 0;
    }

    /* Contenedor horizontal con scroll tipo carrusel */
    .categorias-scroll {
      display: flex;
      overflow-x: auto;
      gap: 20px;
      padding: 20px;
      scroll-snap-type: x mandatory;
      -webkit-overflow-scrolling: touch;
    }

    .card-categoria {
      flex: 0 0 auto;
      width: 250px;
      background-color: #fff;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      scroll-snap-align: start;
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    .card-categoria:hover {
      transform: scale(1.03);
    }

    .imagen-categoria {
      width: 100%;
      height: 160px;
      background-color: #d8ecd6; /* fondo mientras no haya imagen */
      background-size: cover;
      background-position: center;
    }

    .nombre-categoria {
      text-align: center;
      padding: 12px;
      font-size: 1.3rem;
      font-weight: bold;
      color: #444;
    }

    .contenido-categoria {
      display: none;
      padding: 20px;
    }

    .ocultar {
      display: none;
    }
  </style>
</head>
<body>

<header>
  <h1>Menú Punto Verde</h1>
  <p>Selecciona una categoría para comenzar tu pedido</p>
</header>

<!-- 🔄 Scroll horizontal de categorías -->
<div class="categorias-scroll">
  <div class="card-categoria" onclick="mostrarCategoria('promos')">
    <div class="imagen-categoria" style="background-image: url('ruta-promos.jpg');"></div>
    <div class="nombre-categoria">🌟 Promociones</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('bebidas')">
    <div class="imagen-categoria" style="background-image: url('ruta-bebidas.jpg');"></div>
    <div class="nombre-categoria">🥤 Bebidas</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('alimentos')">
    <div class="imagen-categoria" style="background-image: url('ruta-alimentos.jpg');"></div>
    <div class="nombre-categoria">🥪 Alimentos</div>
  </div>

  <!-- Puedes agregar más categorías si algún día expandes -->
</div>

<!-- 🔽 Aquí se desplegarán los productos al seleccionar una categoría -->
<div id="promos" class="contenido-categoria"></div>
<div id="bebidas" class="contenido-categoria"></div>
<div id="alimentos" class="contenido-categoria"></div>

<script>
  function mostrarCategoria(id) {
    // Ocultar contenedor de tarjetas
    document.querySelector('.categorias-scroll').classList.add('ocultar');

    // Mostrar contenido seleccionado
    document.getElementById(id).style.display = 'block';

    // Puedes aquí insertar el contenido dinámico (productos + carrito)
  }
</script>

</body>
</html>
