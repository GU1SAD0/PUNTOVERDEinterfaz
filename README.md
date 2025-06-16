<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Menú Punto Verde</title>
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
      background-color: #d8ecd6;
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

    .items {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .item-card {
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: #f8fff8;
      padding: 15px;
      border: 1px solid #cceccc;
      border-radius: 6px;
      text-align: center;
    }

    .item-card img {
      width: 100px;
      height: 100px;
      object-fit: cover;
      margin-bottom: 10px;
      border-radius: 8px;
    }

    .item-card button {
      background-color: #7BAE7F;
      color: white;
      border: none;
      padding: 6px 12px;
      border-radius: 4px;
      cursor: pointer;
      margin-top: 8px;
    }

    .item-card button:hover {
      background-color: #679b6b;
    }

    #carrito {
      background-color: #fff;
      border-top: 2px solid #7BAE7F;
      padding: 15px 20px;
      margin-top: 30px;
    }

    #carrito h3 {
      margin-top: 0;
    }

    #lista-carrito li {
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .remove-btn {
      background-color: #e74c3c;
      color: white;
      border: none;
      padding: 4px 8px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.8rem;
    }

    .remove-btn:hover {
      background-color: #c0392b;
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

<!-- Tarjetas de categorías (scroll horizontal) -->
<div class="categorias-scroll" id="menu-categorias">
  <div class="card-categoria" onclick="mostrarCategoria('promos')">
    <div class="imagen-categoria" style="background-image: url('img/promos.jpg');"></div>
    <div class="nombre-categoria">🌟 Promociones</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('bebidas')">
    <div class="imagen-categoria" style="background-image: url('img/bebidas.jpg');"></div>
    <div class="nombre-categoria">🥤 Bebidas</div>
  </div>

  <div class="card-categoria" onclick="mostrarCategoria('alimentos')">
    <div class="imagen-categoria" style="background-image: url('img/alimentos.jpg');"></div>
    <div class="nombre-categoria">🥪 Alimentos</div>
  </div>
</div>

<!-- Contenido de cada categoría -->
<div id="promos" class="contenido-categoria">
  <h2>🌟 Promociones</h2>
  <div class="items">
    <div class="item-card">
      <img src="img/promocion1.jpg" alt="Promo 1">
      <span>Baguette + Agua fresca — $70</span>
      <button onclick="agregarAlCarrito('Baguette + Agua fresca', 70)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/promocion2.jpg" alt="Promo 2">
      <span>Wrap + Agua fresca — $65</span>
      <button onclick="agregarAlCarrito('Wrap + Agua fresca', 65)">Agregar</button>
    </div>
  </div>
</div>

<div id="bebidas" class="contenido-categoria">
  <h2>🥤 Bebidas</h2>
  <div class="items">
    <div class="item-card">
      <img src="img/maracuya.jpg" alt="Maracuyá">
      <span>Agua de maracuyá — $25</span>
      <button onclick="agregarAlCarrito('Agua de maracuyá', 25)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/ciruela.jpg" alt="Ciruela">
      <span>Agua de ciruela — $25</span>
      <button onclick="agregarAlCarrito('Agua de ciruela', 25)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/guanabana.jpg" alt="Guanábana">
      <span>Agua de guanábana — $25</span>
      <button onclick="agregarAlCarrito('Agua de guanábana', 25)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/del-dia.jpg" alt="Agua del día">
      <span>Agua del día — $20</span>
      <button onclick="agregarAlCarrito('Agua del día', 20)">Agregar</button>
    </div>
  </div>
</div>

<div id="alimentos" class="contenido-categoria">
  <h2>🥪 Alimentos</h2>
  <div class="items">
    <div class="item-card">
      <img src="img/jamon.jpg" alt="Jamon serrano">
      <span>Baguette jamón serrano — $60</span>
      <button onclick="agregarAlCarrito('Baguette jamón serrano', 60)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/wrap.jpg" alt="Wrap pollo">
      <span>Wrap de pollo a la parrilla — $55</span>
      <button onclick="agregarAlCarrito('Wrap pollo parrilla', 55)">Agregar</button>
    </div>
    <div class="item-card">
      <img src="img/atun.jpg" alt="Cuernito atún">
      <span>Cuernito de atún — $45</span>
      <button onclick="agregarAlCarrito('Cuernito de atún', 45)">Agregar</button>
    </div>
  </div>
</div>

<!-- Carrito -->
<div id="carrito">
  <h3>🛒 Tu compra:</h3>
  <ul id="lista-carrito"></ul>
  <p><strong>Total: $<span id="total">0</span></strong></p>
</div>

<script>
  function mostrarCategoria(id) {
    document.getElementById('menu-categorias').classList.add('ocultar');
    document.getElementById(id).style.display = 'block';
  }

  let total = 0;
  const listaCarrito = document.getElementById('lista-carrito');
  const totalDisplay = document.getElementById('total');

  function agregarAlCarrito(nombre, precio) {
    const item = document.createElement('li');
    item.textContent = `${nombre} — $${precio}`;

    const btnEliminar = document.createElement('button');
    btnEliminar.textContent = 'Quitar';
    btnEliminar.classList.add('remove-btn');
    btnEliminar.onclick = function () {
      item.remove();
      total -= precio;
      totalDisplay.textContent = total;
    };

    item.appendChild(btnEliminar);
    listaCarrito.appendChild(item);
    total += precio;
    totalDisplay.textContent = total;
  }
</script>

</body>
</html>
