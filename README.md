<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Menú Punto Verde</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    /* ===================================== */
    /* VARIABLES CSS GLOBALES Y MODO OSCURO  */
    /* ===================================== */
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
      --error-color: #ff6b6b; /* Rojo para errores */
      --exito-color: #4CAF50; /* Verde para éxito */
      --advertencia-color: #ffc107; /* Amarillo para advertencias */
    }

    /* Modo oscuro */
    body.dark-mode {
      --verde-principal: #4CAF50;
      --verde-oscuro: #388E3C;
      --beige: #303030;
      --blanco: #424242;
      --texto-principal: #e0e0e0;
      --texto-secundario: #a0a0a0;
      --sombra-suave: rgba(0, 0, 0, 0.3);
      --sombra-fuerte: rgba(0, 0, 0, 0.4);
      --borde-suave: rgba(255, 255, 255, 0.1);
      background: linear-gradient(135deg, #212121 0%, #303030 100%);
      color: var(--texto-principal);
    }

    /* ===================================== */
    /* ESTILOS BASE Y GENERALES              */
    /* ===================================== */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Montserrat', sans-serif;
      background: linear-gradient(135deg, var(--beige) 0%, #f8f6f0 100%);
      color: var(--texto-principal);
      overflow-x: hidden;
      min-height: 100vh;
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    /* ===================================== */
    /* ENCABEZADO                            */
    /* ===================================== */
    header {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      text-align: center;
      padding: 2rem 1rem;
      font-size: 2.2rem;
      font-weight: 700;
      box-shadow: 0 4px 20px var(--sombra-suave);
      position: relative;
      overflow: hidden;
      transition: background 0.3s ease, box-shadow 0.3s ease;
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

    /* ===================================== */
    /* CONTENEDORES PRINCIPALES             */
    /* ===================================== */
    .categorias-container, .contenido-categoria, #adminPanel, #kitchenOrdersPanel {
      padding: 2rem 1.5rem;
      background: var(--blanco);
      margin: 1.5rem auto;
      border-radius: 20px;
      box-shadow: 0 10px 30px var(--sombra-fuerte);
      max-width: 1200px;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }

    .categorias-titulo, .categoria-header h2, .admin-header h2, .kitchen-header h2 {
      text-align: center;
      font-size: 1.8rem;
      color: var(--verde-oscuro);
      margin-bottom: 2rem;
      font-weight: 700;
      transition: color 0.3s ease;
    }

    /* ===================================== */
    /* SCROLL HORIZONTAL (CATEGORÍAS/PRODUCTOS) */
    /* ===================================== */
    .categorias-scroll, .scroll-productos {
      display: flex;
      overflow-x: auto;
      gap: 25px;
      padding: 15px 10px 25px 10px;
      scroll-behavior: smooth;
      -webkit-overflow-scrolling: touch;
    }

    .categorias-scroll::-webkit-scrollbar, .scroll-productos::-webkit-scrollbar, #listaPreciosEditar::-webkit-scrollbar, #listaCategoriasEditar::-webkit-scrollbar, #listaProductosAdmin::-webkit-scrollbar {
      height: 10px;
      width: 10px; /* Para scroll vertical también */
    }

    .categorias-scroll::-webkit-scrollbar-track, .scroll-productos::-webkit-scrollbar-track, #listaPreciosEditar::-webkit-scrollbar-track, #listaCategoriasEditar::-webkit-scrollbar-track, #listaProductosAdmin::-webkit-scrollbar-track {
      background: var(--beige);
      border-radius: 10px;
    }

    .categorias-scroll::-webkit-scrollbar-thumb, .scroll-productos::-webkit-scrollbar-thumb, #listaPreciosEditar::-webkit-scrollbar-thumb, #listaCategoriasEditar::-webkit-scrollbar-thumb, #listaProductosAdmin::-webkit-scrollbar-thumb {
      background: var(--verde-principal);
      border-radius: 10px;
      border: 2px solid var(--beige);
    }

    /* ===================================== */
    /* TARJETAS DE CATEGORÍA                 */
    /* ===================================== */
    .card-categoria {
      flex: 0 0 auto;
      width: 280px;
      background: var(--blanco);
      border-radius: 20px;
      box-shadow: 0 8px 25px var(--sombra-suave);
      cursor: pointer;
      overflow: hidden;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      border: 3px solid transparent;
    }

    .card-categoria:hover {
      transform: translateY(-10px) scale(1.03);
      box-shadow: 0 18px 40px var(--sombra-fuerte);
      border-color: var(--verde-principal);
    }

    .card-categoria.activa {
      border-color: var(--verde-principal);
      box-shadow: 0 0 0 4px var(--verde-oscuro);
    }

    .imagen-categoria {
      height: 180px;
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
      background: rgba(0,0,0,0.25);
    }

    .categoria-icono {
      font-size: 3.5rem;
      position: relative;
      z-index: 1;
      color: white;
      text-shadow: 0 3px 6px rgba(0,0,0,0.4);
    }

    .nombre-categoria {
      padding: 1.2rem;
      text-align: center;
      font-weight: 700;
      font-size: 1.3rem;
      color: var(--verde-oscuro);
      transition: color 0.3s ease;
    }

    /* ===================================== */
    /* SECCIONES DE CONTENIDO (CATEGORÍAS)  */
    /* ===================================== */
    .contenido-categoria {
      animation: fadeIn 0.6s ease-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .categoria-header {
      text-align: center;
      margin-bottom: 2.5rem;
    }

    .categoria-header p {
      color: var(--texto-secundario);
      font-size: 1.2rem;
    }

    /* ===================================== */
    /* TARJETAS DE PRODUCTO                  */
    /* ===================================== */
    .item-card {
      flex: 0 0 auto;
      width: 300px;
      background: var(--blanco);
      padding: 2rem;
      border: 3px solid var(--borde-suave);
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 6px 20px var(--sombra-suave);
      transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
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
      background: linear-gradient(45deg, transparent, rgba(123, 174, 127, 0.08), transparent);
      transform: rotate(45deg);
      transition: all 0.5s ease;
      opacity: 0;
    }

    .item-card:hover::before {
      opacity: 1;
      animation: shine 0.8s ease-out forwards;
    }

    @keyframes shine {
      0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
      100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
    }

    .item-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 15px 35px var(--sombra-fuerte);
      border-color: var(--verde-principal);
    }

    .item-card h3 {
      color: var(--verde-oscuro);
      font-size: 1.5rem;
      margin-bottom: 1rem;
      position: relative;
      z-index: 1;
      transition: color 0.3s ease;
    }

    .item-card .precio {
      font-size: 2.2rem;
      font-weight: 700;
      color: var(--verde-principal);
      margin: 1.2rem 0 0.5rem 0; /* Ajustado para espacio con stock */
      position: relative;
      z-index: 1;
    }
    
    .item-card .stock {
      font-size: 0.95rem;
      color: var(--texto-secundario);
      margin-bottom: 1rem;
    }
    .item-card .stock.agotado {
      color: var(--error-color);
      font-weight: 600;
    }

    .item-card .descripcion {
      color: var(--texto-secundario);
      font-size: 1rem;
      margin-bottom: 1.8rem;
      line-height: 1.5;
      position: relative;
      z-index: 1;
    }

    /* ===================================== */
    /* BOTONES DE ACCIÓN                     */
    /* ===================================== */
    .btn-agregar {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      border: none;
      padding: 14px 28px;
      border-radius: 30px;
      cursor: pointer;
      font-size: 1.1rem;
      font-weight: 600;
      transition: all 0.3s ease;
      position: relative;
      z-index: 1;
      box-shadow: 0 6px 20px var(--sombra-suave);
      text-transform: uppercase;
      letter-spacing: 0.8px;
    }

    .btn-agregar:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 30px var(--sombra-fuerte);
    }

    .btn-agregar:active {
      transform: translateY(0);
    }

    .btn-agregar:disabled {
      background: #ccc;
      cursor: not-allowed;
      opacity: 0.7;
      transform: none;
      box-shadow: none;
    }

    /* ===================================== */
    /* BOTONES FLOTANTES                     */
    /* ===================================== */
    .boton-flotante, .admin-button {
      position: fixed;
      bottom: 30px;
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      padding: 18px 30px;
      border: none;
      border-radius: 50px;
      font-size: 1.2rem;
      font-weight: 600;
      cursor: pointer;
      box-shadow: 0 10px 30px var(--sombra-fuerte);
      z-index: 999;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 10px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .boton-flotante:hover, .admin-button:hover {
      transform: translateY(-5px) scale(1.06);
      box-shadow: 0 18px 40px var(--sombra-fuerte);
    }

    .boton-flotante {
      right: 30px;
    }
    .admin-button {
      left: 30px;
      background: linear-gradient(135deg, #6c757d 0%, #495057 100%);
    }

    .carrito-badge {
      background: var(--blanco);
      color: var(--verde-principal);
      border-radius: 50%;
      min-width: 28px;
      height: 28px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.9rem;
      font-weight: 700;
      margin-left: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }

    .toggle-dark-mode {
      position: fixed;
      top: 20px;
      right: 20px;
      background: var(--blanco);
      color: var(--texto-principal);
      border: 2px solid var(--borde-suave);
      border-radius: 50%;
      width: 50px;
      height: 50px;
      font-size: 1.5rem;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: 0 4px 10px var(--sombra-suave);
      z-index: 1001;
      transition: all 0.3s ease;
    }

    .toggle-dark-mode:hover {
      transform: scale(1.1);
      box-shadow: 0 6px 15px var(--sombra-fuerte);
    }

    /* ===================================== */
    /* CARRITO LATERAL                       */
    /* ===================================== */
    #carrito {
      display: none; /* Initially hidden, controlled by JS adding/removing 'mostrar' */
      position: fixed;
      top: 0;
      right: 0;
      width: 450px;
      height: 100vh;
      background: var(--blanco);
      box-shadow: -15px 0 40px var(--sombra-fuerte);
      z-index: 1000;
      overflow-y: auto;
      transform: translateX(100%);
      transition: transform 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
    }

    #carrito.mostrar {
      display: block; /* Make sure it becomes visible */
      transform: translateX(0);
    }

    .carrito-header {
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      padding: 2.5rem 1.8rem;
      position: sticky;
      top: 0;
      z-index: 10;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .carrito-header h2 {
      margin-bottom: 0;
      font-size: 1.8rem;
    }

    .btn-cerrar-carrito {
      background: rgba(255,255,255,0.2);
      color: white;
      border: none;
      border-radius: 50%;
      width: 45px;
      height: 45px;
      cursor: pointer;
      font-size: 1.4rem;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .btn-cerrar-carrito:hover {
      background: rgba(255,255,255,0.3);
      transform: scale(1.15);
    }

    .carrito-contenido {
      padding: 1.8rem;
    }

    .carrito-vacio {
      text-align: center;
      color: var(--texto-secundario);
      font-size: 1.2rem;
      margin: 4rem 0;
    }

    .carrito-vacio .emoji {
      font-size: 4rem;
      margin-bottom: 1.5rem;
      display: block;
    }

    .item-carrito {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1.2rem;
      margin-bottom: 1.2rem;
      background: var(--beige);
      border-radius: 12px;
      transition: all 0.3s ease;
    }

    .item-carrito:hover {
      transform: translateX(8px);
      box-shadow: 6px 6px 18px var(--sombra-suave);
    }

    .item-info h4 {
      color: var(--verde-oscuro);
      margin-bottom: 0.4rem;
      font-size: 1.1rem;
    }

    .item-precio {
      font-weight: 700;
      color: var(--verde-principal);
      font-size: 1.2rem;
    }
    
    .item-carrito .aderezo {
      font-size: 0.9rem;
      color: var(--texto-secundario);
      margin-top: 0.2rem;
    }

    .btn-eliminar {
      background: var(--error-color);
      color: white;
      border: none;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      cursor: pointer;
      font-size: 1.2rem;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .btn-eliminar:hover {
      background: #e04f4f;
      transform: scale(1.15);
    }

    .carrito-total {
      border-top: 3px solid var(--verde-principal);
      padding-top: 2rem;
      margin-top: 2.5rem;
    }

    .total-precio {
      font-size: 2.2rem;
      font-weight: 700;
      color: var(--verde-principal);
      text-align: center;
      margin-bottom: 1.8rem;
    }

    .btn-finalizar {
      width: 100%;
      background: linear-gradient(135deg, var(--verde-principal) 0%, var(--verde-oscuro) 100%);
      color: white;
      border: none;
      padding: 18px;
      border-radius: 12px;
      font-size: 1.3rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 1.2px;
      box-shadow: 0 6px 20px var(--sombra-suave);
    }

    .btn-finalizar:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 30px var(--sombra-fuerte);
    }

    /* ===================================== */
    /* MODALES GENERALES                     */
    /* ===================================== */
    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2000;
      backdrop-filter: blur(8px);
      animation: fadeInOverlay 0.3s ease-out;
    }

    @keyframes fadeInOverlay {
      from { background-color: rgba(0,0,0,0); backdrop-filter: blur(0px); }
      to { background-color: rgba(0,0,0,0.7); backdrop-filter: blur(8px); }
    }

    .modal-content {
      background: var(--blanco);
      padding: 3rem;
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 25px 80px rgba(0,0,0,0.4);
      max-width: 450px;
      width: 90%;
      animation: modalSlideIn 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
      position: relative;
    }

    @keyframes modalSlideIn {
      from { transform: translateY(-80px) scale(0.9); opacity: 0; }
      to { transform: translateY(0) scale(1); opacity: 1; }
    }

    .modal-content h3 {
      color: var(--verde-oscuro);
      margin-bottom: 2rem;
      font-size: 1.8rem;
      transition: color 0.3s ease;
    }

    .modal-content input, .modal-content select {
      padding: 15px 20px;
      width: 100%;
      margin-bottom: 1.8rem;
      border: 2px solid var(--borde-suave);
      border-radius: 10px;
      font-size: 1.1rem;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
      background: var(--beige);
      color: var(--texto-principal);
    }

    .modal-content input:focus, .modal-content select:focus {
      outline: none;
      border-color: var(--verde-principal);
      box-shadow: 0 0 0 4px var(--sombra-suave);
    }

    .modal-buttons {
      display: flex;
      gap: 1.2rem;
      margin-top: 1.5rem;
    }
    
    .modal-content .dressing-options {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-bottom: 1.8rem;
        text-align: left;
    }

    .modal-content .dressing-options label {
        display: flex;
        align-items: center;
        gap: 8px;
        font-size: 1.1rem;
        color: var(--texto-principal);
        cursor: pointer;
    }

    .modal-content .dressing-options input[type="radio"] {
        width: auto;
        margin-bottom: 0;
        transform: scale(1.2);
        cursor: pointer;
    }
    
    .modal-content .payment-options {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-top: 1rem;
        margin-bottom: 1.8rem;
        text-align: left;
    }

    .modal-content .payment-options label {
        display: flex;
        align-items: center;
        gap: 8px;
        font-size: 1.1rem;
        color: var(--texto-principal);
        cursor: pointer;
    }

    .modal-content .payment-options input[type="radio"] {
        width: auto;
        margin-bottom: 0;
        transform: scale(1.2);
        cursor: pointer;
    }


    .btn-modal {
      flex: 1;
      padding: 15px;
      border: none;
      border-radius: 10px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .btn-entrar {
      background: var(--verde-principal);
      color: white;
      box-shadow: 0 4px 15px var(--sombra-suave);
    }

    .btn-entrar:hover {
      background: var(--verde-oscuro);
      transform: translateY(-2px);
      box-shadow: 0 6px 20px var(--sombra-fuerte);
    }

    .btn-cancelar {
      background: #e9ecef;
      color: var(--texto-secundario);
      border: 1px solid var(--borde-suave);
    }
    
    body.dark-mode .btn-cancelar {
        background: #5a5a5a;
        color: #e0e0e0;
        border: 1px solid rgba(255,255,255,0.2);
    }

    .btn-cancelar:hover {
      background: #dee2e6;
    }
    
    body.dark-mode .btn-cancelar:hover {
        background: #6a6a6a;
    }
    
    /* Botón de cerrar general para modales */
    .btn-cerrar-modal-general {
      position: absolute;
      top: 1rem;
      right: 1rem;
      background: rgba(0, 0, 0, 0.1);
      color: var(--texto-principal);
      border: none;
      border-radius: 50%;
      width: 35px;
      height: 35px;
      cursor: pointer;
      font-size: 1.1rem;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.2s ease;
    }
    .btn-cerrar-modal-general:hover {
      background: rgba(0, 0, 0, 0.2);
      transform: scale(1.1);
    }

    /* ===================================== */
    /* PANEL DE ADMINISTRACIÓN               */
    /* ===================================== */
    #adminPanel {
      padding: 2.5rem 2rem;
      position: relative;
    }

    .admin-header {
      text-align: center;
      margin-bottom: 2.5rem;
      padding-bottom: 1.5rem;
      border-bottom: 3px solid var(--verde-principal);
    }

    .admin-header p {
      color: var(--texto-secundario);
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-top: 2.5rem;
    }

    .stat-card {
      background: var(--blanco);
      padding: 2rem;
      border-radius: 15px;
      border-left: 6px solid var(--verde-principal);
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px var(--sombra-suave);
    }
    
    body.dark-mode .stat-card {
        background: var(--beige);
    }

    .stat-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 25px var(--sombra-fuerte);
    }

    .stat-title {
      color: var(--texto-secundario);
      font-size: 1rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.8px;
      margin-bottom: 0.8rem;
    }

    .stat-value {
      color: var(--verde-principal);
      font-size: 2.5rem;
      font-weight: 700;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    
    .btn-cerrar-admin {
      position: absolute;
      top: 1.5rem;
      right: 1.5rem;
      background: var(--error-color);
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      cursor: pointer;
      font-size: 1.4rem;
      z-index: 1001;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .btn-cerrar-admin:hover {
      background: #ff5252;
      transform: scale(1.15);
    }

    .admin-actions {
      margin-top: 3rem;
      text-align: center;
      padding-top: 2rem;
      border-top: 2px dashed var(--borde-suave);
    }

    .admin-actions h3 {
      color: var(--verde-oscuro);
      font-size: 1.8rem;
      margin-bottom: 1.8rem;
      transition: color 0.3s ease;
    }

    .action-buttons {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1.2rem;
    }

    .btn-action {
      background: linear-gradient(135deg, var(--verde-oscuro) 0%, #4CAF50 100%);
      color: white;
      border: none;
      padding: 14px 28px;
      border-radius: 10px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(0,0,0,0.15);
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .btn-action:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(0,0,0,0.25);
    }
    .btn-action.eliminar {
      background: var(--error-color);
    }
    .btn-action.eliminar:hover {
      background: #e04f4f;
    }
    .btn-action.editar {
      background: linear-gradient(135deg, #1e88e5 0%, #0d47a1 100%); /* Azul */
    }
    .btn-action.editar:hover {
      background: #0d47a1;
    }
    
    /* ===================================== */
    /* UTILIDADES Y ANIMACIONES              */
    /* ===================================== */
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
      color: white;
      padding: 1rem 1.8rem;
      border-radius: 12px;
      box-shadow: 0 8px 25px var(--sombra-fuerte);
      z-index: 3000;
      animation: slideInRight 0.5s ease-out forwards, fadeOut 0.5s ease-in 2.5s forwards;
      opacity: 0;
    }
    .notificacion.info { background: #2196F3; } /* Azul claro */
    .notificacion.success { background: var(--exito-color); } /* Verde */
    .notificacion.error { background: var(--error-color); } /* Rojo */
    .notificacion.warning { background: var(--advertencia-color); } /* Amarillo */


    @keyframes slideInRight {
      from { transform: translateX(120%); opacity: 0; }
      to { transform: translateX(0); opacity: 1; }
    }

    @keyframes fadeOut {
      from { opacity: 1; }
      to { opacity: 0; transform: translateX(120%); }
    }
    
    /* ===================================== */
    /* ESTILOS ESPECÍFICOS DE MODALES ADMIN  */
    /* ===================================== */
    .edit-prices-modal { /* Usado para Modales de productos/categorías también */
      max-width: 700px;
    }

    #listaPreciosEditar, #listaCategoriasEditar, #listaProductosAdmin {
      max-height: 400px;
      overflow-y: auto;
      margin-bottom: 2rem;
      padding-right: 10px;
      text-align: left; /* Para alinear el texto de los ítems */
    }
    
    .precio-item, .categoria-admin-item, .producto-admin-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.8rem 0;
      border-bottom: 1px solid var(--borde-suave);
    }

    .precio-item:last-child, .categoria-admin-item:last-child, .producto-admin-item:last-child {
      border-bottom: none;
    }

    .precio-item span, .categoria-admin-item span, .producto-admin-item span {
      font-size: 1.1rem;
      color: var(--texto-principal);
    }

    .precio-item input {
      width: 100px;
      text-align: right;
      margin-bottom: 0;
      padding: 8px 12px;
      font-size: 1rem;
    }
    
    .categoria-admin-item .item-actions, .producto-admin-item .item-actions {
        display: flex;
        gap: 0.5rem;
    }
    .categoria-admin-item .item-actions button, .producto-admin-item .item-actions button {
        padding: 8px 12px;
        border-radius: 8px;
        font-size: 0.9rem;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.2s ease;
        border: none;
        color: white;
    }
    .categoria-admin-item .item-actions .btn-editar, .producto-admin-item .item-actions .btn-editar {
        background: #1e88e5; /* Azul para editar */
    }
    .categoria-admin-item .item-actions .btn-eliminar-rojo, .producto-admin-item .item-actions .btn-eliminar-rojo {
        background: var(--error-color); /* Rojo para eliminar */
    }
    .categoria-admin-item .item-actions button:hover, .producto-admin-item .item-actions button:hover {
        opacity: 0.8;
        transform: translateY(-1px);
    }

    /* Estilos para errores de validación en los inputs */
    input.error, select.error {
      border-color: var(--error-color) !important;
      box-shadow: 0 0 0 3px rgba(255, 107, 107, 0.3) !important;
    }

    /* ===================================== */
    /* PANTALLA DE PEDIDOS EN COCINA         */
    /* ===================================== */
    #kitchenOrdersPanel {
        padding: 2.5rem 2rem;
        position: relative;
        text-align: center;
    }

    .kitchen-header {
        text-align: center;
        margin-bottom: 2.5rem;
        padding-bottom: 1.5rem;
        border-bottom: 3px solid var(--verde-principal);
    }

    .kitchen-header p {
        color: var(--texto-secundario);
    }

    .orders-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
        gap: 2rem;
        margin-top: 2.5rem;
    }

    .order-card {
        background: var(--blanco);
        padding: 1.8rem;
        border-radius: 15px;
        box-shadow: 0 6px 20px var(--sombra-suave);
        border: 3px solid var(--verde-principal);
        text-align: left;
        display: flex;
        flex-direction: column;
        justify-content: space-between; /* Empuja el botón al final */
    }
    body.dark-mode .order-card {
        background: var(--beige);
    }

    .order-card h3 {
        color: var(--verde-oscuro);
        font-size: 1.6rem;
        margin-bottom: 0.8rem;
        border-bottom: 2px dashed var(--borde-suave);
        padding-bottom: 0.5rem;
    }

    .order-card .items-list {
        list-style: none;
        padding: 0;
        margin-bottom: 1.5rem;
    }

    .order-card .items-list li {
        font-size: 1.1rem;
        color: var(--texto-principal);
        margin-bottom: 0.5rem;
    }

    .order-card .items-list li .aderezo {
        font-size: 0.9rem;
        color: var(--texto-secundario);
        margin-left: 10px;
    }

    .order-card .order-total {
        font-size: 1.8rem;
        font-weight: 700;
        color: var(--verde-principal);
        text-align: right;
        margin-top: 1rem;
    }

    .order-card .order-time {
        font-size: 0.9rem;
        color: var(--texto-secundario);
        text-align: right;
        margin-top: 0.5rem;
    }
    
    .order-card .order-payment {
        font-size: 0.95rem;
        color: var(--texto-principal);
        text-align: right;
        margin-top: 0.2rem;
        font-weight: 600;
    }


    .btn-marcar-listo {
        background: linear-gradient(135deg, var(--exito-color) 0%, #388E3C 100%);
        color: white;
        border: none;
        padding: 12px 20px;
        border-radius: 10px;
        font-size: 1.1rem;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 4px 15px rgba(0,0,0,0.15);
        margin-top: 1.5rem;
        width: 100%;
        text-transform: uppercase;
        letter-spacing: 0.8px;
    }

    .btn-marcar-listo:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 20px rgba(0,0,0,0.25);
    }

    .btn-cerrar-kitchen {
      position: absolute;
      top: 1.5rem;
      right: 1.5rem;
      background: var(--error-color);
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      cursor: pointer;
      font-size: 1.4rem;
      z-index: 1001;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .btn-cerrar-kitchen:hover {
      background: #ff5252;
      transform: scale(1.15);
    }

    @media (max-width: 768px) {
        #kitchenOrdersPanel {
            padding: 1.5rem;
        }
        .orders-grid {
            grid-template-columns: 1fr;
            gap: 1.5rem;
        }
        .order-card h3 {
            font-size: 1.4rem;
        }
        .order-card .items-list li {
            font-size: 1rem;
        }
        .order-card .order-total {
            font-size: 1.5rem;
        }
        .btn-marcar-listo {
            padding: 10px 15px;
            font-size: 1rem;
        }
        .btn-cerrar-kitchen {
            width: 40px;
            height: 40px;
            font-size: 1.2rem;
            top: 1rem;
            right: 1rem;
        }
    }

    /* Nuevo: Modal de pago */
    #paymentModal .modal-content {
        max-width: 480px;
    }

    /* Nuevo: Modal de Recibo/Ticket */
    #receiptModal .modal-content {
        max-width: 550px;
        text-align: left;
    }
    #receiptModal .modal-content h3 {
        text-align: center;
        margin-bottom: 1.5rem;
    }
    #receiptModal .receipt-details {
        font-size: 1.1rem;
        line-height: 1.6;
        margin-bottom: 1.5rem;
        border-bottom: 1px dashed var(--borde-suave);
        padding-bottom: 1.5rem;
    }
    #receiptModal .receipt-details strong {
        color: var(--verde-oscuro);
    }
    #receiptModal .receipt-items {
        list-style: none;
        padding: 0;
        margin-bottom: 1.5rem;
    }
    #receiptModal .receipt-item {
        display: flex;
        justify-content: space-between;
        padding: 0.5rem 0;
        border-bottom: 1px dotted var(--borde-suave);
    }
    #receiptModal .receipt-item:last-child {
        border-bottom: none;
    }
    #receiptModal .receipt-item-name {
        flex-grow: 1;
        color: var(--texto-principal);
    }
    #receiptModal .receipt-item-price {
        font-weight: 600;
        color: var(--verde-principal);
    }
    #receiptModal .receipt-total {
        text-align: right;
        font-size: 1.5rem;
        font-weight: 700;
        color: var(--verde-principal);
        margin-top: 1rem;
    }
    /* Eliminado el botón de imprimir, por lo tanto, no es necesario este estilo */
    /*
    #receiptModal .btn-print {
        width: 100%;
        background: linear-gradient(135deg, #007bff 0%, #0056b3 100%);
        color: white;
        border: none;
        padding: 15px;
        border-radius: 10px;
        font-size: 1.1rem;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 4px 15px rgba(0,0,0,0.15);
        margin-top: 2rem;
    }
    #receiptModal .btn-print:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 20px rgba(0,0,0,0.25);
    }
    */

  </style>
