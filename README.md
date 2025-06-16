<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Menú Punto Verde</title>
  <style>
    :root {
      --bg: #f0f5f0;
      --card-bg: #ffffff;
      --text: #333;
      --accent: #7BAE7F;
      --shadow: rgba(0, 0, 0, 0.1);
    }

    body.dark {
      --bg: #222;
      --card-bg: #333;
      --text: #f0f0f0;
      --shadow: rgba(255, 255, 255, 0.1);
    }

    body {
      font-family: 'Arial', sans-serif;
      background-color: var(--bg);
      color: var(--text);
      margin: 0;
      padding: 0;
      transition: background-color 0.3s, color 0.3s;
    }

    header {
      background-color: var(--accent);
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
      background-color: var(--card-bg);
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 2px 10px var(--shadow);
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
    }

    .contenido-categoria {
      display: none;
      padding: 20px;
    }

    .scroll-productos {
      display: flex;
      overflow-x: auto;
      gap: 16px;
      scroll-snap-type: x mandatory;
      -webkit-overflow-scrolling: touch;
    }

    .item-card {
      flex: 0 0 auto;
      scroll-snap-align: start;
      width: 220px;
      background-color: var(--card-bg);
      padding: 15px;
      border: 1px solid #cceccc;
      border-radius: 6px;
      text-align: center;
      box-shadow: 0 1px 4px var(--shadow);
    }

    .item-card img {
      width: 100px;
      height: 100px;
      object-fit: cover;
      margin-bottom: 10px;
      border-radius: 8px;
    }

    .item-card button {
      background-color: var(--accent);
      color: white;
      border: none;
      padding: 6px 12px;
      border-radius: 4px;
      cursor: pointer;
      margin-top: 8px;
    }

    #carrito {
      background-color: var(--card-bg);
      border-top: 2px solid var(--accent);
      padding: 15px 20px;
      margin-top: 30px;
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

    .boton-flotante {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background-color: var(--accent);
      color: white;
      padding: 10px 16px;
      border: none;
      border-radius: 50px;
      font-size: 1.2rem;
      cursor: pointer;
      box-shadow: 0 2px 6px var(--shadow);
      z-index: 999;
    }

    .ocultar { display: none; }
  </style>
</head>
<body>

<header>
  <h1>Menú Punto Verde</h1>
  <p>Selecciona una categoría para comenzar tu pedido</p>
</header>

<!-- Categorías -->
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

<!-- Contenido dinámico -->
<div id="promos" class="contenido-categoria">
  <h2>🌟 Promociones</h2>
  <div class="scroll-productos">
    <div class="item-card">
      <span>Baguette + Agua fresca — $70</span>
      <button onclick="agregarAlCarrito('Baguette + Agua fresca', 70)">Agregar</button>
    </div>
  </div>
</div>

<div id="bebidas" class="contenido-categoria">
  <h2>🥤 Bebidas</h2>
  <div class="scroll-productos">
    <div class="item-card">
      <span>Agua de maracuyá — $25</span>
      <button onclick="agregarAlCarrito('Agua de maracuyá', 25)">Agregar</button>
    </div>
  </div>
</div>

<div id="alimentos" class="contenido-categoria">
  <h2>🥪 Alimentos</h2>
  <div class="scroll-productos">
    <div class="item-card">
      <span>Wrap pollo parrilla — $55</span>
      <button onclick="agregarAlCarrito('Wrap pollo parrilla', 55)">Agregar</button>
    </div>
  </div>
</div>

<!-- Carrito -->
<div id="carrito" class="ocultar">
  <h3>🛒 Tu compra:</h3>
  <ul id="lista-carrito"></ul>
  <p><strong>Total: $<span id="total">0</span></strong></p>
  <button onclick="finalizarCompra()">✅ Finalizar compra</button>
</div>

<!-- Botón flotante -->
<button class="boton-flotante" onclick="toggleCarrito()">🛒 Ver carrito</button>

<script>
  const carrito = document.getElementById('carrito');
  const listaCarrito = document.getElementById('lista-carrito');
  const totalDisplay = document.getElementById('total');
  let total = 0;

  window.onload = function () {
    if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
      document.body.classList.add('dark');
    }

    const guardado = localStorage.getItem('carrito');
    if (guardado) {
      const datos = JSON.parse(guardado);
      datos.items.forEach(p => agregarAlCarrito(p.nombre, p.precio, true));
      total = datos.total;
      totalDisplay.textContent = total;
    }
  };

  function mostrarCategoria(id) {
    document.getElementById('menu-categorias').classList.add('ocultar');
    document.getElementById(id).style.display = 'block';
  }

  function toggleCarrito() {
    carrito.classList.toggle('ocultar');
  }

  function agregarAlCarrito(nombre, precio, silencioso = false) {
    const item = document.createElement('li');
    item.textContent = `${nombre} — $${precio}`;
    const btn = document.createElement('button');
    btn.textContent = 'Quitar';
    btn.className = 'remove-btn';
    btn.onclick = function () {
      item.remove();
      total -= precio;
      totalDisplay.textContent = total;
      guardarCarrito();
    };
    item.appendChild(btn);
    listaCarrito.appendChild(item);
    total += precio;
    totalDisplay.textContent = total;
    guardarCarrito();
  }

  function guardarCarrito() {
    const items = [];
    listaCarrito.querySelectorAll('li').forEach(li => {
      const texto = li.textContent.replace('Quitar', '').trim();
      const partes = texto.split('— $');
      items.push({ nombre: partes[0].trim(), precio: parseFloat(partes[1]) });
    });
    localStorage.setItem('carrito', JSON.stringify({ items, total }));
  }

  function finalizarCompra() {
    alert('Gracias por tu compra. Total: $' + total);
    listaCarrito.innerHTML = '';
    total = 0;
    totalDisplay.textContent = total;
    localStorage.removeItem('carrito');
  }
</script>

</body>
</html>
