<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Menú Punto Verde</title>
  <style>
    :root {
      --verde-principal: #7BAE7F;
      --verde-oscuro: #5a8a5e;
      --beige: #f5f2e8;
      --blanco: #ffffff;
      --texto-principal: #2c3e2d;
      --texto-secundario: #5a6b5d;
      --sombra-suave: rgba(123, 174, 127, 0.15);
      --sombra-fuerte: rgba(0, 0, 0, 0.1);
      --borde-suave: rgba(123, 174, 127, 0.2);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, var(--beige) 0%, #f8f6f0 100%);
      color: var(--texto-principal);
      overflow-x: hidden;
      min-height: 100vh;
    }

    header {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      text-align: center;
      padding: 2rem 1rem;
      font-size: 2.2rem;
      font-weight: 600;
      box-shadow: 0 4px 20px var(--sombra-suave);
      position: relative;
      overflow: hidden;
    }

    header::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
      animation: shimmer 3s ease-in-out infinite;
    }

    @keyframes shimmer {
      0%, 100% { transform: translateX(-50%) translateY(-50%) rotate(0deg); }
      50% { transform: translateX(-30%) translateY(-30%) rotate(5deg); }
    }

    .logo-texto {
      position: relative;
      z-index: 1;
      text-shadow: 0 2px 4px rgba(0,0,0,0.2);
    }

    .categorias-container {
      padding: 2rem 1rem;
      background: var(--blanco);
      margin: 1rem;
      border-radius: 15px;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
    }

    .categorias-titulo {
      text-align: center;
      font-size: 1.5rem;
      color: var(--verde-oscuro);
      margin-bottom: 1.5rem;
      font-weight: 600;
    }

    .categorias-scroll {
      display: flex;
      overflow-x: auto;
      gap: 20px;
      padding: 10px 5px 20px 5px;
      scroll-behavior: smooth;
      -webkit-overflow-scrolling: touch;
    }

    .categorias-scroll::-webkit-scrollbar {
      height: 8px;
    }

    .categorias-scroll::-webkit-scrollbar-track {
      background: var(--beige);
      border-radius: 10px;
    }

    .categorias-scroll::-webkit-scrollbar-thumb {
      background: var(--verde-principal);
      border-radius: 10px;
    }

    .card-categoria {
      flex: 0 0 auto;
      width: 250px;
      background: var(--blanco);
      border-radius: 15px;
      box-shadow: 0 6px 20px var(--sombra-suave);
      cursor: pointer;
      overflow: hidden;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      border: 2px solid transparent;
    }

    .card-categoria:hover {
      transform: translateY(-8px) scale(1.02);
      box-shadow: 0 15px 35px var(--sombra-fuerte);
      border-color: var(--verde-principal);
    }

    .card-categoria.activa {
      border-color: var(--verde-principal);
      box-shadow: 0 0 0 3px var(--sombra-suave);
    }

    .imagen-categoria {
      height: 160px;
      background: linear-gradient(45deg, var(--verde-principal), var(--verde-oscuro));
      background-size: cover;
      background-position: center;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .imagen-categoria::before {
      content: '';
      position: absolute;
      inset: 0;
      background: rgba(0,0,0,0.2);
    }

    .categoria-icono {
      font-size: 3rem;
      position: relative;
      z-index: 1;
      color: white;
      text-shadow: 0 2px 4px rgba(0,0,0,0.3);
    }

    .nombre-categoria {
      padding: 1rem;
      text-align: center;
      font-weight: 600;
      font-size: 1.2rem;
      color: var(--verde-oscuro);
    }

    .contenido-categoria {
      display: none;
      padding: 2rem 1rem;
      margin: 1rem;
      background: var(--blanco);
      border-radius: 15px;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
      animation: fadeIn 0.5s ease-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .categoria-header {
      text-align: center;
      margin-bottom: 2rem;
    }

    .categoria-header h2 {
      color: var(--verde-oscuro);
      font-size: 2rem;
      margin-bottom: 0.5rem;
    }

    .categoria-header p {
      color: var(--texto-secundario);
      font-size: 1.1rem;
    }

    .scroll-productos {
      display: flex;
      overflow-x: auto;
      gap: 20px;
      padding: 10px 5px 20px 5px;
      scroll-behavior: smooth;
      -webkit-overflow-scrolling: touch;
    }

    .scroll-productos::-webkit-scrollbar {
      height: 8px;
    }

    .scroll-productos::-webkit-scrollbar-track {
      background: var(--beige);
      border-radius: 10px;
    }

    .scroll-productos::-webkit-scrollbar-thumb {
      background: var(--verde-principal);
      border-radius: 10px;
    }

    .item-card {
      flex: 0 0 auto;
      width: 280px;
      background: var(--blanco);
      padding: 1.5rem;
      border: 2px solid var(--borde-suave);
      border-radius: 15px;
      text-align: center;
      box-shadow: 0 4px 15px var(--sombra-suave);
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    .item-card::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: linear-gradient(45deg, transparent, rgba(123, 174, 127, 0.05), transparent);
      transform: rotate(45deg);
      transition: all 0.5s ease;
      opacity: 0;
    }

    .item-card:hover::before {
      opacity: 1;
      animation: shine 0.8s ease-out;
    }

    @keyframes shine {
      0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
      100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
    }

    .item-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 12px 30px var(--sombra-fuerte);
      border-color: var(--verde-principal);
    }

    .item-card h3 {
      color: var(--verde-oscuro);
      font-size: 1.3rem;
      margin-bottom: 0.8rem;
      position: relative;
      z-index: 1;
    }

    .item-card .precio {
      font-size: 1.8rem;
      font-weight: 700;
      color: var(--verde-principal);
      margin: 1rem 0;
      position: relative;
      z-index: 1;
    }

    .item-card .descripcion {
      color: var(--texto-secundario);
      font-size: 0.95rem;
      margin-bottom: 1.5rem;
      line-height: 1.4;
      position: relative;
      z-index: 1;
    }

    .btn-agregar {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 25px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: 600;
      transition: all 0.3s ease;
      position: relative;
      z-index: 1;
      box-shadow: 0 4px 15px var(--sombra-suave);
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .btn-agregar:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px var(--sombra-fuerte);
    }

    .btn-agregar:active {
      transform: translateY(0);
    }

    .boton-flotante {
      position: fixed;
      bottom: 30px;
      right: 30px;
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      padding: 15px 25px;
      border: none;
      border-radius: 50px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
      z-index: 999;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .boton-flotante:hover {
      transform: translateY(-3px) scale(1.05);
      box-shadow: 0 15px 35px var(--sombra-fuerte);
    }

    .carrito-badge {
      background: var(--blanco);
      color: var(--verde-principal);
      border-radius: 50%;
      width: 24px;
      height: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.8rem;
      font-weight: 700;
      margin-left: 5px;
    }

    #carrito {
      display: none;
      position: fixed;
      top: 0;
      right: 0;
      width: 400px;
      height: 100vh;
      background: var(--blanco);
      box-shadow: -10px 0 30px var(--sombra-fuerte);
      z-index: 1000;
      overflow-y: auto;
      transform: translateX(100%);
      transition: transform 0.3s ease;
    }

    #carrito.mostrar {
      transform: translateX(0);
    }

    .carrito-header {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      padding: 2rem 1.5rem;
      position: sticky;
      top: 0;
      z-index: 10;
    }

    .carrito-header h2 {
      margin-bottom: 0.5rem;
    }

    .btn-cerrar-carrito {
      position: absolute;
      top: 1rem;
      right: 1rem;
      background: rgba(255,255,255,0.2);
      color: white;
      border: none;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      cursor: pointer;
      font-size: 1.2rem;
      transition: all 0.3s ease;
    }

    .btn-cerrar-carrito:hover {
      background: rgba(255,255,255,0.3);
      transform: scale(1.1);
    }

    .carrito-contenido {
      padding: 1.5rem;
    }

    .carrito-vacio {
      text-align: center;
      color: var(--texto-secundario);
      font-size: 1.1rem;
      margin: 3rem 0;
    }

    .carrito-vacio .emoji {
      font-size: 3rem;
      margin-bottom: 1rem;
      display: block;
    }

    .item-carrito {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem;
      margin-bottom: 1rem;
      background: var(--beige);
      border-radius: 10px;
      transition: all 0.3s ease;
    }

    .item-carrito:hover {
      transform: translateX(5px);
      box-shadow: 5px 5px 15px var(--sombra-suave);
    }

    .item-info h4 {
      color: var(--verde-oscuro);
      margin-bottom: 0.3rem;
    }

    .item-precio {
      font-weight: 700;
      color: var(--verde-principal);
      font-size: 1.1rem;
    }

    .btn-eliminar {
      background: #ff6b6b;
      color: white;
      border: none;
      border-radius: 50%;
      width: 35px;
      height: 35px;
      cursor: pointer;
      font-size: 1.1rem;
      transition: all 0.3s ease;
    }

    .btn-eliminar:hover {
      background: #ff5252;
      transform: scale(1.1);
    }

    .carrito-total {
      border-top: 2px solid var(--verde-principal);
      padding-top: 1.5rem;
      margin-top: 2rem;
    }

    .total-precio {
      font-size: 1.8rem;
      font-weight: 700;
      color: var(--verde-principal);
      text-align: center;
      margin-bottom: 1.5rem;
    }

    .btn-finalizar {
      width: 100%;
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      border: none;
      padding: 15px;
      border-radius: 10px;
      font-size: 1.2rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .btn-finalizar:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px var(--sombra-fuerte);
    }

    .admin-button {
      position: fixed;
      bottom: 30px;
      left: 30px;
      background: linear-gradient(135deg, #6c757d 0%, #495057 100%);
      color: white;
      padding: 12px 20px;
      border: none;
      border-radius: 50px;
      font-size: 0.9rem;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      z-index: 999;
      transition: all 0.3s ease;
    }

    .admin-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(0,0,0,0.3);
    }

    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.6);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2000;
      backdrop-filter: blur(5px);
    }

    .modal-content {
      background: var(--blanco);
      padding: 2.5rem;
      border-radius: 15px;
      text-align: center;
      box-shadow: 0 20px 60px rgba(0,0,0,0.3);
      max-width: 400px;
      width: 90%;
      animation: modalSlideIn 0.3s ease-out;
    }

    @keyframes modalSlideIn {
      from { transform: translateY(-50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .modal-content h3 {
      color: var(--verde-oscuro);
      margin-bottom: 1.5rem;
      font-size: 1.5rem;
    }

    .modal-content input {
      padding: 12px 16px;
      width: 100%;
      margin-bottom: 1.5rem;
      border: 2px solid var(--borde-suave);
      border-radius: 8px;
      font-size: 1rem;
      transition: border-color 0.3s ease;
    }

    .modal-content input:focus {
      outline: none;
      border-color: var(--verde-principal);
      box-shadow: 0 0 0 3px var(--sombra-suave);
    }

    .modal-buttons {
      display: flex;
      gap: 1rem;
      margin-top: 1rem;
    }

    .btn-modal {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .btn-entrar {
      background: var(--verde-principal);
      color: white;
    }

    .btn-entrar:hover {
      background: var(--verde-oscuro);
      transform: translateY(-1px);
    }

    .btn-cancelar {
      background: #f8f9fa;
      color: var(--texto-secundario);
      border: 1px solid var(--borde-suave);
    }

    .btn-cancelar:hover {
      background: #e9ecef;
    }

    #adminPanel {
      padding: 2rem 1rem;
      margin: 1rem;
      background: var(--blanco);
      border-radius: 15px;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
      animation: fadeIn 0.5s ease-out;
    }

    .admin-header {
      text-align: center;
      margin-bottom: 2rem;
      padding-bottom: 1rem;
      border-bottom: 2px solid var(--verde-principal);
    }

    .admin-header h2 {
      color: var(--verde-oscuro);
      font-size: 2rem;
      margin-bottom: 0.5rem;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .stat-card {
      background: linear-gradient(135deg, var(--beige) 0%, #f0f0f0 100%);
      padding: 1.5rem;
      border-radius: 10px;
      border-left: 4px solid var(--verde-principal);
      transition: all 0.3s ease;
    }

    .stat-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px var(--sombra-suave);
    }

    .stat-title {
      color: var(--texto-secundario);
      font-size: 0.9rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 0.5rem;
    }

    .stat-value {
      color: var(--verde-principal);
      font-size: 1.8rem;
      font-weight: 700;
    }

    .btn-cerrar-admin {
      position: fixed;
      top: 2rem;
      right: 2rem;
      background: #ff6b6b;
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      cursor: pointer;
      font-size: 1.2rem;
      z-index: 1001;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
    }

    .btn-cerrar-admin:hover {
      background: #ff5252;
      transform: scale(1.1);
    }

    .oculto {
      display: none !important;
    }

    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 500;
      display: none;
    }

    .overlay.mostrar {
      display: block;
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      .categorias-container, .contenido-categoria, #adminPanel {
        margin: 0.5rem;
      }
      
      #carrito {
        width: 100%;
      }
      
      .item-card {
        width: 240px;
      }
      
      .card-categoria {
        width: 200px;
      }
      
      .stats-grid {
        grid-template-columns: 1fr;
      }
    }

    /* Animaciones adicionales */
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    .boton-flotante.pulse {
      animation: pulse 2s infinite;
    }

    /* Efectos de notificación */
    .notificacion {
      position: fixed;
      top: 2rem;
      right: 2rem;
      background: var(--verde-principal);
      color: white;
      padding: 1rem 1.5rem;
      border-radius: 10px;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
      z-index: 3000;
      animation: slideInRight 0.5s ease-out;
    }

    @keyframes slideInRight {
      from { transform: translateX(100%); }
      to { transform: translateX(0); }
    }
  </style>
</head>
<body>
  <header>
    <div class="logo-texto">🌱 Punto Verde</div>
  </header>

  <div class="categorias-container">
    <h2 class="categorias-titulo">Selecciona una categoría</h2>
    <div class="categorias-scroll">
      <div class="card-categoria" onclick="mostrarCategoria('promos')" data-categoria="promos">
        <div class="imagen-categoria">
          <div class="categoria-icono">🎉</div>
        </div>
        <div class="nombre-categoria">Promociones</div>
      </div>
      <div class="card-categoria" onclick="mostrarCategoria('bebidas')" data-categoria="bebidas">
        <div class="imagen-categoria">
          <div class="categoria-icono">🥤</div>
        </div>
        <div class="nombre-categoria">Bebidas</div>
      </div>
      <div class="card-categoria" onclick="mostrarCategoria('alimentos')" data-categoria="alimentos">
        <div class="imagen-categoria">
          <div class="categoria-icono">🥪</div>
        </div>
        <div class="nombre-categoria">Alimentos</div>
      </div>
    </div>
  </div>

  <div id="promos" class="contenido-categoria">
    <div class="categoria-header">
      <h2>🎉 Promociones Especiales</h2>
      <p>Combos perfectos para ahorrar y disfrutar</p>
    </div>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Combo Wrap + Agua</h3>
        <p class="descripcion">Delicioso wrap de pollo con vegetales frescos + agua natural de tu sabor favorito</p>
        <p class="precio">$65.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Combo Wrap + Agua', 65)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Combo Baguette + Bebida</h3>
        <p class="descripcion">Baguette artesanal recién horneada + agua de fruta natural</p>
        <p class="precio">$55.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Combo Baguette + Bebida', 55)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Combo Estudiante</h3>
        <p class="descripcion">Cuernito de jamón + agua natural + fruta de temporada</p>
        <p class="precio">$45.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Combo Estudiante', 45)">
          Agregar al carrito
        </button>
      </div>
    </div>
  </div>

  <div id="bebidas" class="contenido-categoria">
    <div class="categoria-header">
      <h2>🥤 Bebidas Naturales</h2>
      <p>Aguas frescas preparadas diariamente con frutas naturales</p>
    </div>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Agua de Maracuyá</h3>
        <p class="descripcion">Refrescante agua de maracuyá natural, perfecta para cualquier momento</p>
        <p class="precio">$20.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Agua de Maracuyá', 20)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Agua de Ciruela</h3>
        <p class="descripcion">Agua fresca de ciruela con el toque perfecto de dulzura natural</p>
        <p class="precio">$20.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Agua de Ciruela', 20)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Agua de Guanábana</h3>
        <p class="descripcion">Exótica agua de guanábana con su sabor único y refrescante</p>
        <p class="precio">$22.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Agua de Guanábana', 22)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Agua Natural</h3>
        <p class="descripcion">Agua purificada embotellada, ideal para acompañar tus alimentos</p>
        <p class="precio">$15.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Agua Natural', 15)">
          Agregar al carrito
        </button>
      </div>
    </div>
  </div>

  <div id="alimentos" class="contenido-categoria">
    <div class="categoria-header">
      <h2>🥪 Alimentos Saludables</h2>
      <p>Opciones nutritivas preparadas con ingredientes frescos del día</p>
    </div>
    <div class="scroll-productos">
      <div class="item-card">
        <h3>Baguette de Pollo</h3>
        <p class="descripcion">Pan baguette artesanal con pechuga de pollo, lechuga, tomate y aderezo especial</p>
        <p class="precio">$40.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Baguette de Pollo', 40)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Baguette Vegetariana</h3>
        <p class="descripcion">Pan baguette con aguacate, espinacas, tomate, pepino y aderezo vegano</p>
        <p class="precio">$38.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Baguette Vegetariana', 38)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Wrap de Pollo</h3>
        <p class="descripcion">Tortilla integral con pollo, vegetales frescos y salsa especial</p>
        <p class="precio">$42.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Wrap de Pollo', 42)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Cuernito de Jamón</h3>
        <p class="descripcion">Delicioso cuernito con jamón de pavo, queso y vegetales</p>
        <p class="precio">$35.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Cuernito de Jamón', 35)">
          Agregar al carrito
        </button>
      </div>
      <div class="item-card">
        <h3>Ensalada Verde</h3>
        <p class="descripcion">Mix de lechugas, espinacas, tomate cherry, pepino y aderezo</p>
        <p class="precio">$32.00</p>
        <button class="btn-agregar" onclick="agregarAlCarrito('Ensalada Verde', 32)">
          Agregar al carrito
        </button>
      </div>
    </div>
  </div>

  <!-- Overlay para el carrito -->
  <div class="overlay" id="overlay" onclick="cerrarCarrito()"></div>

  <!-- Carrito lateral -->
  <div id="carrito">
    <div class="carrito-header">
      <h2>🛒 Tu Carrito</h2>
      <button class="btn-cerrar-carrito" onclick="cerrarCarrito()">✕</button>
    </div>
    <div class="carrito-contenido">
      <div id="carrito-items"></div>
      <div class="carrito-total">
        <div class="total-precio">Total: $<span id="total">0.00</span></div>
        <button class="btn-finalizar" onclick="finalizarCompra()">
          Finalizar Compra
        </button>
      </div>
    </div>
  </div>

  <!-- Botones flotantes -->
  <button class="boton-flotante" onclick="abrirCarrito()" id="btnCarrito">
    🛒 Ver carrito
    <span class="carrito-badge" id="carritoBadge">0</span>
  </button>

  <button class="admin-button" onclick="abrirModal()">⚙️ Acceso Personal</button>

  <!-- Toggle modo oscuro -->
  <button class="toggle-dark-mode" onclick="toggleModoOscuro()" id="btnModoOscuro">
    🌙
  </button>

  <!-- Modal de acceso administrativo -->
  <div id="adminModal" class="modal oculto">
    <div class="modal-content">
      <h3>🔐 Acceso Personal Autorizado</h3>
      <input type="password" id="adminPass" placeholder="Ingresa la contraseña" />
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="validarAcceso()">Entrar</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarModal()">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- Panel de administración -->
  <div id="adminPanel" class="oculto">
    <button class="btn-cerrar-admin" onclick="cerrarAdmin()">✕</button>
    <div class="admin-header">
      <h2>📊 Panel de Administración</h2>
      <p>Gestiona tu negocio y revisa las estadísticas</p>
    </div>
    
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-title">Ventas del Día</div>
        <div class="stat-value">$<span id="ventasDia">0.00</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Ventas Semanales</div>
        <div class="stat-value">$<span id="ventasSemana">0.00</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Productos Vendidos Hoy</div>
        <div class="stat-value"><span id="productosVendidos">0</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Ticket Promedio</div>
        <div class="stat-value">$<span id="ticketPromedio">0.00</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Producto Más Vendido</div>
        <div class="stat-value"><span id="topProducto">-</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Promoción Más Efectiva</div>
        <div class="stat-value"><span id="topPromocion">-</span></div>
      </div>
    </div>

    <div class="admin-actions">
      <h3>🛠️ Acciones Administrativas</h3>
      <div class="action-buttons">
        <button class="btn-action" onclick="resetearEstadisticas()">
          🔄 Resetear Estadísticas
        </button>
        <button class="btn-action" onclick="exportarVentas()">
          📄 Exportar Ventas
        </button>
        <button class="btn-action" onclick="mostrarEditarPrecios()">
          💰 Editar Precios
        </button>
      </div>
    </div>
  </div>

  <!-- Panel de edición de precios -->
  <div id="editarPreciosPanel" class="modal oculto">
    <div class="modal-content edit-prices-modal">
      <h3>💰 Editar Precios de Productos</h3>
      <div id="listaPreciosEditar"></div>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="guardarPrecios()">Guardar Cambios</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarEditarPrecios()">Cancelar</button>
      </div>
    </div>
  </div>

<script>
// =====================================
// VARIABLES GLOBALES Y CONFIGURACIÓN
// =====================================

let carrito = JSON.parse(localStorage.getItem('carrito')) || [];
let ventasData = JSON.parse(localStorage.getItem('ventasData')) || {
  ventasDia: 0,
  ventasSemana: 0,
  productosVendidos: 0,
  ticketsRealizados: 0,
  productosContador: {},
  promocionesContador: {},
  ultimaVenta: null
};

// Productos con precios editables
let productos = JSON.parse(localStorage.getItem('productos')) || {
  'Combo Wrap + Agua': { precio: 65, categoria: 'promociones' },
  'Combo Baguette + Bebida': { precio: 55, categoria: 'promociones' },
  'Combo Estudiante': { precio: 45, categoria: 'promociones' },
  'Agua de Maracuyá': { precio: 20, categoria: 'bebidas' },
  'Agua de Ciruela': { precio: 20, categoria: 'bebidas' },
  'Agua de Guanábana': { precio: 22, categoria: 'bebidas' },
  'Agua Natural': { precio: 15, categoria: 'bebidas' },
  'Baguette de Pollo': { precio: 40, categoria: 'alimentos' },
  'Baguette Vegetariana': { precio: 38, categoria: 'alimentos' },
  'Wrap de Pollo': { precio: 42, categoria: 'alimentos' },
  'Cuernito de Jamón': { precio: 35, categoria: 'alimentos' },
  'Ensalada Verde': { precio: 32, categoria: 'alimentos' }
};

// Configuración de modo oscuro
let modoOscuro = localStorage.getItem('modoOscuro') === 'true' || 
                 (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches);

// =====================================
// FUNCIONES DE INICIALIZACIÓN
// =====================================

document.addEventListener('DOMContentLoaded', function() {
  inicializarApp();
});

function inicializarApp() {
  actualizarCarrito();
  actualizarEstadisticas();
  aplicarModoOscuro();
  verificarVentasSemanales();
  
  // Detectar cambios en la preferencia del sistema
  if (window.matchMedia) {
    window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', function(e) {
      if (!localStorage.getItem('modoOscuroManual')) {
        modoOscuro = e.matches;
        aplicarModoOscuro();
      }
    });
  }
}