</head>
<body>
  <header>
    <div class="logo-texto">🌱 Punto Verde</div>
  </header>

  <div class="categorias-container">
    <h2 class="categorias-titulo">Selecciona una categoría</h2>
    <div class="categorias-scroll" id="categoriasScroll">
      <!-- Las categorías se cargarán dinámicamente aquí -->
    </div>
  </div>

  <!-- Contenedores de productos por categoría -->
  <!-- Cada div 'contenido-categoria' se llenará dinámicamente con productos -->
  <div id="promos" class="contenido-categoria main-view">
    <div class="categoria-header">
      <h2>🎉 Promociones Especiales</h2>
      <p>Combos perfectos para ahorrar y disfrutar</p>
    </div>
    <div class="scroll-productos"></div>
  </div>

  <div id="bebidas" class="contenido-categoria main-view">
    <div class="categoria-header">
      <h2>🥤 Bebidas Naturales</h2>
      <p>Aguas frescas preparadas diariamente con frutas naturales</p>
    </div>
    <div class="scroll-productos"></div>
  </div>

  <div id="alimentos" class="contenido-categoria main-view">
    <div class="categoria-header">
      <h2>🥪 Alimentos Saludables</h2>
      <p>Opciones nutritivas preparadas con ingredientes frescos del día</p>
    </div>
    <div class="scroll-productos"></div>
  </div>
  
  <!-- Overlay para el carrito y modales -->
  <div class="overlay" id="overlay" onclick="cerrarTodasLasVentanas()"></div>

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
        <button class="btn-finalizar" onclick="iniciarProcesoDePago()">
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

  <button class="admin-button" onclick="mostrarVista('admin')">⚙️ Acceso Personal</button>

  <!-- Toggle modo oscuro -->
  <button class="toggle-dark-mode" onclick="toggleModoOscuro()" id="btnModoOscuro">
    🌙
  </button>

  <!-- Modal de acceso administrativo -->
  <div id="adminModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('adminModal')">✕</button>
      <h3>🔐 Acceso Personal Autorizado</h3>
      <input type="password" id="adminPass" placeholder="Ingresa la contraseña" autocomplete="off"/>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="validarAcceso()">Entrar</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('adminModal')">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- Panel de administración -->
  <div id="adminPanel" class="oculto">
    <button class="btn-cerrar-admin" onclick="mostrarVista('usuario')">✕</button>
    <div class="admin-header">
      <h2>📊 Panel de Administración</h2>
      <p>Gestiona tu negocio y revisa las estadísticas e inventario</p>
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
        <div class="stat-title">Producto Más Vendido (Semanal)</div>
        <div class="stat-value"><span id="topProducto">-</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Promoción Más Efectiva (Semanal)</div>
        <div class="stat-value"><span id="topPromocion">-</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Total Unidades en Inventario</div>
        <div class="stat-value"><span id="totalUnidadesInventario">0</span></div>
      </div>
      <div class="stat-card">
        <div class="stat-title">Valor Total del Inventario</div>
        <div class="stat-value">$<span id="valorInventario">0.00</span></div>
      </div>
    </div>

    <div class="admin-actions">
      <h3>🛠️ Acciones Administrativas</h3>
      <div class="action-buttons">
        <button class="btn-action" onclick="resetearEstadisticas()">
          🔄 Resetear Estadísticas Diarias
        </button>
        <button class="btn-action" onclick="exportarVentas()">
          📄 Exportar Ventas
        </button>
        <button class="btn-action editar" onclick="mostrarGestionProductos()">
          📦 Gestión de Productos
        </button>
        <button class="btn-action editar" onclick="mostrarGestionCategorias()">
          🗂️ Gestión de Categorías
        </button>
        <button class="btn-action" onclick="mostrarVista('cocina')">
          👩‍🍳 Pedidos en Cocina
        </button>
      </div>
    </div>
  </div>

  <!-- Modal para Gestión de Productos (Añadir/Editar/Eliminar) -->
  <div id="gestionProductosModal" class="modal oculto">
    <div class="modal-content edit-prices-modal">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('gestionProductosModal')">✕</button>
      <h3>📦 Gestión de Productos</h3>
      <div class="action-buttons" style="margin-bottom: 20px;">
        <button class="btn-action" onclick="abrirAnadirProductoModal()">➕ Añadir Nuevo Producto</button>
      </div>
      <h4>Productos Existentes:</h4>
      <div id="listaProductosAdmin"></div>
      <div class="modal-buttons" style="margin-top: 20px;">
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('gestionProductosModal')">Cerrar</button>
      </div>
    </div>
  </div>

  <!-- Modal para Añadir Producto -->
  <div id="anadirProductoModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('anadirProductoModal')">✕</button>
      <h3>➕ Añadir Nuevo Producto</h3>
      <input type="text" id="addNombreProducto" placeholder="Nombre del producto" />
      <input type="number" id="addPrecioProducto" placeholder="Precio del producto" step="0.01" min="0" />
      <input type="number" id="addStockProducto" placeholder="Stock inicial" step="1" min="0" />
      <input type="text" id="addDescripcionProducto" placeholder="Descripción (opcional)" />
      <select id="addCategoriaProducto">
        <option value="">Selecciona categoría</option>
        <!-- Opciones se llenan dinámicamente -->
      </select>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="anadirProducto()">Añadir Producto</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('anadirProductoModal')">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- Modal para Editar Producto -->
  <div id="editarProductoModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('editarProductoModal')">✕</button>
      <h3>✏️ Editar Producto</h3>
      <input type="text" id="editNombreProducto" placeholder="Nombre del producto" disabled />
      <input type="number" id="editPrecioProducto" placeholder="Precio del producto" step="0.01" min="0" />
      <input type="number" id="editStockProducto" placeholder="Stock" step="1" min="0" />
      <input type="text" id="editDescripcionProducto" placeholder="Descripción (opcional)" />
      <select id="editCategoriaProducto">
        <option value="">Selecciona categoría</option>
        <!-- Opciones se llenan dinámicamente -->
      </select>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="guardarEdicionProducto()">Guardar Cambios</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('editarProductoModal')">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- Modal para Gestión de Categorías (Añadir/Eliminar) -->
  <div id="gestionCategoriasModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('gestionCategoriasModal')">✕</button>
      <h3>🗂️ Gestión de Categorías</h3>
      <div class="action-buttons" style="margin-bottom: 20px;">
        <input type="text" id="addNombreCategoria" placeholder="Nombre de nueva categoría" style="margin-bottom: 0;" />
        <button class="btn-action" onclick="anadirCategoria()">➕ Añadir Categoría</button>
      </div>
      <h4>Categorías Existentes:</h4>
      <div id="listaCategoriasEditar"></div>
      <div class="modal-buttons" style="margin-top: 20px;">
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('gestionCategoriasModal')">Cerrar</button>
      </div>
    </div>
  </div>

  <!-- Nuevo Modal para Selección de Aderezo -->
  <div id="aderezoModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('aderezoModal')">✕</button>
      <h3>Aderezo para <span id="aderezoProductoNombre"></span></h3>
      <div class="dressing-options">
        <label><input type="radio" name="aderezo" value="Chipotle" checked> Chipotle</label>
        <label><input type="radio" name="aderezo" value="Mostaza Dulce"> Mostaza Dulce</label>
        <label><input type="radio" name="aderezo" value="Ranch"> Ranch</label>
        <label><input type="radio" name="aderezo" value="Sin Aderezo"> Sin Aderezo</label>
      </div>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="finalizarSeleccionAderezo()">Aceptar</button>
        <button class="btn-modal btn-cancelar" onclick="cancelarSeleccionAderezo()">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- NUEVO: Modal para Detalles de Pago -->
  <div id="paymentModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('paymentModal')">✕</button>
      <h3>Detalles del Pago y Cliente</h3>
      <input type="text" id="clienteNombreInput" placeholder="Nombre del Cliente (Ej: Juan)" />
      <p style="margin-top: 1rem; color: var(--texto-principal);">Método de Pago:</p>
      <div class="payment-options">
        <label><input type="radio" name="paymentMethod" value="Efectivo" checked> Efectivo</label>
        <label><input type="radio" name="paymentMethod" value="Tarjeta"> Tarjeta</label>
      </div>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="confirmarPago()">Confirmar Pago</button>
        <button class="btn-modal btn-cancelar" onclick="cerrarModal('paymentModal')">Cancelar</button>
      </div>
    </div>
  </div>

  <!-- NUEVO: Modal de Recibo/Ticket -->
  <div id="receiptModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cerrarModal('receiptModal')">✕</button>
      <h3>✅ Pedido Confirmado - ¡Listo!</h3>
      <p style="text-align: center; color: var(--texto-secundario); margin-bottom: 2rem;">Gracias por tu compra.</p>
      <div class="receipt-details">
        <p><strong>Cliente:</strong> <span id="receiptClienteNombre"></span></p>
        <p><strong>Fecha:</strong> <span id="receiptFecha"></span></p>
        <p><strong>Hora:</strong> <span id="receiptHora"></span></p>
        <p><strong>Método de Pago:</strong> <span id="receiptMetodoPago"></span></p>
      </div>
      <h4>Detalle del Pedido:</h4>
      <ul class="receipt-items" id="receiptItemsList">
        <!-- Items del pedido se insertarán aquí -->
      </ul>
      <div class="receipt-total">Total: $<span id="receiptTotal">0.00</span></div>
      <!-- BOTÓN DE IMPRIMIR ELIMINADO -->
    </div>
  </div>

  <!-- NUEVO: Modal para confirmar pedido listo en cocina -->
  <div id="confirmarPedidoListoModal" class="modal oculto">
    <div class="modal-content">
      <button class="btn-cerrar-modal-general" onclick="cancelarPedidoListoAccion()">✕</button>
      <h3>¿Confirmar Pedido Listo?</h3>
      <p>Estás a punto de marcar como listo el pedido para:</p>
      <p style="font-weight: 700; font-size: 1.2rem; color: var(--verde-oscuro); margin-top: 0.5rem;" id="confirmarPedidoCliente"></p>
      <p style="margin-top: 1rem; margin-bottom: 2rem;">¿Estás seguro de que este pedido está listo para ser entregado?</p>
      <div class="modal-buttons">
        <button class="btn-modal btn-entrar" onclick="confirmarPedidoListoAccion()">Sí, Listo</button>
        <button class="btn-modal btn-cancelar" onclick="cancelarPedidoListoAccion()">Cancelar</button>
      </div>
    </div>
  </div>


  <!-- NUEVO: Panel de Pedidos en Cocina -->
  <div id="kitchenOrdersPanel" class="oculto">
    <button class="btn-cerrar-kitchen" onclick="mostrarVista('admin')">✕</button>
    <div class="kitchen-header">
      <h2>🍳 Pedidos en Cocina</h2>
      <p>Aquí puedes ver los pedidos pendientes y marcarlos como listos.</p>
    </div>
    <div class="orders-grid" id="pedidosPendientesGrid">
      <!-- Los pedidos se cargarán dinámicamente aquí -->
      <div class="carrito-vacio" id="noPedidosMessage" style="display: none;">
        <span class="emoji">🎉</span>
        <p>¡No hay pedidos pendientes!</p>
        <p>A la espera de nuevas órdenes...</p>
      </div>
    </div>
  </div>

