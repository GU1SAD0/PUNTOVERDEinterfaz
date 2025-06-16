
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

    .categorias {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
      padding: 20px;
    }

    .card-categoria {
      width: 90%;
      max-width: 400px;
      background-color: #fff;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    .card-categoria:hover {
      transform: scale(1.02);
    }

    .imagen-categoria {
      width: 100%;
      height: 180px;
      background-color: #d8ecd6; /* color de fondo mientras no haya imagen */
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

    /* Estilos para el contenido desplegado (oculto inicialmente) */
    .contenido-categoria {
      display: none;
      padding: 20px;
    }

    /* Opcional: puedes ocultar las categorías cuando se abra una */
    .ocultar {
      display: none;
    }
  </style>
</head>
<body>

<header>
  <h1>Menú Punto Verde</h1>
  <p>Toca una categoría para comenzar tu pedido</p>
</header>

<!-- Tarjetas de categorías -->
<div class="categorias">
  <div class="card-categoria" onclick="mostrarCategoria('promos')">
    <div class="imagen-categoria" style="background-image: url('ruta-a-imagen-promos.jpg');"></div>
    <div class="nombre-categoria">🌟 Promociones</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('bebidas')">
    <div class="imagen-categoria" style="background-image: url('ruta-a-imagen-bebidas.jpg');"></div>
    <div class="nombre-categoria">🥤 Bebidas</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('alimentos')">
    <div class="imagen-categoria" style="background-image: url('ruta-a-imagen-alimentos.jpg');"></div>
    <div class="nombre-categoria">🥪 Alimentos</div>
  </div>
</div>

<!-- Aquí iría el contenido que ya programamos (productos, carrito, etc.) -->
<div id="promos" class="contenido-categoria">
  <!-- Aquí se insertará el bloque de promociones al seleccionarlas -->
</div>
<div id="bebidas" class="contenido-categoria">
  <!-- Aquí se insertará el bloque de bebidas al seleccionarlas -->
</div>
<div id="alimentos" class="contenido-categoria">
  <!-- Aquí se insertará el bloque de alimentos al seleccionarlas -->
</div>

<script>
  function mostrarCategoria(id) {
    // Oculta tarjetas de selección
    document.querySelector('.categorias').classList.add('ocultar');

    // Muestra la categoría elegida
    document.getElementById(id).style.display = 'block';

    // Aquí podrías cargar dinámicamente el contenido o ya tenerlo listo
  }
</script>

</body>
</html>
