<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Maíz Solo</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    #cover-panel {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: #0D3D0C;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2.5rem;
      font-weight: bold;
      z-index: 1000;
      cursor: pointer;
      opacity: 1;
      transition: opacity 1s ease-out;
    }
    #cover-panel.hidden {
      opacity: 0;
      pointer-events: none;
    }
    .hidden {
      display: none;
    }
    .tab-button {
      padding: 10px;
      cursor: pointer;
      text-decoration: none;
      color: white;
      background-color: #0D3D0C;
      border: 2px solid transparent;
      border-radius: 8px;
    }
    .tab-button:hover {
      background-color: #2b6e34;
    }
    .tab-button.active {
      background-color: #2b6e34;
      border-color: white;
    }
    .card:hover {
      transform: scale(1.05);
      transition: transform 0.3s ease;
    }
    .swiper-container {
      width: 100%;
      height: 200px;
    }
    .swiper-slide {
      background: #f0fff4;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.2rem;
    }
  </style>
</head>
<body class="bg-[#f0fff4] font-sans text-gray-900">

  <!-- Pantalla inicial -->
  <div id="cover-panel" onclick="ocultarPanel()">
    Maíz Solo
  </div>

  <!-- Header -->
  <header class="bg-[#0D3D0C] text-white shadow-md py-4 sticky top-0 z-40">
    <div class="container mx-auto flex justify-between items-center px-6">
      <h1 class="text-3xl font-extrabold tracking-wide">Maíz Solo</h1>
      <nav class="space-x-4">
        <a href="#" class="tab-button active" onclick="mostrarSeccion('productos')">Productos</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('reseñas')">Reseñas</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('blog')">Blog</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('ofertas')">Ofertas</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('cobertura')">Cobertura</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('infraestructura')">Infraestructura</a>
        <a href="#" class="tab-button" onclick="mostrarSeccion('logistica')">Logística</a>
      </nav>
      <button id="cart-button" class="relative bg-white text-[#0D3D0C] px-4 py-2 rounded-full hover:bg-gray-100 transition">
        🛒
        <span id="cart-count" class="absolute -top-2 -right-2 bg-red-600 text-white text-xs w-5 h-5 flex items-center justify-center rounded-full">0</span>
      </button>
    </div>
  </header>

  <!-- Barra de búsqueda -->
  <div class="mb-6 container mx-auto text-center">
    <input type="text" placeholder="Buscar productos..." class="px-4 py-2 border rounded" id="search">
    <button onclick="buscarProducto()" class="bg-[#0D3D0C] text-white px-4 py-2 rounded">Buscar</button>
  </div>

  <!-- Pantalla de estado -->
  <div class="bg-yellow-300 text-black text-center py-2">
    <p>Actualmente estamos realizando mejoras en el sitio. ¡Gracias por tu paciencia!</p>
  </div>

  <main class="px-6 py-10">
    <!-- Sección Productos -->
    <section id="productos" class="seccion">
      <h2 class="text-3xl font-bold mb-6">Productos</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <div class="bg-white shadow rounded p-4 card">
          <h3 class="font-bold text-xl mb-2">Tortillas de Maíz</h3>
          <p>Hechas con maíz 100% natural.</p>
          <select class="mt-2 border p-1 rounded" onchange="agregarProducto('Tortillas de Maíz', this.value)">
            <option value="">Cantidad</option>
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="Otro">Otra cantidad</option>
          </select>
        </div>
      </div>
    </section>

    <!-- Sección Reseñas -->
    <section id="reseñas" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Reseñas</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <!-- Reseña 1 -->
        <div class="bg-white p-4 rounded shadow-lg">
          <p class="text-lg font-semibold">"Excelente producto, muy frescas!"</p>
          <p>- Ana</p>
        </div>
        <!-- Reseña 2 -->
        <div class="bg-white p-4 rounded shadow-lg">
          <p class="text-lg font-semibold">"Servicio de entrega rápido y confiable."</p>
          <p>- Juan</p>
        </div>
        <!-- Reseña 3 -->
        <div class="bg-white p-4 rounded shadow-lg">
          <p class="text-lg font-semibold">"Muy buen sabor y calidad. Recomendado!"</p>
          <p>- Carlos</p>
        </div>
      </div>
    </section>

    <!-- Sección Blog -->
    <section id="blog" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Blog</h2>
      <div class="grid md:grid-cols-2 gap-6">
        <div class="bg-white p-4 rounded shadow">
          <h3 class="text-xl font-semibold">El maíz y la tradición</h3>
          <p>Conoce cómo el maíz forma parte esencial de nuestra cultura alimentaria.</p>
        </div>
      </div>
    </section>

    <!-- Sección Ofertas -->
    <section id="ofertas" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Ofertas</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-semibold text-lg">3x2 en Totopos</h3>
          <p>Solo por esta semana, no te lo pierdas.</p>
        </div>
      </div>
    </section>

    <!-- Sección Cobertura -->
    <section id="cobertura" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Cobertura</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-semibold text-lg">México</h3>
          <p>Presencia en Ciudad de México, Guadalajara, Monterrey...</p>
        </div>
        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-semibold text-lg">Estados Unidos</h3>
          <p>Exportación a Texas, California, Illinois...</p>
        </div>
      </div>
    </section>

    <!-- Sección Infraestructura -->
    <section id="infraestructura" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Infraestructura</h2>
      <div class="bg-white p-6 rounded shadow">
        <p>Contamos con plantas modernas equipadas con tecnología de punta para garantizar productos frescos y de alta calidad.</p>
      </div>
    </section>

    <!-- Sección Logística -->
    <section id="logistica" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Logística</h2>
      <div class="bg-white p-6 rounded shadow">
        <p>Con una red logística nacional e internacional, aseguramos entregas rápidas y eficientes. Trabajamos con socios confiables para mantener nuestra promesa de calidad.</p>
      </div>
    </section>

    <!-- Formulario de Contacto -->
    <section id="contacto" class="seccion hidden">
      <h2 class="text-3xl font-bold mb-6">Formulario de Contacto</h2>
      <form action="mailto:tuemail@dominio.com" method="POST" enctype="multipart/form-data">
        <input type="text" name="nombre" placeholder="Tu nombre" class="w-full p-2 mb-4 border rounded" required />
        <input type="email" name="email" placeholder="Tu email" class="w-full p-2 mb-4 border rounded" required />
        <textarea name="mensaje" placeholder="Tu mensaje" class="w-full p-2 mb-4 border rounded" required></textarea>
        <button type="submit" class="bg-[#0D3D0C] text-white px-4 py-2 rounded">Enviar</button>
      </form>
    </section>

    <!-- Botón de Suscripción -->
    <section id="suscripcion" class="bg-[#0D3D0C] text-white py-10 mt-10">
      <div class="container mx-auto text-center">
        <h2 class="text-2xl mb-4">¡Suscríbete a nuestro boletín!</h2>
        <p>Recibe las últimas noticias y ofertas directamente en tu correo.</p>
        <form action="#" method="POST" class="mt-6">
          <input type="email" name="email" placeholder="Tu correo electrónico" class="px-4 py-2 w-2/3 border rounded" required />
          <button type="submit" class="bg-yellow-400 text-black px-4 py-2 ml-4 rounded">Suscribirse</button>
        </form>
      </div>
    </section>
  </main>

  <!-- Footer -->
  <footer class="bg-[#0D3D0C] text-white py-6 mt-10">
    <div class="container mx-auto text-center">
      <p>&copy; 2025 Maíz Solo. Todos los derechos reservados.</p>
      <div class="mt-4">
        <a href="#" class="mx-2">Facebook</a>
        <a href="#" class="mx-2">Instagram</a>
        <a href="#" class="mx-2">Twitter</a>
      </div>
    </div>
  </footer>

  <script src="https://unpkg.com/swiper/swiper-bundle.min.js"></script>
  <script>
    function ocultarPanel() {
      document.getElementById('cover-panel').classList.add('hidden');
    }

    function mostrarSeccion(seccion) {
      const secciones = document.querySelectorAll('.seccion');
      const botones = document.querySelectorAll('.tab-button');
      
      secciones.forEach(section => section.classList.add('hidden'));
      botones.forEach(btn => btn.classList.remove('active'));
      
      document.getElementById(seccion).classList.remove('hidden');
      document.querySelector(`[onclick="mostrarSeccion('${seccion}')"]`).classList.add('active');
    }

    function buscarProducto() {
      alert('Buscando productos...');
    }

    let cartCount = 0;
    function agregarProducto(producto, cantidad) {
      if (cantidad !== '') {
        cartCount += parseInt(cantidad);
        document.getElementById('cart-count').textContent = cartCount;
      }
    }
  </script>

</body>
</html>