<!-- Agrega estos scripts de Firebase al inicio del body o en el head -->
<!-- Asegúrate de que estén ANTES de tu script principal -->
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>

<script>
// =====================================
// CONFIGURACIÓN DE FIREBASE E INICIALIZACIÓN
// =====================================

// TU CONFIGURACIÓN DE FIREBASE PROPORCIONADA
const firebaseConfig = {
  apiKey: "AIzaSyBMR1kXCO2xlFkPFaBby-GTUuN7umkSaJQ",
  authDomain: "mipos-e5430.firebaseapp.com",
  projectId: "mipos-e5430",
  storageBucket: "mipos-e5430.firebasestorage.app",
  messagingSenderId: "1092023571594",
  appId: "1:1092023571594:web:318f7af08e0844d1294973"
};

// Inicializa Firebase (usando el objeto global 'firebase' ahora)
const app = firebase.initializeApp(firebaseConfig);
const db = app.firestore(); // Accede a Firestore a través de la instancia de la app

// =====================================
// VARIABLES GLOBALES (AHORA CARGADAS DESDE/HACIA FIREBASE)
// =====================================

// Datos de ventas por día (YYYY-MM-DD) para estadísticas semanales/mensuales
// Se cargarán desde Firebase
let ventasDiarias = {};

// Carrito de compras actual (local al cliente)
let carrito = [];

