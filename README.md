<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Repuestos TDT</title>
    <style>
        :root { --primary: #e11c19; --dark: #060606; --light: #f4f4f4; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: var(--light); }
        header { background: var(--dark); color: rgb(211, 27, 27); padding: 1rem; text-align: center; }
        .search-container { padding: 20px; text-align: center; background: #fff; box-shadow: 0 2px 5px rgba(255, 254, 254, 0.1); }
        input { padding: 10px; width: 60%; border: 1px solid #ccc; border-radius: 5px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; padding: 20px; }
        .card { background: rgb(248, 246, 246); padding: 15px; border-radius: 8px; box-shadow: 0 4px 6px rgba(241, 9, 9, 0.79); text-align: center; transition: 0.3s; }
        .card:hover { transform: translateY(-5px); }
        .card h3 { color: var(--primary); margin: 10px 0; }
        .card button { background: var(--primary); color: rgb(6, 0, 0); border: none; padding: 10px 15px; cursor: pointer; border-radius: 4px; }
    </style>
</head>
<body>

<header>
    <h1>Repuestos TDT</h1>
</header>

<div class="search-container">
    <input type="text" id="buscador" placeholder="Busca tu repuesto (ej: bomba de agua, tensor)...">
</div>

<div class="grid" id="contenedor-productos">
    <!-- Los repuestos se cargarán aquí dinámicamente -->
</div>

<script>
    // 1. Datos de ejemplo (Simulando una base de datos)
    const productos = [
        { id: 1, nombre: "Bomba de agua npw", categoria: "motor", precio: "$55.00" },
        { id: 2, nombre: "kit de tiempo osk", categoria: "kit de distribuccion", precio: "$85.00" },
        { id: 3, nombre: "tensor gmb", categoria: "", precio: "$4.00" },
        { id: 4, nombre: "correa de tiempo sun", categoria: "correa", precio: "$45.00" },
        { id: 5, nombre: "kit de tiempo gmb", categoria: "kit de distribucion", precio: "$85.00" }
    ];

    const contenedor = document.getElementById('contenedor-productos');
    const buscador = document.getElementById('buscador');

    // 2. Función para mostrar productos
    function mostrarProductos(lista) {
        contenedor.innerHTML = ''; // Limpiar contenedor
        lista.forEach(prod => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <h3>${prod.nombre}</h3>
                <p>Categoría: ${prod.categoria}</p>
                <p><strong>${prod.precio}</strong></p>
                <button onclick="agregarAlCarrito(${prod.id})">Agregar</button>
            `;
            contenedor.appendChild(card);
        });
    }

    // 3. Lógica del buscador (Filtrado en tiempo real)
    buscador.addEventListener('input', (e) => {
        const busqueda = e.target.value.toLowerCase();
        const filtrados = productos.filter(p => 
            p.nombre.toLowerCase().includes(busqueda) || 
            p.categoria.toLowerCase().includes(busqueda)
        );
        mostrarProductos(filtrados);
    });

    // 4. Función de interacción simple
    function agregarAlCarrito(id) {
        const prod = productos.find(p => p.id === id);
        alert(`¡${prod.nombre} añadido al carrito de Repuestos TDT!`);
    }

    // Carga inicial
    mostrarProductos(productos);
</script>

</body>
</html>