// =====================================
// FUNCIONES DE CATEGORÍAS Y PRODUCTOS
// =====================================

function mostrarCategoria(id) {
  // Ocultar todas las categorías
  document.querySelectorAll('.contenido-categoria').forEach(div => {
    div.style.display = 'none';
  });
  
  // Remover clase activa de todas las categorías
  document.querySelectorAll('.card-categoria').forEach(card => {
    card.classList.remove('activa');
  });
  
  // Mostrar la categoría seleccionada
  document.getElementById(id).style.display = 'block';
  
  // Agregar clase activa a la categoría seleccionada
  document.querySelector(`[data-categoria="${id}"]`).classList.add('activa');
  
  // Actualizar precios dinámicamente
  actualizarPreciosEnDOM();
}

function actualizarPreciosEnDOM() {
  document.querySelectorAll('.item-card').forEach(card => {
    const nombreProducto = card.querySelector('h3').textContent;
    const precioElement = card.querySelector('.precio');
    const boton = card.querySelector('.btn-agregar');
    
    if (productos[nombreProducto]) {
      precioElement.textContent = `${productos[nombreProducto].precio.toFixed(2)}`;
      boton.setAttribute('onclick', `agregarAlCarrito('${nombreProducto}', ${productos[nombreProducto].precio})`);
    }
  });
}