// Array para almacenar pedidos pendientes para la cocina (sincronizados con Firebase)
let pedidosPendientes = [];

// Definición de categorías con sus propiedades (icono, nombre, imagen de fondo)
// Se cargarán desde Firebase
let categorias = {};

// Productos con precios y stock editables, y si requieren aderezo.
// Se cargarán desde Firebase
let productos = {};

// Default data (used if Firebase is empty)
const DEFAULT_CATEGORIES = {
  'promos': { nombre: 'Promociones', icono: '🎉', imageUrl: 'https://placehold.co/280x180/7BAE7F/5a8a5e?text=Promociones' },
  'bebidas': { nombre: 'Bebidas', icono: '🥤', imageUrl: 'https://placehold.co/280x180/7BAE7F/5a8a5e?text=Bebidas' },
  'alimentos': { nombre: 'Alimentos', icono: '🥪', imageUrl: 'https://placehold.co/280x180/7BAE7F/5a8a5e?text=Alimentos' }
};

const DEFAULT_PRODUCTS = {
  'Combo Wrap + Agua': { precio: 65, stock: 10, categoria: 'promos', descripcion: 'Delicioso wrap de pollo con vegetales frescos + agua natural de tu sabor favorito', requiresDressing: true },
  'Combo Baguette + Bebida': { precio: 55, stock: 8, categoria: 'promos', descripcion: 'Baguette artesanal recién horneada + agua de fruta natural', requiresDressing: true },
  'Combo Estudiante': { precio: 45, stock: 12, categoria: 'promos', descripcion: 'Cuernito de jamón + agua natural + fruta de temporada', requiresDressing: false },
  'Agua de Maracuyá': { precio: 20, stock: 50, categoria: 'bebidas', descripcion: 'Refrescante agua de maracuyá natural, perfecta para cualquier momento', requiresDressing: false },
  'Agua de Ciruela': { precio: 20, stock: 45, categoria: 'bebidas', descripcion: 'Agua fresca de ciruela con el toque perfecto de dulzura natural', requiresDressing: false },
  'Agua de Guanábana': { precio: 22, stock: 30, categoria: 'bebidas', descripcion: 'Exótica agua de guanábana con su sabor único y refrescante', requiresDressing: false },
  'Agua Natural': { precio: 15, stock: 100, categoria: 'bebidas', descripcion: 'Agua purificada embotellada, ideal para acompañar tus alimentos', requiresDressing: false },
  'Baguette de Pollo': { precio: 40, stock: 20, categoria: 'alimentos', descripcion: 'Pan baguette artesanal con pechuga de pollo, lechuga, tomate y aderezo especial', requiresDressing: true },
  'Baguette Vegetariana': { precio: 38, stock: 18, categoria: 'alimentos', descripcion: 'Pan baguette con aguacate, espinacas, tomate, pepino y aderezo vegano', requiresDressing: true },
  'Wrap de Pollo': { precio: 42, stock: 25, categoria: 'alimentos', descripcion: 'Tortilla integral con pollo, vegetales frescos y salsa especial', requiresDressing: true },
  'Cuernito de Jamón': { precio: 35, stock: 30, categoria: 'alimentos', descripcion: 'Delicioso cuernito con jamón de pavo, queso y vegetales', requiresDressing: true },
  'Ensalada Verde': { precio: 32, stock: 15, categoria: 'alimentos', descripcion: 'Mix de lechugas, espinacas, tomate cherry, pepino y aderezo', requiresDressing: false }
};

const ADMIN_PASSWORD = "NDENTRAB";

// Configuración de modo oscuro (true/false) - Sigue en localStorage
let modoOscuro;
try {
    modoOscuro = localStorage.getItem('modoOscuro') === 'true' || 
                 (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches);
    if (typeof modoOscuro !== 'boolean') { modoOscuro = false; }
} catch (e) {
    console.error("Error al leer 'modoOscuro' de localStorage:", e);
    modoOscuro = false;
}

// Variables para el flujo de aderezos y productos
let productoSeleccionadoParaAderezo = null;
let currentOrderIdToConfirm = null; // Para confirmar pedidos listos en cocina

let unsubscribeKitchenListener = null; // Para almacenar la función para desuscribirse del listener de cocina

// =====================================
// HELPERS PARA LOCALSTORAGE (AHORA SOLO PARA SETTINGS PEQUEÑOS)
// =====================================

// Helper para guardar configuraciones pequeñas en localStorage
function setSetting(key, value) {
    try {
        localStorage.setItem(key, JSON.stringify(value));
    } catch (e) {
        console.error(`Error al guardar '${key}' en localStorage:`, e);
        mostrarNotificacion(`Error al guardar configuración (${key}). Intenta de nuevo.`, 'error');
    }
}

// Helper para obtener configuraciones pequeñas de localStorage
function getSetting(key, defaultValue) {
    try {
        const item = localStorage.getItem(key);
        return item ? JSON.parse(item) : defaultValue;
    } catch (e) {
        console.error(`Error al parsear '${key}' de localStorage:`, e);
        return defaultValue;
    }
}

// =====================================
// FUNCIONES DE FIREBASE (Carga y Guardado de Datos Principales)
// =====================================

async function cargarDatosIniciales() {
  try {
    // --- Cargar Productos ---
    const productosRef = db.collection('appData').doc('productos');
    const productosSnap = await productosRef.get();
    if (productosSnap.exists) {
      productos = productosSnap.data(); // Carga el objeto completo
      console.log("Productos cargados desde Firebase.");
    } else {
      console.log("No se encontraron productos en Firebase. Inicializando con valores por defecto.");
      productos = DEFAULT_PRODUCTS;
      await guardarProductosEnFirebase(); // Sube los productos por defecto a Firebase
    }

    // --- Cargar Categorías ---
    const categoriasRef = db.collection('appData').doc('categorias');
    const categoriasSnap = await categoriasRef.get();
    if (categoriasSnap.exists) {
      categorias = categoriasSnap.data(); // Carga el objeto completo
      console.log("Categorías cargadas desde Firebase.");
    } else {
      console.log("No se encontraron categorías en Firebase. Inicializando con valores por defecto.");
      categorias = DEFAULT_CATEGORIES;
      await guardarCategoriasEnFirebase(); // Sube las categorías por defecto a Firebase
    }
    
    // --- Cargar Ventas Diarias ---
    // Como las ventas diarias son dinámicas por fecha, no las cargamos todas de golpe al inicio.
    // Se cargarán cuando se necesiten para las estadísticas.
    // Solo cargamos los datos recientes para el cálculo de estadísticas.
    console.log("Ventas Diarias serán cargadas al actualizar estadísticas.");

  } catch (e) {
    console.error("Error al cargar datos iniciales de Firebase:", e);
    mostrarNotificacion("Error al cargar datos del servidor. Usando datos locales.", 'error');
    // Fallback si Firebase falla (aunque ahora no tenemos localStorage de fallback para estos datos)
    // En un escenario real, aquí se podría cargar una copia de respaldo local si existiera.
  }
}

async function guardarProductosEnFirebase() {
  try {
    await db.collection('appData').doc('productos').set(productos);
    console.log("Productos guardados en Firebase.");
  } catch (e) {
    console.error("Error al guardar productos en Firebase:", e);
    mostrarNotificacion("Error al guardar productos. Verifica tu conexión.", 'error');
  }
}

async function guardarCategoriasEnFirebase() {
  try {
    await db.collection('appData').doc('categorias').set(categorias);
    console.log("Categorías guardadas en Firebase.");
  } catch (e) {
    console.error("Error al guardar categorías en Firebase:", e);
    mostrarNotificacion("Error al guardar categorías. Verifica tu conexión.", 'error');
  }
}

async function guardarVentasDiariasEnFirebase(fecha, data) {
  try {
    await db.collection('ventasDiarias').doc(fecha).set(data, { merge: true }); // Usamos merge para actualizar si ya existe
    console.log(`Ventas diarias para ${fecha} guardadas en Firebase.`);
  } catch (e) {
    console.error("Error al guardar ventas diarias en Firebase:", e);
    mostrarNotificacion("Error al guardar ventas. Verifica tu conexión.", 'error');
  }
}

async function obtenerVentasDiariasDeFirebase(fecha) {
    try {
        const docRef = db.collection('ventasDiarias').doc(fecha);
        const docSnap = await docRef.get();
        if (docSnap.exists) {
            return docSnap.data();
        } else {
            return { totalVentas: 0, numeroTickets: 0, productosVendidos: {}, promocionesVendidas: {} };
        }
    } catch (e) {
        console.error(`Error al obtener ventas diarias de Firebase para ${fecha}:`, e);
        mostrarNotificacion(`Error al obtener ventas para ${fecha}.`, 'error');
        return { totalVentas: 0, numeroTickets: 0, productosVendidos: {}, promocionesVendidas: {} };
    }
}


// =====================================
// FUNCIONES DE INICIALIZACIÓN
// =====================================

// Se ejecuta cuando el DOM está completamente cargado
document.addEventListener('DOMContentLoaded', async function() {
  await inicializarApp();
});

