<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">vffyy
  <title>Mi Tienda Estilo Temu</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: #f4f4f4;
      padding-top: 60px;
      padding-bottom: 70px;
    }

    /* BARRA SUPERIOR */
    .header {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      height: 60px;
      background-color: #fb5200; /* Color naranja característico */
      display: flex;
      align-items: center;
      padding: 0 12px;
      gap: 10px;
      z-index: 1000;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    .search-bar {
      flex: 1;
      background: #fff;
      border-radius: 20px;
      display: flex;
      align-items: center;
      padding: 6px 12px;
    }

    .search-bar input {
      border: none;
      outline: none;
      width: 100%;
      font-size: 14px;
      margin-left: 6px;
    }

    .header-icon {
      color: white;
      font-size: 20px;
      cursor: pointer;
    }

    /* BANNER DE OFERTAS Y BANDERAS */
    .flash-deal-banner {
      background: linear-gradient(90deg, #ff0055, #fb5200);
      color: white;
      padding: 10px 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: bold;
      font-size: 14px;
    }

    .timer {
      background: rgba(0,0,0,0.2);
      padding: 4px 8px;
      border-radius: 4px;
      font-family: monospace;
      font-size: 13px;
    }

    /* CATEGORÍAS */
    .categories {
      display: flex;
      overflow-x: auto;
      background: white;
      padding: 10px;
      gap: 15px;
      white-space: nowrap;
      scrollbar-width: none;
    }
    .categories::-webkit-scrollbar { display: none; }

    .cat-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      font-size: 12px;
      color: #333;
      cursor: pointer;
    }

    .cat-item img {
      width: 45px;
      height: 45px;
      border-radius: 50%;
      object-fit: cover;
      margin-bottom: 4px;
      background: #eee;
    }

    /* CATÁLOGO DE PRODUCTOS (GRID DE 2 COLUMNAS) */
    .products-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      padding: 10px;
    }

    .product-card {
      background: white;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 1px 4px rgba(0,0,0,0.08);
      display: flex;
      flex-direction: column;
      position: relative;
    }

    .product-card img {
      width: 100%;
      height: 160px;
      object-fit: cover;
    }

    .product-info {
      padding: 8px;
      display: flex;
      flex-direction: column;
      flex: 1;
    }

    .product-title {
      font-size: 13px;
      color: #333;
      height: 34px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      margin-bottom: 6px;
    }

    .price-row {
      display: flex;
      align-items: baseline;
      gap: 6px;
      margin-bottom: 6px;
    }

    .price {
      color: #fb5200;
      font-size: 16px;
      font-weight: bold;
    }

    .old-price {
      color: #888;
      font-size: 11px;
      text-decoration: line-through;
    }

    .badge {
      background: #ffebe8;
      color: #fb5200;
      font-size: 10px;
      padding: 2px 4px;
      border-radius: 3px;
      width: fit-content;
      margin-bottom: 8px;
    }

    .btn-add {
      background: #fb5200;
      color: white;
      border: none;
      padding: 8px;
      border-radius: 15px;
      font-weight: bold;
      font-size: 12px;
      cursor: pointer;
      margin-top: auto;
      width: 100%;
    }

    /* NAVEGACIÓN INFERIOR */
    .bottom-nav {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      height: 60px;
      background: white;
      border-top: 1px solid #e5e5e5;
      display: flex;
      justify-content: space-around;
      align-items: center;
      z-index: 1000;
    }

    .nav-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      font-size: 11px;
      color: #666;
      text-decoration: none;
      cursor: pointer;
      position: relative;
    }

    .nav-item.active {
      color: #fb5200;
      font-weight: bold;
    }

    .cart-badge {
      position: absolute;
      top: -4px;
      right: 4px;
      background: #ff0055;
      color: white;
      border-radius: 10px;
      padding: 2px 6px;
      font-size: 10px;
      font-weight: bold;
    }

    /* MODAL CARRITO */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.5);
      z-index: 2000;
      justify-content: flex-end;
      flex-direction: column;
    }

    .modal-content {
      background: white;
      border-top-left-radius: 16px;
      border-top-right-radius: 16px;
      max-height: 80vh;
      padding: 20px;
      display: flex;
      flex-direction: column;
      overflow-y: auto;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
      border-bottom: 1px solid #eee;
      padding-bottom: 10px;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
    }

    .btn-checkout {
      background: #fb5200;
      color: white;
      border: none;
      padding: 12px;
      border-radius: 25px;
      font-size: 16px;
      font-weight: bold;
      width: 100%;
      margin-top: 15px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <!-- ENCABEZADO CON BUSCADOR -->
  <div class="header">
    <div class="search-bar">
      🔍 <input type="text" id="searchInput" placeholder="Buscar en la tienda..." onkeyup="filterProducts()">
    </div>
    <div class="header-icon" onclick="toggleCart()">🛒</div>
  </div>

  <!-- BANNER DE OFERTAS RELÁMPAGO -->
  <div class="flash-deal-banner">
    <span>⚡ Ofertas Relámpago - Hasta 70% OFF</span>
    <span class="timer" id="countdown">04:59:59</span>
  </div>

  <!-- CATEGORÍAS -->
  <div class="categories">
    <div class="cat-item" onclick="filterCategory('todos')">
      <img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=100" alt="Todo">
      <span>Todos</span>
    </div>
    <div class="cat-item" onclick="filterCategory('tecnologia')">
      <img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=100" alt="Tech">
      <span>Tecnología</span>
    </div>
    <div class="cat-item" onclick="filterCategory('herramientas')">
      <img src="https://images.unsplash.com/photo-1581092160607-ee22621dd758?w=100" alt="Tools">
      <span>Herramientas</span>
    </div>
    <div class="cat-item" onclick="filterCategory('hogar')">
      <img src="https://images.unsplash.com/photo-1583847268964-b28dc8f51f92?w=100" alt="Hogar">
      <span>Hogar</span>
    </div>
  </div>

  <!-- GRID DE PRODUCTOS -->
  <div class="products-grid" id="productsGrid"></div>

  <!-- BARRA DE NAVEGACIÓN INFERIOR (ESTILO APP MÓVIL) -->
  <div class="bottom-nav">
    <div class="nav-item active">
      🏠 <span>Inicio</span>
    </div>
    <div class="nav-item" onclick="alert('Sección de ofertas')">
      ⚡ <span>Ofertas</span>
    </div>
    <div class="nav-item" onclick="toggleCart()">
      🛒 <span>Carrito</span>
      <span class="cart-badge" id="cartCount">0</span>
    </div>
    <div class="nav-item" onclick="alert('Sección de Usuario')">
      👤 <span>Perfil</span>
    </div>
  </div>

  <!-- MODAL DEL CARRITO -->
  <div class="modal" id="cartModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>Tu Carrito</h3>
        <span style="font-size: 20px; cursor: pointer;" onclick="toggleCart()">✕</span>
      </div>
      <div id="cartItemsList">
        <p style="text-align: center; color: #888; margin: 20px 0;">El carrito está vacío</p>
      </div>
      <div style="margin-top: 15px; font-weight: bold; font-size: 18px; display: flex; justify-content: space-between;">
        <span>Total:</span>
        <span id="cartTotal">$0 COP</span>
      </div>
      <button class="btn-checkout" onclick="checkout()">Proceder al Pago</button>
    </div>
  </div>

  <script>
    // BASE DE DATOS DE PRODUCTOS DE EJEMPLO
    const products = [
      {
        id: 1,
        title: "Audífonos Inalámbricos Bluetooth HD Bass",
        category: "tecnologia",
        price: 35000,
        oldPrice: 85000,
        badge: "Envío Gratis",
        image: "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=400"
      },
      {
        id: 2,
        title: "Multímetro Digital Profesional Automático",
        category: "herramientas",
        price: 62000,
        oldPrice: 120000,
        badge: "Más vendido",
        image: "https://images.unsplash.com/photo-1581092160607-ee22621dd758?w=400"
      },
      {
        id: 3,
        title: "Lámpara LED Inteligente RGB USB",
        category: "hogar",
        price: 28000,
        oldPrice: 50000,
        badge: "Oferta -44%",
        image: "https://images.unsplash.com/photo-1583847268964-b28dc8f51f92?w=400"
      },
      {
        id: 4,
        title: "Reloj Inteligente Smartwatch Deportivo",
        category: "tecnologia",
        price: 79000,
        oldPrice: 190000,
        badge: "Casi agotado",
        image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=400"
      }
    ];

    let cart = [];

    // CARGAR PRODUCTOS EN LA PANTALLA
    function renderProducts(items) {
      const container = document.getElementById('productsGrid');
      container.innerHTML = '';
      
      items.forEach(product => {
        container.innerHTML += `
          <div class="product-card">
            <img src="${product.image}" alt="${product.title}">
            <div class="product-info">
              <div class="product-title">${product.title}</div>
              <div class="price-row">
                <span class="price">$${product.price.toLocaleString()}</span>
                <span class="old-price">$${product.oldPrice.toLocaleString()}</span>
              </div>
              <div class="badge">${product.badge}</div>
              <button class="btn-add" onclick="addToCart(${product.id})">Añadir al Carrito</button>
            </div>
          </div>
        `;
      });
    }

    // FILTRAR POR BÚSQUEDA
    function filterProducts() {
      const query = document.getElementById('searchInput').value.toLowerCase();
      const filtered = products.filter(p => p.title.toLowerCase().includes(query));
      renderProducts(filtered);
    }

    // FILTRAR POR CATEGORÍA
    function filterCategory(cat) {
      if (cat === 'todos') {
        renderProducts(products);
      } else {
        const filtered = products.filter(p => p.category === cat);
        renderProducts(filtered);
      }
    }

    // LÓGICA DEL CARRITO
    function addToCart(id) {
      const prod = products.find(p => p.id === id);
      cart.push(prod);
      updateCartUI();
    }

    function updateCartUI() {
      document.getElementById('cartCount').innerText = cart.length;
      
      const listContainer = document.getElementById('cartItemsList');
      if (cart.length === 0) {
        listContainer.innerHTML = '<p style="text-align: center; color: #888; margin: 20px 0;">El carrito está vacío</p>';
        document.getElementById('cartTotal').innerText = '$0 COP';
        return;
      }

      listContainer.innerHTML = '';
      let total = 0;

      cart.forEach((item, index) => {
        total += item.price;
        listContainer.innerHTML += `
          <div class="cart-item">
            <div>
              <div style="font-size: 13px; font-weight: bold;">${item.title}</div>
              <div style="color: #fb5200; font-size: 14px;">$${item.price.toLocaleString()} COP</div>
            </div>
            <button onclick="removeFromCart(${index})" style="background: none; border: none; color: red; cursor: pointer;">Eliminar</button>
          </div>
        `;
      });

      document.getElementById('cartTotal').innerText = `$${total.toLocaleString()} COP`;
    }

    function removeFromCart(index) {
      cart.splice(index, 1);
      updateCartUI();
    }

    function toggleCart() {
      const modal = document.getElementById('cartModal');
      modal.style.display = modal.style.display === 'flex' ? 'none' : 'flex';
    }

    function checkout() {
      if (cart.length === 0) {
        alert('Tu carrito está vacío');
        return;
      }
      alert('¡Redirigiendo a la pasarela de pago (Mercado Pago / PSE / Wompi)...!');
    }

    // RELOJ REGRESIVO
    function startTimer() {
      let duration = 5 * 3600; // 5 horas
      const display = document.getElementById('countdown');
      setInterval(() => {
        let hours = Math.floor(duration / 3600);
        let minutes = Math.floor((duration % 3600) / 60);
        let seconds = duration % 60;

        display.innerText = 
          (hours < 10 ? "0" + hours : hours) + ":" +
          (minutes < 10 ? "0" + minutes : minutes) + ":" +
          (seconds < 10 ? "0" + seconds : seconds);

        if (--duration < 0) duration = 5 * 3600;
      }, 1000);
    }

    // INICIALIZACIÓN
    window.onload = () => {
      renderProducts(products);
      startTimer();
    };
  </script>
</body>
</html>