// =====================================
// FUNCIONES DEL CARRITO
// =====================================

function agregarAlCarrito(nombre, precio) {
  // Usar precio actualizado si existe
  const precioActual = productos[nombre] ? productos[nombre].precio : precio;
  
  carrito.push({ 
    nombre, 
    precio: precioActual,
    id: Date.now() + Math.random() // ID único para cada item
  });
  
  localStorage.setItem('carrito', JSON.stringify(carrito));
  actualizarCarrito();
  mostrarNotificacion(`${nombre} agregado al carrito`);
  
  // Animar el botón del carrito
  const btnCarrito = document.getElementById('btnCarrito');
  btnCarrito.classList.add('pulse');
  setTimeout(() => btnCarrito.classList.remove('pulse'), 1000);
}

function actualizarCarrito() {
  const carritoItems = document.getElementById('carrito-items');
  const totalElement = document.getElementById('total');
  const badge = document.getElementById('carritoBadge');
  
  if (carrito.length === 0) {
    carritoItems.innerHTML = `
      <div class="carrito-vacio">
        <span class="emoji">🛒</span>
        <p>Tu carrito está vacío</p>
        <p>¡Agrega algunos productos deliciosos!</p>
      </div>
    `;
  } else {
    carritoItems.innerHTML = carrito.map((item, index) => `
      <div class="item-carrito">
        <div class="item-info">
          <h4>${item.nombre}</h4>
          <div class="item-precio">${item.precio.toFixed(2)}</div>
        </div>
        <button class="btn-eliminar" onclick="eliminarDelCarrito(${index})" title="Eliminar producto">
          🗑️
        </button>
      </div>
    `).join('');
  }
  
  const total = carrito.reduce((sum, item) => sum + item.precio, 0);
  totalElement.textContent = total.toFixed(2);
  badge.textContent = carrito.length;
  badge.style.display = carrito.length > 0 ? 'flex' : 'none';
}