// Función principal de inicialización de la aplicación
async function inicializarApp() {
  await cargarDatosIniciales(); // Primero carga los datos de Firebase
  
  cargarCategoriasEnDOM(); // Carga las categorías en el carrusel principal
  cargarProductosEnDOM(); // Carga los productos dentro de sus respectivas categorías
  actualizarCarrito(); // Actualiza la vista del carrito
  actualizarEstadisticas(); // Actualiza las estadísticas del panel de administración
  aplicarModoOscuro(); // Aplica el modo oscuro si está activado
  
  // Escucha cambios en la preferencia de color del sistema operativo para el modo oscuro automático
  if (window.matchMedia) {
    window.mediaQuery = window.matchMedia('(prefers-color-scheme: dark)'); // Guarda la media query
    window.mediaQuery.addEventListener('change', function(e) {
      try {
        if (getSetting('modoOscuroManual') === null) { // Si el usuario no ha puesto modo manual
          modoOscuro = e.matches;
          aplicarModoOscuro();
        }
      } catch (error) {
        console.error("Error al acceder 'modoOscuroManual' en localStorage:", error);
      }
    });
  }

  // Persistencia de la vista: Muestra la última sección activa o la de usuario por defecto
  const ultimaVista = getSetting('ultimaVista', 'usuario'); // 'usuario' es la vista por defecto
  mostrarVista(ultimaVista);
  
  // Si la última vista era la de cocina, iniciamos el listener
  if (ultimaVista === 'cocina') {
    escucharPedidosDeCocina();
  }
}

// =====================================
// CONTROL DE VISTAS (User, Admin, Kitchen)
// =====================================

// Controla qué sección de la aplicación está visible
function mostrarVista(vista) {
    // Oculta todas las secciones principales
    document.querySelector('header').classList.add('oculto');
    document.querySelector('.categorias-container').classList.add('oculto');
    document.querySelectorAll('.contenido-categoria').forEach(div => div.classList.add('oculto'));
    document.getElementById('btnCarrito').classList.add('oculto');
    document.querySelector('.admin-button').classList.add('oculto');
    document.getElementById('btnModoOscuro').classList.add('oculto');
    document.getElementById('adminPanel').classList.add('oculto');
    document.getElementById('kitchenOrdersPanel').classList.add('oculto');

    // Cierra cualquier modal abierto
    cerrarTodasLasVentanas();

    // Desuscribe el listener de cocina si estaba activo
    if (unsubscribeKitchenListener) {
      unsubscribeKitchenListener();
      unsubscribeKitchenListener = null;
      console.log("Listener de cocina desuscrito.");
    }

    // Muestra la sección solicitada
    switch (vista) {
        case 'usuario':
            document.querySelector('header').classList.remove('oculto');
            document.querySelector('.categorias-container').classList.remove('oculto');
            document.getElementById('btnCarrito').classList.remove('oculto');
            document.querySelector('.admin-button').classList.remove('oculto');
            document.getElementById('btnModoOscuro').classList.remove('oculto');
            // Muestra la categoría activa o la primera por defecto
            const categoriaActiva = document.querySelector('.card-categoria.activa');
            if (categoriaActiva) {
                mostrarCategoria(categoriaActiva.dataset.categoria);
            } else {
                // Aquí usamos `Object.keys(categorias)[0]` que se cargará desde Firebase.
                // Si aún no hay categorías en Firebase, puede ser 'undefined'.
                mostrarCategoria(Object.keys(categorias).length > 0 ? Object.keys(categorias)[0] : 'promos'); 
            }
            break;
        case 'admin':
            document.getElementById('adminPanel').classList.remove('oculto');
            document.querySelector('.admin-button').classList.remove('oculto'); // Mantener visible para salir
            document.getElementById('btnModoOscuro').classList.remove('oculto'); // Mantener visible
            actualizarEstadisticas();
            break;
        case 'cocina':
            document.getElementById('kitchenOrdersPanel').classList.remove('oculto');
            document.querySelector('.admin-button').classList.remove('oculto'); // Mantener visible para salir
            document.getElementById('btnModoOscuro').classList.remove('oculto'); // Mantener visible
            escucharPedidosDeCocina(); // Inicia el listener en tiempo real
            break;
        default:
            // Por si acaso, vuelve a la vista de usuario
            mostrarVista('usuario');
            break;
    }
    // Guarda la vista actual en localStorage
    setSetting('ultimaVista', vista);
}


// =====================================
// FUNCIONES DE CATEGORÍAS Y PRODUCTOS
// (CLIENTE Y CARGA DINÁMICA)
// =====================================

// Carga las tarjetas de categoría en el carrusel superior
function cargarCategoriasEnDOM() {
  const categoriasScroll = document.getElementById('categoriasScroll');
  categoriasScroll.innerHTML = ''; // Limpiar categorías existentes
  
  for (const id in categorias) {
    const categoria = categorias[id];
    const card = document.createElement('div');
    card.className = 'card-categoria';
    card.setAttribute('onclick', `mostrarCategoria('${id}')`);
    card.setAttribute('data-categoria', id);
    card.innerHTML = `
      <div class="imagen-categoria" style="background-image: url('${categoria.imageUrl || 'https://placehold.co/280x180/7BAE7F/5a8a5e?text=' + categoria.nombre}');">
        <div class="categoria-icono">${categoria.icono}</div>
      </div>
      <div class="nombre-categoria">${categoria.nombre}</div>
    `;
    categoriasScroll.appendChild(card);
  }
}

// Carga las tarjetas de productos dentro de cada contenedor de categoría
function cargarProductosEnDOM() {
  // Iterar sobre todos los contenedores de productos (uno por cada categoría)
  document.querySelectorAll('.contenido-categoria .scroll-productos').forEach(container => {
    container.innerHTML = ''; // Limpiar productos existentes en este contenedor
    // Obtener el ID de la categoría a la que pertenece este contenedor
    const categoriaId = container.closest('.contenido-categoria').id;
    
    // Filtrar los productos que pertenecen a esta categoría
    const productosDeCategoria = Object.keys(productos).filter(nombreProducto => 
      productos[nombreProducto].categoria === categoriaId
    );

    // Si no hay productos en esta categoría, mostrar un mensaje
    if (productosDeCategoria.length === 0) {
      container.innerHTML = `
        <div style="text-align: center; width: 100%; color: var(--texto-secundario); padding: 20px;">
          <p>No hay productos en esta categoría aún.</p>
        </div>
      `;
      return;
    }

    // Crear y añadir cada tarjeta de producto
    productosDeCategoria.forEach(nombreProducto => {
      const producto = productos[nombreProducto];
      const itemCard = document.createElement('div');
      itemCard.className = 'item-card';
      // Deshabilitar botón si no hay stock
      const isDisabled = producto.stock <= 0 ? 'disabled' : '';
      const stockText = producto.stock <= 0 ? '<span class="stock agotado">AGOTADO</span>' : `<span class="stock">Stock: ${producto.stock}</span>`;

      itemCard.innerHTML = `
        <h3>${nombreProducto}</h3>
        <p class="descripcion">${producto.descripcion}</p>
        <p class="precio">$${producto.precio.toFixed(2)}</p>
        ${stockText}
        <button class="btn-agregar" onclick="manejarAgregarAlCarrito('${nombreProducto}')" ${isDisabled}>
          Agregar al carrito
        </button>
      `;
      container.appendChild(itemCard);
    });
  });
}

// Muestra el contenido de una categoría específica y actualiza la tarjeta activa
function mostrarCategoria(id) {
  // Oculta todas las secciones de contenido de categorías
  document.querySelectorAll('.contenido-categoria.main-view').forEach(div => {
    div.classList.add('oculto');
    const scrollProductosDiv = div.querySelector('.scroll-productos');
    if (scrollProductosDiv) {
        scrollProductosDiv.style.display = '';
    }
  });
  
  // Remueve la clase 'activa' de todas las tarjetas de categoría
  document.querySelectorAll('.card-categoria').forEach(card => {
    card.classList.remove('activa');
  });
  
  // Muestra la sección de contenido de la categoría seleccionada
  const categoriaSeleccionada = document.getElementById(id);
  if (categoriaSeleccionada) {
    categoriaSeleccionada.classList.remove('oculto');
    const scrollProductosDiv = categoriaSeleccionada.querySelector('.scroll-productos');
    if (scrollProductosDiv) {
        scrollProductosDiv.style.display = 'flex';
    }
  } else {
    mostrarNotificacion(`Categoría "${id}" no encontrada. Mostrando la primera categoría disponible.`, 'warning');
    const primeraCategoriaId = Object.keys(categorias)[0];
    if (primeraCategoriaId) {
        mostrarCategoria(primeraCategoriaId);
    } else {
        console.warn("No hay categorías disponibles para mostrar.");
        document.querySelector('.categorias-container').classList.remove('oculto');
        document.querySelector('.categorias-scroll').innerHTML = '<p style="text-align: center; width: 100%; color: var(--texto-secundario); padding: 20px;">No hay categorías disponibles.</p>';
    }
    return;
  }
  
  // Agrega la clase 'activa' a la tarjeta de categoría seleccionada
  const cardCategoriaActiva = document.querySelector(`[data-categoria="${id}"]`);
  if (cardCategoriaActiva) {
    cardCategoriaActiva.classList.add('activa');
  }
}

// =====================================
// FUNCIONES DEL CARRITO DE COMPRAS
// =====================================

// Maneja el flujo para agregar un producto al carrito (incluyendo selección de aderezo)
async function manejarAgregarAlCarrito(nombreProducto) {
  // Verifica si el producto existe y tiene stock disponible
  // Re-cargamos productos para asegurar el stock más reciente
  await cargarDatosIniciales(); 
  
  if (!productos[nombreProducto] || productos[nombreProducto].stock <= 0) {
    mostrarNotificacion(`"${nombreProducto}" está agotado.`, 'error');
    return;
  }

  // Si el producto requiere aderezo, abre el modal de aderezo
  if (productos[nombreProducto].requiresDressing) {
    productoSeleccionadoParaAderezo = nombreProducto; // Guarda el producto actual
    document.getElementById('aderezoProductoNombre').textContent = nombreProducto;
    // Seleccionar el primer radio button por defecto
    document.querySelector('input[name="aderezo"][value="Chipotle"]').checked = true;
    abrirModal('aderezoModal');
  } else {
    // Si no requiere aderezo, agrégalo directamente al carrito
    await agregarProductoAlCarritoConDetalles(nombreProducto, null); // null para aderezo
  }
}

// Agrega un producto al carrito con su aderezo (o sin él) y actualiza el inventario
async function agregarProductoAlCarritoConDetalles(nombreProducto, aderezo) {
  console.log("DEBUG: agregarProductoAlCarritoConDetalles - Agregando:", nombreProducto, "con aderezo:", aderezo);
  
  // Decrementa el stock del producto y guarda en Firebase
  if (productos[nombreProducto]) {
    productos[nombreProducto].stock--;
    await guardarProductosEnFirebase(); // Guarda el inventario actualizado en Firebase
  } else {
    console.error(`Producto "${nombreProducto}" no encontrado en la lista de productos.`);
    mostrarNotificacion(`Error: Producto "${nombreProducto}" no encontrado.`, 'error');
    return;
  }

  // Añade el producto al carrito
  carrito.push({ 
    nombre: nombreProducto, 
    precio: productos[nombreProducto].precio, 
    aderezo: aderezo, 
    id: Date.now() + Math.random() // ID único para cada instancia en el carrito
  });
  
  actualizarCarrito(); // Actualiza la UI
  cargarProductosEnDOM(); // Para reflejar el cambio de stock en la UI
  mostrarNotificacion(`"${nombreProducto}${aderezo ? ' con ' + aderezo : ''}" agregado al carrito`, 'success');
  
  // Animar el botón del carrito
  const btnCarrito = document.getElementById('btnCarrito');
  btnCarrito.classList.add('pulse');
  setTimeout(() => btnCarrito.classList.remove('pulse'), 1000);
}

// Finaliza la selección de aderezo y agrega el producto al carrito
async function finalizarSeleccionAderezo() {
    const aderezoSeleccionado = document.querySelector('input[name="aderezo"]:checked').value;
    if (productoSeleccionadoParaAderezo) {
        await agregarProductoAlCarritoConDetalles(productoSeleccionadoParaAderezo, aderezoSeleccionado);
    }
    productoSeleccionadoParaAderezo = null; // Limpiar la variable
    cerrarModal('aderezoModal');
}

// Cancela la selección de aderezo (no agrega el producto al carrito)
function cancelarSeleccionAderezo() {
    productoSeleccionadoParaAderezo = null; // Limpiar la variable
    cerrarModal('aderezoModal');
    mostrarNotificacion('Selección de aderezo cancelada.', 'info');
}

