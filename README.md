<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
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

    .menu-container {
      padding: 20px;
    }

    .category {
      margin-bottom: 15px;
      border-radius: 6px;
      overflow: hidden;
      background-color: #ffffff;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .category h2 {
      margin: 0;
      padding: 12px 16px;
      background-color: #e0f1e0;
      font-size: 1.2rem;
      cursor: pointer;
    }

    .items {
      display: none;
      padding: 10px 16px;
      display: flex;
      flex-direction: column;
      gap: 10px;
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
  </style>
</head>
<body>

<header>
  <h1>Menú Punto Verde</h1>
  <p>Selecciona lo que deseas agregar a tu compra</p>
</header>

<div class="menu-container">

  <!-- Promociones -->
  <div class="category" onclick="toggleItems(this)">
    <h2>🌟 Promociones</h2>
    <div class="items">
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Promo">
        <span>Baguette + Agua fresca — $70</span>
        <button onclick="agregarAlCarrito('Baguette + Agua fresca', 70)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Promo">
        <span>Wrap + Agua fresca — $65</span>
        <button onclick="agregarAlCarrito('Wrap + Agua fresca', 65)">Agregar</button>
      </div>
    </div>
  </div>

  <!-- Bebidas -->
  <div class="category" onclick="toggleItems(this)">
    <h2>🥤 Bebidas</h2>
    <div class="items">
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Bebida">
        <span>Agua de maracuyá — $25</span>
        <button onclick="agregarAlCarrito('Agua de maracuyá', 25)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Bebida">
        <span>Agua de ciruela — $25</span>
        <button onclick="agregarAlCarrito('Agua de ciruela', 25)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Bebida">
        <span>Agua de guanábana — $25</span>
        <button onclick="agregarAlCarrito('Agua de guanábana', 25)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Bebida">
        <span>Agua del día — $20</span>
        <button onclick="agregarAlCarrito('Agua del día', 20)">Agregar</button>
      </div>
    </div>
  </div>

  <!-- Alimentos -->
  <div class="category" onclick="toggleItems(this)">
    <h2>🥪 Alimentos</h2>
    <div class="items">
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Alimento">
        <span>Baguette de jamón serrano — $60</span>
        <button onclick="agregarAlCarrito('Baguette jamón serrano', 60)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Alimento">
        <span>Wrap de pollo a la parrilla — $55</span>
        <button onclick="agregarAlCarrito('Wrap pollo parrilla', 55)">Agregar</button>
      </div>
      <div class="item-card">
        <img src="ruta-a-tu-imagen.jpg" alt="Alimento">
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

</div>

<script>
  function toggleItems(category) {
    const items = category.querySelector('.items');
    const allItems = document.querySelectorAll('.items');
    allItems.forEach(i => {
      if (i !== items) i.style.display = 'none';
    });
    items.style.display = (items.style.display === 'block') ? 'none' : 'block';
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