function eliminarDelCarrito(index) {
  const itemEliminado = carrito[index];
  carrito.splice(index, 1);
  localStorage.setItem('carrito', JSON.stringify(carrito));
  actualizarCarrito();
  mostrarNotificacion(`${itemEliminado.nombre} eliminado del carrito`);
}

function abrirCarrito() {
  document.getElementById('carrito').style.display = 'block';
  document.getElementById('overlay').classList.add('mostrar');
  setTimeout(() => {
    document.getElementById('carrito').classList.add('mostrar');
  }, 10);
}

function cerrarCarrito() {
  document.getElementById('carrito').classList.remove('mostrar');
  document.getElementById('overlay').classList.remove('mostrar');
  setTimeout(() => {
    document.getElementById('carrito').style.display = 'none';
  }, 300);
}

function finalizarCompra() {
  if (carrito.length === 0) {
    mostrarNotificacion('Tu carrito está vacío', 'warning');
    return;
  }
  
  const total = carrito.reduce((sum, item) => sum + item.precio, 0);
  
  // Registrar venta
  registrarVenta(carrito, total);
  
  // Mostrar mensaje de confirmación
  mostrarNotificacion(`¡Gracias por tu compra! Total: ${total.toFixed(2)}`, 'success');
  
  // Limpiar carrito
  carrito = [];
  localStorage.setItem('carrito', JSON.stringify(carrito));
  actualizarCarrito();
  cerrarCarrito();
}