// Actualiza la visualización del carrito y el total
function actualizarCarrito() {
  console.log("DEBUG: actualizarCarrito - Estado actual del carrito:", carrito);
  const carritoItemsDiv = document.getElementById('carrito-items');
  const totalElement = document.getElementById('total');
  const badge = document.getElementById('carritoBadge');
  
  let total = 0;
  carritoItemsDiv.innerHTML = ''; // Limpiar antes de renderizar

  if (carrito.length === 0) {
    carritoItemsDiv.innerHTML = `
      <div class="carrito-vacio">
        <span class="emoji">🛒</span>
        <p>Tu carrito está vacío</p>
        <p>¡Agrega algunos productos deliciosos!</p>
      </div>
    `;
  } else {
    carrito.forEach(item => {
      total += item.precio;
      const aderezoHtml = item.aderezo ? `<div class="aderezo">Aderezo: ${item.aderezo}</div>` : '';
      const itemDiv = document.createElement('div');
      itemDiv.className = 'item-carrito';
      itemDiv.innerHTML = `
        <div class="item-info">
          <h4>${item.nombre}</h4>
          ${aderezoHtml}
          <div class="item-precio">$${item.precio.toFixed(2)}</div>
        </div>
        <button class="btn-eliminar" onclick="eliminarDelCarrito(${item.id})">✕</button>
      `;
      carritoItemsDiv.appendChild(itemDiv);
    });
  }
  
  totalElement.textContent = total.toFixed(2);
  badge.textContent = carrito.length;
}

// Elimina un producto del carrito y actualiza el inventario
async function eliminarDelCarrito(itemId) {
  const index = carrito.findIndex(item => item.id === itemId);
  if (index !== -1) {
    const productoEliminado = carrito[index];
    carrito.splice(index, 1); // Elimina el producto del carrito
    
    // Incrementa el stock del producto de vuelta en el inventario
    if (productos[productoEliminado.nombre]) {
      productos[productoEliminado.nombre].stock++;
      await guardarProductosEnFirebase(); // Guarda el inventario actualizado en Firebase
      cargarProductosEnDOM(); // Refleja el cambio de stock
    }

    actualizarCarrito();
    mostrarNotificacion(`"${productoEliminado.nombre}" eliminado del carrito`, 'info');
  }
}

// Abre el carrito lateral
function abrirCarrito() {
  console.log("DEBUG: abrirCarrito() - Llamada a la función.");
  // No necesitamos cerrar todas las ventanas aquí, ya que el carrito es lateral.
  // Pero sí aseguramos que no haya un overlay de modal encima.
  const carritoElement = document.getElementById('carrito');
  const overlayElement = document.getElementById('overlay');

  if (carritoElement && overlayElement) {
    carritoElement.classList.add('mostrar');
    // Si no hay otro modal, mostrar el overlay
    if (document.querySelectorAll('.modal:not(.oculto)').length === 0) {
      overlayElement.classList.add('mostrar');
    }
    console.log("DEBUG: abrirCarrito() - Clases 'mostrar' añadidas al carrito y overlay si aplica.");
  } else {
    console.error("ERROR: abrirCarrito() - Elementos #carrito o #overlay no encontrados.");
  }
}

// Cierra el carrito lateral
function cerrarCarrito() {
  const carritoElement = document.getElementById('carrito');
  const overlayElement = document.getElementById('overlay');

  if (carritoElement && overlayElement) {
    carritoElement.classList.remove('mostrar');
    // Solo ocultar el overlay si NO hay ningún otro modal visible
    const anyModalVisible = document.querySelectorAll('.modal:not(.oculto)').length > 0;
    if (!anyModalVisible) {
      overlayElement.classList.remove('mostrar');
    }
  }
}

// Inicia el proceso de pago (nombre del cliente y método de pago)
function iniciarProcesoDePago() {
    console.log("DEBUG: iniciarProcesoDePago() - Llamada a la función.");
    if (carrito.length === 0) {
        mostrarNotificacion('El carrito está vacío. Agrega productos para finalizar la compra.', 'error');
        console.log("DEBUG: iniciarProcesoDePago() - Carrito vacío, no se procede.");
        return;
    }
    document.getElementById('clienteNombreInput').value = ''; // Limpiar campo
    document.querySelector('input[name="paymentMethod"][value="Efectivo"]').checked = true; // Seleccionar Efectivo por defecto
    abrirModal('paymentModal');
    console.log("DEBUG: iniciarProcesoDePago() - Abriendo modal de pago.");
}

// Confirma el pago con el nombre del cliente y el método de pago
async function confirmarPago() {
    console.log("DEBUG: confirmarPago() - Llamada a la función.");
    const nombreCliente = document.getElementById('clienteNombreInput').value.trim();
    const metodoPago = document.querySelector('input[name="paymentMethod"]:checked').value;
    console.log("DEBUG: confirmarPago() - Cliente:", nombreCliente, "Método de Pago:", metodoPago);

    if (!nombreCliente) {
        mostrarNotificacion('Por favor, ingresa el nombre del cliente.', 'error');
        console.log("DEBUG: confirmarPago() - Nombre del cliente vacío, mostrando error.");
        return;
    }
    
    await finalizarCompra(nombreCliente, metodoPago); // Pasa el nombre y método de pago
    cerrarModal('paymentModal');
    console.log("DEBUG: confirmarPago() - Modal de pago cerrado.");
}


// Procesa la compra, actualiza las estadísticas y guarda el pedido para la cocina
async function finalizarCompra(nombreCliente, metodoPago) {
  console.log("DEBUG: finalizarCompra() - Iniciando proceso de compra para cliente:", nombreCliente, "con método de pago:", metodoPago);
  const totalElement = document.getElementById('total');
  const totalCompra = parseFloat(totalElement.textContent);
  console.log("DEBUG: finalizarCompra() - Total de la compra:", totalCompra);

  const fechaActual = new Date().toISOString().slice(0, 10); // Formato ISO AAAA-MM-DD
  const horaActual = new Date().toLocaleTimeString('es-MX', { hour: '2-digit', minute: '2-digit' });

  // Cargar datos de ventas diarias para la fecha actual (si existen)
  let hoyData = await obtenerVentasDiariasDeFirebase(fechaActual);

  // Acumular ventas del día
  hoyData.totalVentas = (hoyData.totalVentas || 0) + totalCompra;
  hoyData.numeroTickets = (hoyData.numeroTickets || 0) + 1;

  carrito.forEach(item => {
    // Contar productos vendidos
    hoyData.productosVendidos[item.nombre] = 
      (hoyData.productosVendidos[item.nombre] || 0) + 1;
    
    // Contar promociones (si aplica)
    if (productos[item.nombre] && productos[item.nombre].categoria === 'promos') {
      hoyData.promocionesVendidas[item.nombre] =
        (hoyData.promocionesVendidas[item.nombre] || 0) + 1;
    }
  });

  await guardarVentasDiariasEnFirebase(fechaActual, hoyData);
  console.log("DEBUG: Ventas diarias guardadas en Firebase.");
  
  // Almacenar el pedido para la pantalla de cocina en Firebase
  const nuevoPedido = {
    id: Date.now().toString(), // Usamos un string como ID para el documento de Firebase
    cliente: nombreCliente,
    items: JSON.parse(JSON.stringify(carrito)), // Copia profunda del carrito
    total: totalCompra,
    hora: horaActual,
    fecha: fechaActual,
    metodoPago: metodoPago 
  };
  console.log("DEBUG: finalizarCompra() - Nuevo pedido creado:", nuevoPedido);

  try {
    const pedidosCollection = db.collection('pedidosPendientes');
    await pedidosCollection.doc(nuevoPedido.id).set(nuevoPedido);
    console.log("DEBUG: Pedido añadido y guardado en pedidosPendientes en Firebase.");
  } catch (error) {
    console.error("Error al guardar pedido en Firebase:", error);
    mostrarNotificacion("Error al enviar pedido a cocina. Intenta de nuevo.", 'error');
  }

  // Mostrar el ticket/recibo al cliente
  mostrarTicket(nuevoPedido);

  // Mensaje al comprador de que el pedido está en preparación
  mostrarNotificacion(`¡Tu pedido ya está en preparación! Gracias por tu compra, ${nombreCliente}.`, 'success');

  // Limpiar carrito y actualizar UI
  carrito = [];
  actualizarCarrito();
  actualizarEstadisticas();
  cerrarCarrito();
  console.log("DEBUG: finalizarCompra() - Proceso de compra finalizado.");
}

// Muestra el modal del ticket/recibo
function mostrarTicket(pedido) {
    document.getElementById('receiptClienteNombre').textContent = pedido.cliente;
    document.getElementById('receiptFecha').textContent = pedido.fecha;
    document.getElementById('receiptHora').textContent = pedido.hora;
    document.getElementById('receiptMetodoPago').textContent = pedido.metodoPago;
    document.getElementById('receiptTotal').textContent = pedido.total.toFixed(2);

    const receiptItemsList = document.getElementById('receiptItemsList');
    receiptItemsList.innerHTML = '';
    pedido.items.forEach(item => {
        const itemLi = document.createElement('li');
        itemLi.className = 'receipt-item';
        const aderezoText = item.aderezo && item.aderezo !== 'Sin Aderezo' ? ` (${item.aderezo})` : '';
        itemLi.innerHTML = `
            <span class="receipt-item-name">${item.nombre}${aderezoText}</span>
            <span class="receipt-item-price">$${item.precio.toFixed(2)}</span>
        `;
        receiptItemsList.appendChild(itemLi);
    });

    abrirModal('receiptModal');
}


// =====================================
// FUNCIONES DE ADMINISTRACIÓN (PANEL Y MODALES)
// =====================================

// Abre un modal específico (usado para login, añadir, editar, etc.)
function abrirModal(modalId) {
  // Asegura que el overlay se muestre solo si un modal está abierto
  document.querySelectorAll('.modal').forEach(m => m.classList.add('oculto')); // Oculta todos los modales primero
  document.getElementById(modalId).classList.remove('oculto');
  document.getElementById('overlay').classList.add('mostrar');

  if (modalId === 'adminModal') {
    document.getElementById('adminPass').value = '';
    document.getElementById('adminPass').focus();
    document.addEventListener('keydown', handleAdminModalKeyPress);
  } else {
    document.removeEventListener('keydown', handleAdminModalKeyPress);
  }
}

// Cierra un modal específico
function cerrarModal(modalId) {
  document.getElementById(modalId).classList.add('oculto');
  const anyModalVisible = document.querySelectorAll('.modal:not(.oculto)').length > 0;
  // Solo ocultar el overlay si NO hay ningún otro modal visible Y el carrito NO está abierto
  const isCarritoOpen = document.getElementById('carrito').classList.contains('mostrar');
  if (!anyModalVisible && !isCarritoOpen) {
    document.getElementById('overlay').classList.remove('mostrar');
  }
  document.removeEventListener('keydown', handleAdminModalKeyPress);
}

// Maneja las teclas en el modal de admin (Enter para validar, Escape para cerrar)
function handleAdminModalKeyPress(event) {
  if (event.key === 'Escape') {
    cerrarModal('adminModal');
  } else if (event.key === 'Enter') {
    validarAcceso();
  }
}

// Oculta todas las ventanas (carrito, modales, y ahora la pantalla de cocina)
function cerrarTodasLasVentanas() {
  const carritoElement = document.getElementById('carrito');
  if (carritoElement) { carritoElement.classList.remove('mostrar'); }

  document.getElementById('adminModal').classList.add('oculto');
  document.getElementById('gestionProductosModal').classList.add('oculto');
  document.getElementById('anadirProductoModal').classList.add('oculto');
  document.getElementById('editarProductoModal').classList.add('oculto');
  document.getElementById('gestionCategoriasModal').classList.add('oculto');
  document.getElementById('aderezoModal').classList.add('oculto');
  document.getElementById('paymentModal').classList.add('oculto');
  document.getElementById('receiptModal').classList.add('oculto');
  document.getElementById('confirmarPedidoListoModal').classList.add('oculto');

  // Asegurar que el overlay se oculte si nada más está visible
  document.getElementById('overlay').classList.remove('mostrar');
  document.removeEventListener('keydown', handleAdminModalKeyPress);
}

// Valida la contraseña para acceder al panel de administración
function validarAcceso() {
  const password = document.getElementById('adminPass').value;
  if (password === ADMIN_PASSWORD) {
    cerrarModal('adminModal');
    mostrarVista('admin'); // Usamos la nueva función para mostrar vistas
  } else {
    mostrarNotificacion('Contraseña incorrecta. Intenta de nuevo.', 'error');
  }
}

