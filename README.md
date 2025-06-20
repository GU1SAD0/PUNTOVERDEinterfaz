
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
  <header>
    <h1>Menú Punto Verde</h1>
  </header>

  <!-- CATEGORÍAS, PRODUCTOS, CARRITO, ADMIN, JS OMITIDO PARA BREVEDAD -->
</body>
</html>

