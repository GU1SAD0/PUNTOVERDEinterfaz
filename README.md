<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Punto Verde</title>
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

    .admin-button {
      position: fixed;
      bottom: 20px;
      left: 20px;
      background-color: var(--accent);
      color: white;
      padding: 8px 14px;
      border: none;
      border-radius: 50px;
      font-size: 1rem;
      cursor: pointer;
      box-shadow: 0 2px 6px var(--shadow);
      z-index: 999;
    }

    .modal {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background-color: rgba(0,0,0,0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
    }

    .modal-content {
      background-color: var(--card-bg);
      padding: 20px;
      border-radius: 8px;
      text-align: center;
      box-shadow: 0 2px 10px var(--shadow);
    }

    .modal-content input {
      padding: 8px;
      width: 200px;
      margin-bottom: 10px;
    }

    .ocultar { display: none; }
  </style>
</head>
<body>
  <body>
  <header>
    <h1>Menú Punto Verde</h1>
  </header>

  <div class="categorias-scroll">
    <div class="card-categoria" onclick="mostrarCategoria('promos')">
      <div class="imagen-categoria" style="background-image: url('img/promo.jpg');"></div>
      <div class="nombre-categoria">Promociones</div>
    </div>
    <div class="card-categoria" onclick="mostrarCategoria('bebidas')">
      <div class="imagen-categoria" style="background-image: url('img/bebida.jpg');"></div>
      <div class="nombre-categoria">Bebidas</div>
    </div>
    <div class="card-categoria" onclick="mostrarCategoria('alimentos')">
      <div class="imagen-categoria" style="background-image: url('img/alimento.jpg');"></div>
      <div class="nombre-categoria">Alimentos</div>
    </div>
  </div>

  <div id="promos" class="contenido-categoria">
    <h2>Promociones</h2>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Combo Wrap + Agua</h3>
        <p>$65.00</p>
        <button onclick="agregarAlCarrito('Combo Wrap + Agua', 65)">Agregar</button>
      </div>
    </div>
  </div>

  <div id="bebidas" class="contenido-categoria">
    <h2>Bebidas</h2>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Agua de Maracuyá</h3>
        <p>$20.00</p>
        <button onclick="agregarAlCarrito('Agua de Maracuyá', 20)">Agregar</button>
      </div>
      <div class="item-card">
        <h3>Agua de Ciruela</h3>
        <p>$20.00</p>
        <button onclick="agregarAlCarrito('Agua de Ciruela', 20)">Agregar</button>
      </div>
      <div class="item-card">
        <h3>Agua de Guanábana</h3>
        <p>$20.00</p>
        <button onclick="agregarAlCarrito('Agua de Guanábana', 20)">Agregar</button>
      </div>
    </div>
  </div>

  <div id="alimentos" class="contenido-categoria">
    <h2>Alimentos</h2>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Baguette de Pollo</h3>
        <p>$40.00</p>
        <button onclick="agregarAlCarrito('Baguette de Pollo', 40)">Agregar</button>
      </div>
      <div class="item-card">
        <h3>Cuernito de Jamón</h3>
        <p>$35.00</p>
        <button onclick="agregarAlCarrito('Cuernito de Jamón', 35)">Agregar</button>
      </div>

        <div id="carrito" class="ocultar">
    <h2>Carrito de Compras</h2>
    <ul id="lista-carrito"></ul>
    <p><strong>Total: $<span id="total">0.00</span></strong></p>
    <button onclick="finalizarCompra()">Finalizar compra</button>
  </div>

  <button class="boton-flotante" onclick="toggleCarrito()">🛒 Ver carrito</button>
  <button class="admin-button" onclick="abrirModal()">⚙️ Acceso Personal</button>

  <div id="adminModal" class="modal ocultar">
    <div class="modal-content">
      <h3>Acceso Personal Autorizado</h3>
      <input type="password" id="adminPass" placeholder="Ingresa la contraseña" />
      <br />
      <button onclick="validarAcceso()">Entrar</button>
    </div>
  </div>

  <div id="adminPanel" class="contenido-categoria ocultar">
    <h2>Panel de Administración</h2>
    <ul>
      <li>Ventas del día: $<span id="ventasDia">0.00</span></li>
      <li>Ventas semanales: $<span id="ventasSemana">0.00</span></li>
      <li>Productos más vendidos: <span id="topProductos">Baguette de Pollo</span></li>
      <li>Promociones efectivas: <span id="promoEfectiva">Combo Wrap + Agua</span></li>
      <li>Ticket promedio: $<span id="ticketPromedio">52.50</span></li>
    </ul>
  </div>
    <script>
    let carrito = JSON.parse(localStorage.getItem('carrito')) || [];

    function mostrarCategoria(id) {
      document.querySelectorAll('.contenido-categoria').forEach(div => div.style.display = 'none');
      document.getElementById(id).style.display = 'block';
    }

    function agregarAlCarrito(nombre, precio) {
      carrito.push({ nombre, precio });
      localStorage.setItem('carrito', JSON.stringify(carrito));
      actualizarCarrito();
    }

    function actualizarCarrito() {
      const lista = document.getElementById('lista-carrito');
      lista.innerHTML = '';
      let total = 0;
      carrito.forEach((item, index) => {
        total += item.precio;
        const li = document.createElement('li');
        li.innerHTML = `${item.nombre} - $${item.precio.toFixed(2)}
          <button class="remove-btn" onclick="eliminarDelCarrito(${index})">Quitar</button>`;
        lista.appendChild(li);
      });
      document.getElementById('total').textContent = total.toFixed(2);
    }

    function eliminarDelCarrito(index) {
      carrito.splice(index, 1);
      localStorage.setItem('carrito', JSON.stringify(carrito));
      actualizarCarrito();
    }

    function toggleCarrito() {
      const carritoDiv = document.getElementById('carrito');
      carritoDiv.classList.toggle('ocultar');
    }

    function finalizarCompra() {
      alert("¡Gracias por tu compra! Total: $" + document.getElementById('total').textContent);
      carrito = [];
      localStorage.removeItem('carrito');
      actualizarCarrito();
    }

    function abrirModal() {
      document.getElementById('adminModal').classList.remove('ocultar');
    }

    function validarAcceso() {
      const pass = document.getElementById('adminPass').value;
      if (pass === "NDENTRAB") {
        document.getElementById('adminModal').classList.add('ocultar');
        document.getElementById('adminPanel').classList.remove('ocultar');
      } else {
        alert("Contraseña incorrecta");
      }
    }

    // Inicializa el carrito si ya había algo guardado
    document.addEventListener("DOMContentLoaded", actualizarCarrito);
  </script>

</body>
</html>
    </div>
  </div>