// =====================================
// FUNCIONES DE VENTAS Y ESTADÍSTICAS
// =====================================

function registrarVenta(items, total) {
  const ahora = new Date();
  const hoy = ahora.toDateString();
  
  // Actualizar estadísticas
  ventasData.ventasDia += total;
  ventasData.ventasSemana += total;
  ventasData.productosVendidos += items.length;
  ventasData.ticketsRealizados += 1;
  ventasData.ultimaVenta = ahora.toISOString();
  
  // Contar productos vendidos
  items.forEach(item => {
    if (ventasData.productosContador[item.nombre]) {
      ventasData.productosContador[item.nombre]++;
    } else {
      ventasData.productosContador[item.nombre] = 1;
    }
    
    // Contar promociones
    if (productos[item.nombre] && productos[item.nombre].categoria === 'promociones') {
      if (ventasData.promocionesContador[item.nombre]) {
        ventasData.promocionesContador[item.nombre]++;
      } else {
        ventasData.promocionesContador[item.nombre] = 1;
      }
    }
  });
  
  // Guardar en localStorage
  localStorage.setItem('ventasData', JSON.stringify(ventasData));
  
  // Actualizar estadísticas en el DOM
  actualizarEstadisticas();
}

function actualizarEstadisticas() {
  document.getElementById('ventasDia').textContent = ventasData.ventasDia.toFixed(2);
  document.getElementById('ventasSemana').textContent = ventasData.ventasSemana.toFixed(2);
  document.getElementById('productosVendidos').textContent = ventasData.productosVendidos;
  
  const ticketPromedio = ventasData.ticketsRealizados > 0 ? 
    (ventasData.ventasDia / ventasData.ticketsRealizados) : 0;
  document.getElementById('ticketPromedio').textContent = ticketPromedio.toFixed(2);
  
  // Producto más vendido
  const topProducto = Object.keys(ventasData.productosContador).reduce((a, b) => 
    ventasData.productosContador[a] > ventasData.productosContador[b] ? a : b, '-');
  document.getElementById('topProducto').textContent = topProducto;
  
  // Promoción más efectiva
  const topPromocion = Object.keys(ventasData.promocionesContador).reduce((a, b) => 
    ventasData.promocionesContador[a] > ventasData.promocionesContador[b] ? a : b, '-');
  document.getElementById('topPromocion').textContent = topPromocion;
}