// Actualiza todas las estadísticas en el panel de administración
async function actualizarEstadisticas() {
  const fechaActual = new Date().toISOString().slice(0, 10);
  
  // Para obtener estadísticas semanales, necesitamos cargar datos de los últimos 7 días
  let ventasSemanaTotal = 0;
  let ventasSemanaProductosContador = {};
  let ventasSemanaPromocionesContador = {};

  // Obtener la fecha de hace 7 días
  const sieteDiasAtras = new Date();
  sieteDiasAtras.setDate(sieteDiasAtras.getDate() - 6); // Incluye el día actual + 6 días atrás

  // Iterar y sumar las ventas de los últimos 7 días
  for (let i = 0; i < 7; i++) {
    const d = new Date(sieteDiasAtras);
    d.setDate(sieteDiasAtras.getDate() + i);
    const fecha = d.toISOString().slice(0, 10);
    const diaData = await obtenerVentasDiariasDeFirebase(fecha);

    if (diaData) {
      ventasSemanaTotal += (diaData.totalVentas || 0);
      for (const prod in (diaData.productosVendidos || {})) {
        ventasSemanaProductosContador[prod] = (ventasSemanaProductosContador[prod] || 0) + diaData.productosVendidos[prod];
      }
      for (const promo in (diaData.promocionesVendidas || {})) {
        ventasSemanaPromocionesContador[promo] = (ventasSemanaPromocionesContador[promo] || 0) + diaData.promocionesVendidas[promo];
      }
    }
  }

  // Datos de hoy
  const hoyData = await obtenerVentasDiariasDeFirebase(fechaActual);

  document.getElementById('ventasDia').textContent = (hoyData.totalVentas || 0).toFixed(2);
  const totalProductosVendidosHoy = Object.values(hoyData.productosVendidos || {}).reduce((acc, val) => acc + val, 0);
  document.getElementById('productosVendidos').textContent = totalProductosVendidosHoy;
  document.getElementById('ticketPromedio').textContent = hoyData.numeroTickets > 0 ? (hoyData.totalVentas / hoyData.numeroTickets).toFixed(2) : '0.00';
  
  document.getElementById('ventasSemana').textContent = ventasSemanaTotal.toFixed(2);

  let topProducto = { nombre: '-', cantidad: 0 };
  for (const prod in ventasSemanaProductosContador) {
    if (ventasSemanaProductosContador[prod] > topProducto.cantidad) {
      topProducto.nombre = prod;
      topProducto.cantidad = ventasSemanaProductosContador[prod];
    }
  }
  document.getElementById('topProducto').textContent = topProducto.nombre;

  let topPromocion = { nombre: '-', cantidad: 0 };
  for (const promo in ventasSemanaPromocionesContador) {
    if (ventasSemanaPromocionesContador[promo] > topPromocion.cantidad) {
      topPromocion.nombre = promo;
      topPromocion.cantidad = ventasSemanaPromocionesContador[promo];
    }
  }
  document.getElementById('topPromocion').textContent = topPromocion.nombre;

  // Estadísticas de Inventario (ya cargadas al inicio desde Firebase)
  let totalUnidades = 0;
  let valorInventarioTotal = 0;
  for (const prodName in productos) {
    totalUnidades += productos[prodName].stock;
    valorInventarioTotal += productos[prodName].stock * productos[prodName].precio;
  }
  document.getElementById('totalUnidadesInventario').textContent = totalUnidades;
  document.getElementById('valorInventario').textContent = valorInventarioTotal.toFixed(2);
}

// Resetea las estadísticas de ventas del día actual
async function resetearEstadisticas() {
  if (confirm('¿Estás seguro de que quieres resetear las estadísticas del DÍA? Esta acción es irreversible.')) {
    const fechaActual = new Date().toISOString().slice(0, 10);
    const dataVacia = {
      totalVentas: 0,
      numeroTickets: 0,
      productosVendidos: {},
      promocionesVendidas: {}
    };
    await guardarVentasDiariasEnFirebase(fechaActual, dataVacia);
    actualizarEstadisticas();
    mostrarNotificacion('Estadísticas diarias reseteadas.', 'success');
  }
}