function verificarVentasSemanales() {
  const ahora = new Date();
  const ultimaVenta = ventasData.ultimaVenta ? new Date(ventasData.ultimaVenta) : null;
  
  if (ultimaVenta) {
    const diferenciaDias = (ahora - ultimaVenta) / (1000 * 60 * 60 * 24);
    if (diferenciaDias > 7) {
      // Resetear ventas semanales si han pasado más de 7 días
      ventasData.ventasSemana = ventasData.ventasDia;
      localStorage.setItem('ventasData', JSON.stringify(ventasData));
    }
  }
}

// =====================================
// FUNCIONES DE ADMINISTRACIÓN
// =====================================

function abrirModal() {
  document.getElementById('adminModal').classList.remove('oculto');
  document.getElementById('adminPass').focus();
}

function cerrarModal() {
  document.getElementById('adminModal').classList.add('oculto');
  document.getElementById('adminPass').value = '';
}

function validarAcceso() {
  const pass = document.getElementById('adminPass').value;
  if (pass === 'NDENTRAB') {
    cerrarModal();
    mostrarPanelAdmin();
  } else {
    mostrarNotificacion('Contraseña incorrecta', 'error');
    document.getElementById('adminPass').value = '';
    document.getElementById('adminPass').focus();
  }
}

function mostrarPanelAdmin() {
  // Ocultar contenido principal
  document.querySelector('.categorias-container').style.display = 'none';
  document.querySelectorAll('.contenido-categoria').forEach(div => {
    div.style.display = 'none';
  });
  
  // Mostrar panel admin
  document.getElementById('adminPanel').classList.remove('oculto');
  actualizarEstadisticas();
}

function cerrarAdmin() {
  // Mostrar contenido principal
  document.querySelector('.categorias-container').style.display = 'block';
  
  // Ocultar panel admin
  document.getElementById('adminPanel').classList.add('oculto');
}

function resetearEstadisticas() {
  if (confirm('¿Estás seguro de que quieres resetear todas las estadísticas?')) {
    ventasData = {
      ventasDia: 0,
      ventasSemana: 0,
      productosVendidos: 0,
      ticketsRealizados: 0,
      productosContador: {},
      promocionesContador: {},
      ultimaVenta: null
    };
    localStorage.setItem('ventasData', JSON.stringify(ventasData));
    actualizarEstadisticas();
    mostrarNotificacion('Estadísticas reseteadas correctamente', 'success');
  }
}

function exportarVentas() {
  const datosExport = {
    fecha: new Date().toISOString(),
    ventasDia: ventasData.ventasDia,
    ventasSemana: ventasData.ventasSemana,
    productosVendidos: ventasData.productosVendidos,
    ticketsRealizados: ventasData.ticketsRealizados,
    productosContador: ventasData.productosContador,
    promocionesContador: ventasData.promocionesContador
  };
  
  const dataStr = JSON.stringify(datosExport, null, 2);
  const dataBlob = new Blob([dataStr], {type: 'application/json'});
  const url = URL.createObjectURL(dataBlob);
  const link = document.createElement('a');
  link.href = url;
  link.download = `ventas_punto_verde_${new Date().toISOString().split('T')[0]}.json`;
  link.click();
  URL.revokeObjectURL(url);
  
  mostrarNotificacion('Ventas exportadas correctamente', 'success');
}

// =====================================
// FUNCIONES DE EDICIÓN DE PRECIOS
// =====================================

function mostrarEditarPrecios() {
  const lista = document.getElementById('listaPreciosEditar');
  lista.innerHTML = Object.keys(productos).map(nombre => `
    <div class="precio-item">
      <label>${nombre}</label>
      <input type="number" value="${productos[nombre].precio}" 
             step="0.01" min="0" data-producto="${nombre}">
    </div>
  `).join('');
  
  document.getElementById('editarPreciosPanel').classList.remove('oculto');
}

function cerrarEditarPrecios() {
  document.getElementById('editarPreciosPanel').classList.add('oculto');
}