// Exporta los datos de ventas como un archivo JSON
async function exportarVentas() {
  try {
    const allVentasDocs = await db.collection('ventasDiarias').get();
    let allVentasData = {};
    allVentasDocs.forEach(doc => {
      allVentasData[doc.id] = doc.data();
    });

    const data = JSON.stringify(allVentasData, null, 2);
    const blob = new Blob([data], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `ventas_punto_verde_${new Date().toISOString().slice(0, 10)}.json`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    mostrarNotificacion('Datos de ventas exportados.', 'success');
  } catch (e) {
    console.error("Error al exportar ventas:", e);
    mostrarNotificacion("Error al exportar ventas. Verifica tu conexión.", 'error');
  }
}

// =====================================
// FUNCIONES DE GESTIÓN DE PRODUCTOS (ADMIN)
// =====================================

// Muestra el modal de gestión de productos
function mostrarGestionProductos() {
  abrirModal('gestionProductosModal');
  actualizarListaProductosAdmin();
}

// Actualiza la lista de productos en el modal de gestión
function actualizarListaProductosAdmin() {
  const lista = document.getElementById('listaProductosAdmin');
  lista.innerHTML = ''; // Limpiar lista actual

  if (Object.keys(productos).length === 0) {
    lista.innerHTML = '<p style="text-align: center; color: var(--texto-secundario);">No hay productos registrados.</p>';
    return;
  }

  for (const nombreProd in productos) {
    const prod = productos[nombreProd];
    const itemDiv = document.createElement('div');
    itemDiv.className = 'producto-admin-item';
    itemDiv.innerHTML = `
      <span>${nombreProd} ($${prod.precio.toFixed(2)}) - Stock: ${prod.stock}</span>
      <div class="item-actions">
        <button class="btn-editar" onclick="editarProducto('${nombreProd}')">Editar</button>
        <button class="btn-eliminar-rojo" onclick="eliminarProducto('${nombreProd}')">Eliminar</button>
      </div>
    `;
    lista.appendChild(itemDiv);
  }
}

// Abre el modal para añadir un nuevo producto
function abrirAnadirProductoModal() {
  document.getElementById('addNombreProducto').value = '';
  document.getElementById('addPrecioProducto').value = '';
  document.getElementById('addStockProducto').value = '';
  document.getElementById('addDescripcionProducto').value = '';
  document.getElementById('addCategoriaProducto').innerHTML = '<option value="">Selecciona categoría</option>';
  // Llenar el select con las categorías existentes
  for (const id in categorias) {
    const option = document.createElement('option');
    option.value = id;
    option.textContent = categorias[id].nombre;
    document.getElementById('addCategoriaProducto').appendChild(option);
  }
  // Limpiar posibles errores de validación previos
  document.getElementById('addNombreProducto').classList.remove('error');
  document.getElementById('addPrecioProducto').classList.remove('error');
  document.getElementById('addStockProducto').classList.remove('error');
  document.getElementById('addCategoriaProducto').classList.remove('error');

  abrirModal('anadirProductoModal');
}

// Añade un nuevo producto al inventario
async function anadirProducto() {
  const nombre = document.getElementById('addNombreProducto').value.trim();
  const precio = parseFloat(document.getElementById('addPrecioProducto').value);
  const stock = parseInt(document.getElementById('addStockProducto').value);
  const descripcion = document.getElementById('addDescripcionProducto').value.trim();
  const categoria = document.getElementById('addCategoriaProducto').value;

  // Validación de inputs
  let isValid = true;
  document.getElementById('addNombreProducto').classList.remove('error');
  document.getElementById('addPrecioProducto').classList.remove('error');
  document.getElementById('addStockProducto').classList.remove('error');
  document.getElementById('addCategoriaProducto').classList.remove('error');

  if (!nombre) {
    document.getElementById('addNombreProducto').classList.add('error');
    isValid = false;
  }
  if (isNaN(precio) || precio < 0) {
    document.getElementById('addPrecioProducto').classList.add('error');
    isValid = false;
  }
  if (isNaN(stock) || stock < 0) {
    document.getElementById('addStockProducto').classList.add('error');
    isValid = false;
  }
  if (!categoria) {
    document.getElementById('addCategoriaProducto').classList.add('error');
    isValid = false;
  }

  if (!isValid) {
    mostrarNotificacion('Por favor, completa todos los campos válidos.', 'error');
    return;
  }

  if (productos[nombre]) {
    mostrarNotificacion(`El producto "${nombre}" ya existe.`, 'error');
    return;
  }
  
  // Determinar si el producto requiere aderezo basado en el nombre (ajustar según tus productos)
  const requiresDressing = ['Baguette', 'Wrap', 'Cuernito'].some(type => nombre.includes(type));

  productos[nombre] = { precio: precio, stock: stock, categoria: categoria, descripcion: descripcion, requiresDressing: requiresDressing };
  await guardarProductosEnFirebase(); // Guarda en Firebase
  
  cargarProductosEnDOM(); // Recargar la vista del cliente
  actualizarListaProductosAdmin(); // Actualizar lista en admin
  actualizarEstadisticas(); // Actualizar stats de inventario
  mostrarNotificacion(`Producto "${nombre}" añadido con éxito.`, 'success');
  cerrarModal('anadirProductoModal');
}

// Abre el modal para editar un producto existente
function editarProducto(nombreProducto) {
  window.productoEditando = nombreProducto; // Guarda el nombre del producto que se está editando
  const prod = productos[nombreProducto];

  if (!prod) {
    mostrarNotificacion('Producto no encontrado para editar.', 'error');
    return;
  }

  // Llenar los campos del formulario de edición
  document.getElementById('editNombreProducto').value = nombreProducto; // El nombre no se edita
  document.getElementById('editPrecioProducto').value = prod.precio.toFixed(2);
  document.getElementById('editStockProducto').value = prod.stock;
  document.getElementById('editDescripcionProducto').value = prod.descripcion;

  const selectCategoria = document.getElementById('editCategoriaProducto');
  selectCategoria.innerHTML = '<option value="">Selecciona categoría</option>';
  for (const id in categorias) {
    const option = document.createElement('option');
    option.value = id;
    option.textContent = categorias[id].nombre;
    selectCategoria.appendChild(option);
    if (id === prod.categoria) {
      option.selected = true; // Seleccionar la categoría actual del producto
    }
  }

  // Limpiar posibles errores de validación previos
  document.getElementById('editPrecioProducto').classList.remove('error');
  document.getElementById('editStockProducto').classList.remove('error');
  document.getElementById('editDescripcionProducto').classList.remove('error');
  document.getElementById('editCategoriaProducto').classList.remove('error');

  abrirModal('editarProductoModal');
}

// Guarda los cambios de un producto editado
async function guardarEdicionProducto() {
  if (!window.productoEditando) {
    mostrarNotificacion('No hay producto seleccionado para guardar.', 'error');
    return;
  }

  const nombreOriginal = window.productoEditando;
  const precio = parseFloat(document.getElementById('editPrecioProducto').value);
  const stock = parseInt(document.getElementById('editStockProducto').value);
  const descripcion = document.getElementById('editDescripcionProducto').value.trim();
  const categoria = document.getElementById('editCategoriaProducto').value;

  // Validación de inputs
  let isValid = true;
  document.getElementById('editPrecioProducto').classList.remove('error');
  document.getElementById('editStockProducto').classList.remove('error');
  document.getElementById('editDescripcionProducto').classList.remove('error');
  document.getElementById('editCategoriaProducto').classList.remove('error');

  if (isNaN(precio) || precio < 0) {
    document.getElementById('editPrecioProducto').classList.add('error');
    isValid = false;
  }
  if (isNaN(stock) || stock < 0) {
    document.getElementById('editStockProducto').classList.add('error');
    isValid = false;
  }
  if (!categoria) {
    document.getElementById('editCategoriaProducto').classList.add('error');
    isValid = false;
  }

  if (!isValid) {
    mostrarNotificacion('Por favor, corrige los campos inválidos.', 'error');
    return;
  }

  // Actualiza las propiedades del producto
  productos[nombreOriginal].precio = precio;
  productos[nombreOriginal].stock = stock;
  productos[nombreOriginal].descripcion = descripcion;
  productos[nombreOriginal].categoria = categoria;

  await guardarProductosEnFirebase(); // Guarda en Firebase
  
  cargarProductosEnDOM();
  actualizarListaProductosAdmin();
  actualizarEstadisticas();
  mostrarNotificacion(`Producto "${nombreOriginal}" actualizado.`, 'success');
  cerrarModal('editarProductoModal');
  window.productoEditando = null; // Resetear la variable
}

// Elimina un producto del inventario
async function eliminarProducto(nombreProducto) {
  if (confirm(`¿Estás seguro de que quieres eliminar el producto "${nombreProducto}"? Esta acción es irreversible.`)) {
    if (productos[nombreProducto]) {
      delete productos[nombreProducto];
      await guardarProductosEnFirebase(); // Guarda en Firebase
      
      cargarProductosEnDOM();
      actualizarListaProductosAdmin();
      actualizarEstadisticas();
      mostrarNotificacion(`Producto "${nombreProducto}" eliminado.`, 'success');
    } else {
      mostrarNotificacion(`Producto "${nombreProducto}" no encontrado.`, 'error');
    }
  }
}

// =====================================
// FUNCIONES DE GESTIÓN DE CATEGORÍAS (ADMIN)
// =====================================

// Muestra el modal de gestión de categorías
function mostrarGestionCategorias() {
  abrirModal('gestionCategoriasModal');
  actualizarListaCategoriasAdmin();
}

// Actualiza la lista de categorías en el modal de gestión
function actualizarListaCategoriasAdmin() {
  const lista = document.getElementById('listaCategoriasEditar');
  lista.innerHTML = ''; // Limpiar lista actual
  document.getElementById('addNombreCategoria').value = ''; // Limpiar input de añadir

  if (Object.keys(categorias).length === 0) {
    lista.innerHTML = '<p style="text-align: center; color: var(--texto-secundario);">No hay categorías registradas.</p>';
    return;
  }

  for (const id in categorias) {
    const cat = categorias[id];
    const itemDiv = document.createElement('div');
    itemDiv.className = 'categoria-admin-item';
    itemDiv.innerHTML = `
      <span>${cat.nombre} (ID: ${id})</span>
      <div class="item-actions">
        <button class="btn-eliminar-rojo" onclick="eliminarCategoria('${id}')">Eliminar</button>
      </div>
    `;
    lista.appendChild(itemDiv);
  }
}

// Añade una nueva categoría
async function anadirCategoria() {
  const nombreCategoria = document.getElementById('addNombreCategoria').value.trim();
  const idCategoria = nombreCategoria.toLowerCase().replace(/[^a-z0-9]/g, '').replace(/\s/g, ''); 
  const iconoDefault = '✨';
  const imageUrlDefault = `https://placehold.co/280x180/7BAE7F/5a8a5e?text=${encodeURIComponent(nombreCategoria)}`;

  if (!nombreCategoria) {
    mostrarNotificacion('El nombre de la categoría no puede estar vacío.', 'error');
    return;
  }
  if (categorias[idCategoria]) {
    mostrarNotificacion(`La categoría "${nombreCategoria}" ya existe.`, 'error');
    return;
  }

  categorias[idCategoria] = { nombre: nombreCategoria, icono: iconoDefault, imageUrl: imageUrlDefault };
  await guardarCategoriasEnFirebase(); // Guarda en Firebase
  
  cargarCategoriasEnDOM();
  actualizarListaCategoriasAdmin();
  mostrarNotificacion(`Categoría "${nombreCategoria}" añadida.`, 'success');
}

// Elimina una categoría existente
async function eliminarCategoria(idCategoria) {
  // Verificar si hay productos en esta categoría
  const productosEnCategoria = Object.keys(productos).filter(prodName => productos[prodName].categoria === idCategoria);
  
  let confirmMessage = `¿Estás seguro de que quieres eliminar la categoría "${categorias[idCategoria].nombre}"? Esta acción es irreversible.`;
  if (productosEnCategoria.length > 0) {
    confirmMessage = `La categoría "${categorias[idCategoria].nombre}" tiene ${productosEnCategoria.length} productos asociados. ¿Estás seguro de que quieres eliminarla? ¡Los productos de esta categoría TAMBIÉN serán eliminados!`;
  }

  if (!confirm(confirmMessage)) {
    return;
  }

  // Eliminar productos asociados a la categoría
  productosEnCategoria.forEach(prodName => {
    delete productos[prodName];
  });
  await guardarProductosEnFirebase(); // Guardar cambios en productos en Firebase

  if (categorias[idCategoria]) {
    delete categorias[idCategoria];
    await guardarCategoriasEnFirebase(); // Guardar cambios en categorías en Firebase
    
    cargarCategoriasEnDOM();
    cargarProductosEnDOM();
    actualizarListaCategoriasAdmin();
    actualizarEstadisticas();
    mostrarNotificacion(`Categoría "${idCategoria}" y sus productos asociados eliminados.`, 'success');
    
    // Si la categoría activa era la eliminada, cambiar a la primera disponible
    const categoriaActiva = document.querySelector('.card-categoria.activa');
    if (!categoriaActiva || categoriaActiva.dataset.categoria === idCategoria) {
      const primeraCategoriaId = Object.keys(categorias)[0];
      if (primeraCategoriaId) {
          mostrarCategoria(primeraCategoriaId);
      } else {
          document.querySelectorAll('.contenido-categoria').forEach(div => div.classList.add('oculto'));
      }
    }
  } else {
    mostrarNotificacion(`Categoría "${idCategoria}" no encontrada.`, 'error');
  }
}

// =====================================
// FUNCIONES: PANTALLA DE PEDIDOS EN COCINA
// =====================================

// Escucha los pedidos en tiempo real desde Firebase
function escucharPedidosDeCocina() {
  // Si ya hay un listener activo, lo desuscribimos para evitar duplicados
  if (unsubscribeKitchenListener) {
    unsubscribeKitchenListener();
    console.log("DEBUG: Listener de cocina anterior desuscrito.");
  }

  // Crea una consulta a la colección de pedidos pendientes
  const pedidosCollectionRef = db.collection('pedidosPendientes');
  const q = pedidosCollectionRef.orderBy('id'); // Ordenamos por ID (timestamp) para que los más nuevos salgan al final

  // Configura el listener en tiempo real
  unsubscribeKitchenListener = q.onSnapshot((querySnapshot) => {
    const nuevosPedidos = [];
    querySnapshot.forEach((doc) => {
      nuevosPedidos.push(doc.data());
    });
    pedidosPendientes = nuevosPedidos; // Actualiza la variable global
    actualizarPantallaCocinaUI(); // Actualiza la interfaz de usuario de la cocina
    console.log("DEBUG: Pedidos en tiempo real actualizados:", pedidosPendientes.length);
  }, (error) => {
    console.error("Error al escuchar pedidos de cocina:", error);
    mostrarNotificacion("Error al sincronizar pedidos de cocina. Revisa tu conexión.", 'error');
  });
  console.log("DEBUG: Listener de pedidos de cocina iniciado.");
}


// Actualiza la visualización de los pedidos pendientes en la pantalla de cocina
function actualizarPantallaCocinaUI() {
  const pedidosGrid = document.getElementById('pedidosPendientesGrid');
  const noPedidosMessage = document.getElementById('noPedidosMessage');
  pedidosGrid.innerHTML = ''; // Limpiar grid antes de volver a renderizar

  if (pedidosPendientes.length === 0) {
    noPedidosMessage.style.display = 'block'; // Mostrar mensaje de "no hay pedidos"
    pedidosGrid.appendChild(noPedidosMessage); // Asegurarse de que el mensaje está dentro del grid
    return;
  } else {
    noPedidosMessage.style.display = 'none'; // Ocultar mensaje si hay pedidos
  }

  pedidosPendientes.forEach(order => {
    const orderCard = document.createElement('div');
    orderCard.className = 'order-card';
    
    let itemsListHtml = '';
    order.items.forEach(item => {
      const aderezoHtml = item.aderezo ? `<span class="aderezo">(${item.aderezo})</span>` : '';
      itemsListHtml += `<li>${item.nombre} ${aderezoHtml}</li>`;
    });

    orderCard.innerHTML = `
      <h3>Pedido para: ${order.cliente}</h3>
      <ul class="items-list">
        ${itemsListHtml}
      </ul>
      <div class="order-total">Total: $${order.total.toFixed(2)}</div>
      <div class="order-payment">Pago: ${order.metodoPago}</div>
      <div class="order-time">Hora del pedido: ${order.hora}</div>
      <button class="btn-marcar-listo" onclick="prepararMarcarPedidoListo('${order.id}')">
        ✅ Marcar como Listo
      </button>
    `;
    pedidosGrid.appendChild(orderCard);
  });
}

// Función intermedia para preparar la confirmación de "Marcar como Listo"
function prepararMarcarPedidoListo(orderId) {
    console.log("DEBUG: prepararMarcarPedidoListo - ID del pedido a confirmar:", orderId);
    currentOrderIdToConfirm = orderId; // Guarda el ID globalmente

    const orderToConfirm = pedidosPendientes.find(order => order.id === orderId);
    if (orderToConfirm) {
        document.getElementById('confirmarPedidoCliente').textContent = orderToConfirm.cliente;
        abrirModal('confirmarPedidoListoModal');
    } else {
        mostrarNotificacion('Error: Pedido no encontrado para confirmar.', 'error');
        console.error("ERROR: prepararMarcarPedidoListo - Pedido con ID", orderId, "no encontrado.");
    }
}

// Función que ejecuta la acción de "Marcar como Listo" después de la confirmación
async function confirmarPedidoListoAccion() {
    if (currentOrderIdToConfirm === null) {
        console.error("ERROR: confirmarPedidoListoAccion - No hay ID de pedido para confirmar.");
        mostrarNotificacion('Error en la confirmación del pedido. Intenta de nuevo.', 'error');
        return;
    }

    const orderId = currentOrderIdToConfirm;
    console.log("DEBUG: confirmarPedidoListoAccion - Ejecutando para ID:", orderId);

    try {
        await db.collection('pedidosPendientes').doc(orderId).delete();
        console.log(`DEBUG: Pedido ${orderId} eliminado de Firebase.`);
        // La UI se actualizará automáticamente gracias al listener onSnapshot
        mostrarNotificacion('Pedido marcado como listo y eliminado de la cola.', 'success');
    } catch (e) {
        console.error("Error al eliminar pedido de Firebase:", e);
        mostrarNotificacion("Error al marcar pedido como listo. Intenta de nuevo.", 'error');
    }

    currentOrderIdToConfirm = null; // Reinicia la variable
    cerrarModal('confirmarPedidoListoModal');
    console.log("DEBUG: Modal de confirmación cerrado.");
}

// Función para cancelar la acción de "Marcar como Listo"
function cancelarPedidoListoAccion() {
    console.log("DEBUG: cancelarPedidoListoAccion - Acción de marcar como listo cancelada.");
    currentOrderIdToConfirm = null; // Reinicia la variable
    cerrarModal('confirmarPedidoListoModal');
    mostrarNotificacion('Acción de marcar pedido como listo cancelada.', 'info');
}

// =====================================
// FUNCIONES DE UTILIDAD / UX
// =====================================

// Muestra una notificación temporal al usuario
function mostrarNotificacion(mensaje, tipo = 'info') {
  const notificacionDiv = document.createElement('div');
  notificacionDiv.className = `notificacion ${tipo}`;
  notificacionDiv.textContent = mensaje;
  document.body.appendChild(notificacionDiv);

  // Eliminar la notificación después de 3 segundos
  setTimeout(() => {
    notificacionDiv.remove();
  }, 3000);
}

// Alterna entre modo oscuro y modo claro
function toggleModoOscuro() {
  modoOscuro = !modoOscuro;
  setSetting('modoOscuro', modoOscuro);
  setSetting('modoOscuroManual', true); // Indicar que el usuario lo cambió manualmente
  
  aplicarModoOscuro();
  mostrarNotificacion(`Modo Oscuro: ${modoOscuro ? 'Activado' : 'Desactivado'}`, 'info');
}

// Aplica o remueve la clase 'dark-mode' al body
function aplicarModoOscuro() {
  if (modoOscuro) {
    document.body.classList.add('dark-mode');
    document.getElementById('btnModoOscuro').textContent = '☀️'; // Icono de sol
  } else {
    document.body.classList.remove('dark-mode');
    document.getElementById('btnModoOscuro').textContent = '🌙'; // Icono de luna
  }
}

</script>
</body>
</html>