function guardarPrecios() {
  const inputs = document.querySelectorAll('#listaPreciosEditar input[data-producto]');
  let cambios = 0;
  
  inputs.forEach(input => {
    const nombre = input.dataset.producto;
    const nuevoPrecio = parseFloat(input.value);
    
    if (nuevoPrecio !== productos[nombre].precio && nuevoPrecio > 0) {
      productos[nombre].precio = nuevoPrecio;
      cambios++;
    }
  });
  
  if (cambios > 0) {
    localStorage.setItem('productos', JSON.stringify(productos));
    actualizarPreciosEnDOM();
    mostrarNotificacion(`${cambios} precio(s) actualizados correctamente`, 'success');
  }
  
  cerrarEditarPrecios();
}

// =====================================
// FUNCIONES DE MODO OSCURO
// =====================================

function toggleModoOscuro() {
  modoOscuro = !modoOscuro;
  localStorage.setItem('modoOscuro', modoOscuro);
  localStorage.setItem('modoOscuroManual', 'true');
  aplicarModoOscuro();
}

function aplicarModoOscuro() {
  const body = document.body;
  const btn = document.getElementById('btnModoOscuro');
  
  if (modoOscuro) {
    body.classList.add('modo-oscuro');
    btn.textContent = '☀️';
  } else {
    body.classList.remove('modo-oscuro');
    btn.textContent = '🌙';
  }
}

// =====================================
// FUNCIONES DE UTILIDAD
// =====================================

function mostrarNotificacion(mensaje, tipo = 'info') {
  const notificacion = document.createElement('div');
  notificacion.className = `notificacion ${tipo}`;
  notificacion.textContent = mensaje;
  
  document.body.appendChild(notificacion);
  
  setTimeout(() => {
    notificacion.style.animation = 'slideOutRight 0.5s ease-out forwards';
    setTimeout(() => {
      document.body.removeChild(notificacion);
    }, 500);
  }, 3000);
}

// =====================================
// EVENT LISTENERS
// =====================================

document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    cerrarModal();
    cerrarEditarPrecios();
    if (document.getElementById('carrito').classList.contains('mostrar')) {
      cerrarCarrito();
    }
  }
});

// Detectar Enter en el campo de contraseña
document.getElementById('adminPass').addEventListener('keypress', function(e) {
  if (e.key === 'Enter') {
    validarAcceso();
  }
});
</script>

<!-- Estilos adicionales para nuevas funcionalidades -->
<style>
  .toggle-dark-mode {
    position: fixed;
    top: 2rem;
    right: 2rem;
    background: var(--verde-principal);
    color: white;
    border: none;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    cursor: pointer;
    font-size: 1.5rem;
    z-index: 1000;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px var(--sombra-suave);
  }

  .toggle-dark-mode:hover {
    transform: scale(1.1);
    box-shadow: 0 8px 25px var(--sombra-fuerte);
  }

  /* Estilos para modo oscuro */
  .modo-oscuro {
    --bg: #1a1a1a;
    --card-bg: #2d2d2d;
    --text: #e0e0e0;
    --accent: #7BAE7F;
    --shadow: rgba(0, 0, 0, 0.3);
    --verde-principal: #8bc34a;
    --verde-oscuro: #689f38;
    --beige: #3a3a3a;
    --blanco: #2d2d2d;
    --texto-principal: #e0e0e0;
    --texto-secundario: #b0b0b0;
    --borde-suave: rgba(139, 195, 74, 0.3);
  }

  .modo-oscuro .imagen-categoria {
    background: linear-gradient(45deg, var(--verde-principal), var(--verde-oscuro));
  }

  .edit-prices-modal {
    max-width: 500px;
    max-height: 70vh;
    overflow-y: auto;
  }

  .precio-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    margin-bottom: 0.5rem;
    background: var(--beige);
    border-radius: 8px;
  }

  .precio-item label {
    font-weight: 600;
    color: var(--texto-principal);
  }

  .precio-item input {
    width: 100px;
    padding: 0.5rem;
    border: 1px solid var(--borde-suave);
    border-radius: 4px;
    text-align: right;
  }

  .admin-actions {
    margin-top: 2rem;
    padding: 1.5rem;
    background: var(--beige);
    border-radius: 10px;
  }

  .admin-actions h3 {
    color: var(--verde-oscuro);
    margin-bottom: 1rem;
    text-align: center;
  }

  .action-buttons {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
  }

  .btn-action {
    background: var(--verde-principal);
    color: white;
    border: none;
    padding: 0.8rem 1.5rem;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9rem;
    transition: all 0.3s ease;
  }

  .btn-action:hover {
    background: var(--verde-oscuro);
    transform: translateY(-2px);
  }

  .notificacion.success {
    background: #4caf50;
  }

  .notificacion.error {
    background: #f44336;
  }

  .notificacion.warning {
    background: #ff9800;
  }

  @keyframes slideOutRight {
    from { transform: translateX(0); opacity: 1; }
    to { transform: translateX(100%); opacity: 0; }
  }

  /* Responsive adicional */
  @media (max-width: 480px) {
    .toggle-dark-mode {
      top: 1rem;
      right: 1rem;
      width: 40px;
      height: 40px;
      font-size: 1.2rem;
    }
    
    .action-buttons {
      flex-direction: column;
    }
    
    .precio-item {
      flex-direction: column;
      text-align: center;
      gap: 0.5rem;
    }
    
    .precio-item
     </script>
</body>
</html>
