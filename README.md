<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Control de Reparaciones Pro</title>
    <style>
        :root {
            --primary-color: #667eea;
            --secondary-color: #764ba2;
            --success-color: #56ab2f;
            --warning-color: #f093fb;
            --danger-color: #ff6b6b;
            --info-color: #74b9ff;
            --text-color: #2c3e50;
            --bg-color: #ffffff;
            --card-bg: #ffffff;
            --border-color: #e9ecef;
            --shadow: 0 2px 10px rgba(0,0,0,0.1);
            --gradient-bg: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        [data-theme="dark"] {
            --text-color: #e2e8f0;
            --bg-color: #1a202c;
            --card-bg: #2d3748;
            --border-color: #4a5568;
            --shadow: 0 2px 10px rgba(0,0,0,0.3);
            --gradient-bg: linear-gradient(135deg, #4a5568 0%, #2d3748 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--gradient-bg);
            min-height: 100vh;
            padding: 10px;
            color: var(--text-color);
            transition: all 0.3s ease;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: var(--bg-color);
            border-radius: 15px;
            box-shadow: var(--shadow);
            overflow: hidden;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 20px;
            text-align: center;
            position: relative;
        }

        .header-controls {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
        }

        .theme-toggle {
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            padding: 8px 12px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .theme-toggle:hover {
            background: rgba(255,255,255,0.3);
            transform: scale(1.1);
        }

        .offline-indicator {
            background: #ff6b6b;
            color: white;
            padding: 5px 15px;
            border-radius: 15px;
            font-size: 12px;
            display: none;
        }

        .logo {
            width: 60px;
            height: 60px;
            margin: 0 auto 10px;
            background: rgba(255,255,255,0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            animation: pulse 2s infinite;
        }

        .header h1 {
            font-size: 24px;
            margin-bottom: 5px;
        }

        .header p {
            opacity: 0.9;
            font-size: 14px;
        }

        .main-content {
            padding: 20px;
        }

        .form-section {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            border: 2px solid var(--border-color);
            animation: fadeIn 0.5s ease-out;
        }

        .form-section h2 {
            color: var(--text-color);
            margin-bottom: 15px;
            font-size: 18px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: var(--text-color);
            font-weight: 500;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            font-size: 14px;
            transition: all 0.3s;
            background: var(--card-bg);
            color: var(--text-color);
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary-color);
            transform: scale(1.02);
        }

        .form-group textarea {
            height: 80px;
            resize: vertical;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .image-upload {
            border: 2px dashed var(--border-color);
            padding: 20px;
            text-align: center;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .image-upload:hover {
            border-color: var(--primary-color);
            background: rgba(102, 126, 234, 0.1);
        }

        .image-preview {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }

        .image-item {
            position: relative;
            width: 100px;
            height: 100px;
            border-radius: 8px;
            overflow: hidden;
        }

        .image-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .image-remove {
            position: absolute;
            top: 5px;
            right: 5px;
            background: #ff6b6b;
            color: white;
            border: none;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            cursor: pointer;
            font-size: 12px;
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            margin: 5px;
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success-color), #a8e6cf);
            color: white;
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning-color), #f5576c);
            color: white;
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger-color), #ee5a24);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(135deg, var(--info-color), #0984e3);
            color: white;
        }

        .button-group {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        /* Filtros y búsqueda */
        .search-filters {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }

        .search-box {
            position: relative;
        }

        .search-box input {
            padding-left: 40px;
        }

        .search-box::before {
            content: "🔍";
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            z-index: 1;
        }

        /* Paginación */
        .pagination {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin: 20px 0;
        }

        .pagination button {
            padding: 8px 12px;
            border: 1px solid var(--border-color);
            background: var(--card-bg);
            color: var(--text-color);
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .pagination button:hover {
            background: var(--primary-color);
            color: white;
        }

        .pagination button.active {
            background: var(--primary-color);
            color: white;
        }

        .pagination button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Lista de reparaciones */
        .repair-list {
            margin-top: 20px;
        }

        .repair-item {
            background: var(--card-bg);
            border: 2px solid var(--border-color);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: var(--shadow);
            transition: all 0.3s;
            animation: fadeIn 0.5s ease-out;
        }

        .repair-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }

        .repair-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .repair-title {
            font-weight: bold;
            color: var(--text-color);
            font-size: 16px;
        }

        .repair-cost {
            color: var(--success-color);
            font-weight: bold;
            font-size: 18px;
        }

        .repair-details {
            color: var(--text-color);
            line-height: 1.5;
            opacity: 0.8;
        }

        .repair-actions {
            margin-top: 10px;
            display: flex;
            gap: 10px;
        }

        .repair-images {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .repair-images img {
            width: 60px;
            height: 60px;
            border-radius: 5px;
            object-fit: cover;
            cursor: pointer;
            transition: all 0.3s;
        }

        .repair-images img:hover {
            transform: scale(1.1);
        }

        .empty-state {
            text-align: center;
            padding: 40px;
            color: var(--text-color);
            opacity: 0.6;
        }

        .empty-state svg {
            width: 80px;
            height: 80px;
            margin-bottom: 20px;
            opacity: 0.5;
        }

        .status-badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 15px;
            font-size: 12px;
            font-weight: 500;
            margin-left: 10px;
        }

        .status-pendiente {
            background: #fff3cd;
            color: #856404;
        }

        .status-en-proceso {
            background: #d4edda;
            color: #155724;
        }

        .status-completado {
            background: #d1ecf1;
            color: #0c5460;
        }

        /* Notificaciones */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            border-radius: 8px;
            color: white;
            font-weight: 500;
            z-index: 9999;
            animation: slideInRight 0.3s ease-out;
            max-width: 300px;
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .notification.success {
            background: var(--success-color);
        }

        .notification.error {
            background: var(--danger-color);
        }

        .notification.info {
            background: var(--info-color);
        }

        /* Modal para calendario */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 10000;
            animation: fadeIn 0.3s ease-out;
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: var(--card-bg);
            padding: 30px;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
            animation: slideIn 0.3s ease-out;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: var(--text-color);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .search-filters {
                grid-template-columns: 1fr;
            }
            
            .button-group {
                justify-content: center;
            }
            
            .repair-actions {
                flex-direction: column;
            }

            .header-controls {
                position: relative;
                top: auto;
                right: auto;
                justify-content: center;
                margin-top: 15px;
            }
        }

        .hidden {
            display: none;
        }

        /* Indicador de entrega próxima */
        .delivery-warning {
            background: linear-gradient(135deg, #ffa726, #ff7043);
            color: white;
            padding: 8px 12px;
            border-radius: 15px;
            font-size: 12px;
            margin-left: 10px;
            animation: pulse 1.5s infinite;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="header-controls">
                <button class="theme-toggle" onclick="toggleTheme()">🌙</button>
                <div class="offline-indicator" id="offline-indicator">Sin conexión</div>
            </div>
            <div class="logo">🔧</div>
            <h1>Control de Reparaciones Pro</h1>
            <p>Gestiona tus servicios de reparación con estilo</p>
        </div>

        <div class="main-content">
            <!-- Formulario -->
            <div class="form-section">
                <h2 id="form-title">Agregar Nueva Reparación</h2>
                <form id="repair-form">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="cliente">Nombre del Cliente</label>
                            <input type="text" id="cliente" name="cliente" required>
                        </div>
                        <div class="form-group">
                            <label for="contacto">Contacto</label>
                            <input type="text" id="contacto" name="contacto" placeholder="Teléfono o email">
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="modelo">Modelo/Equipo</label>
                            <input type="text" id="modelo" name="modelo" required>
                        </div>
                        <div class="form-group">
                            <label for="costo">Costo ($)</label>
                            <input type="number" id="costo" name="costo" step="0.01" min="0">
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="reparacion">Tipo de Reparación</label>
                            <input type="text" id="reparacion" name="reparacion" required>
                        </div>
                        <div class="form-group">
                            <label for="estado">Estado</label>
                            <select id="estado" name="estado">
                                <option value="pendiente">Pendiente</option>
                                <option value="en-proceso">En Proceso</option>
                                <option value="completado">Completado</option>
                            </select>
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="fechaEntrega">Fecha de Entrega</label>
                            <input type="date" id="fechaEntrega" name="fechaEntrega">
                        </div>
                        <div class="form-group">
                            <label for="prioridad">Prioridad</label>
                            <select id="prioridad" name="prioridad">
                                <option value="baja">Baja</option>
                                <option value="media">Media</option>
                                <option value="alta">Alta</option>
                                <option value="urgente">Urgente</option>
                            </select>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="observaciones">Observaciones</label>
                        <textarea id="observaciones" name="observaciones" placeholder="Detalles adicionales, problemas encontrados, etc."></textarea>
                    </div>

                    <div class="form-group">
                        <label>Imágenes del Equipo/Problema</label>
                        <div class="image-upload" onclick="document.getElementById('image-input').click()">
                            <p>📷 Haz clic para adjuntar imágenes</p>
                            <p style="font-size: 12px; opacity: 0.7;">Máximo 5 imágenes por reparación</p>
                        </div>
                        <input type="file" id="image-input" multiple accept="image/*" style="display: none;" onchange="handleImageUpload(event)">
                        <div class="image-preview" id="image-preview"></div>
                    </div>

                    <div class="button-group">
                        <button type="submit" class="btn btn-primary">
                            <span id="btn-text">Guardar Reparación</span>
                        </button>
                        <button type="button" class="btn btn-secondary" id="btn-cancel" onclick="cancelEdit()" style="display: none;">
                            Cancelar
                        </button>
                    </div>
                </form>
            </div>

            <!-- Botones de Acción -->
            <div class="form-section">
                <h2>Acciones</h2>
                <div class="button-group">
                    <button class="btn btn-success" onclick="exportData()">
                        📥 Hacer Copia de Seguridad
                    </button>
                    <button class="btn btn-warning" onclick="importData()">
                        📤 Restaurar Copia
                    </button>
                    <button class="btn btn-secondary" onclick="showCalendar()">
                        📅 Calendario de Entregas
                    </button>
                    <button class="btn btn-danger" onclick="clearAllData()">
                        🗑 Borrar Todo
                    </button>
                </div>
                <input type="file" id="file-input" accept=".json" style="display: none;" onchange="handleFileImport(event)">
            </div>

            <!-- Filtros y Búsqueda -->
            <div class="form-section">
                <h2>Filtros y Búsqueda</h2>
                <div class="search-filters">
                    <div class="search-box">
                        <input type="text" id="search-term" placeholder="Buscar por cliente, modelo o reparación..." onkeyup="filterRepairs()">
                    </div>
                    <div class="form-group">
                        <select id="status-filter" onchange="filterRepairs()">
                            <option value="">Todos los estados</option>
                            <option value="pendiente">Pendiente</option>
                            <option value="en-proceso">En Proceso</option>
                            <option value="completado">Completado</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <select id="sort-by" onchange="sortRepairs()">
                            <option value="fecha-desc">Fecha (Más reciente)</option>
                            <option value="fecha-asc">Fecha (Más antigua)</option>
                            <option value="cliente-asc">Cliente (A-Z)</option>
                            <option value="cliente-desc">Cliente (Z-A)</option>
                            <option value="costo-desc">Costo (Mayor)</option>
                            <option value="costo-asc">Costo (Menor)</option>
                            <option value="entrega-asc">Entrega próxima</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <select id="items-per-page" onchange="updatePagination()">
                            <option value="5">5 por página</option>
                            <option value="10" selected>10 por página</option>
                            <option value="20">20 por página</option>
                            <option value="50">50 por página</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Lista de Reparaciones -->
            <div class="repair-list">
                <h2>Reparaciones Registradas</h2>
                <div class="pagination" id="pagination-top"></div>
                <div id="repairs-container">
                    <div class="empty-state">
                        <svg viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
                        </svg>
                        <p>No hay reparaciones registradas aún.<br>Agrega tu primera reparación usando el formulario de arriba.</p>
                    </div>
                </div>
                <div class="pagination" id="pagination-bottom"></div>
            </div>
        </div>
    </div>

    <!-- Modal del Calendario -->
    <div class="modal" id="calendar-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>📅 Calendario de Entregas</h2>
                <button class="modal-close" onclick="closeCalendar()">&times;</button>
            </div>
            <div id="calendar-content">
                <!-- El contenido del calendario se generará dinámicamente -->
            </div>
        </div>
    </div>

    <script>
        let repairs = [];
        let editingIndex = -1;
        let filteredRepairs = [];
        let currentPage = 1;
        let itemsPerPage = 10;
        let currentImages = [];

        // Variables para modo offline
        let isOnline = navigator.onLine;

        // Cargar datos al iniciar
        window.onload = function() {
            loadData();
            loadTheme();
            displayRepairs();
            checkDeliveryReminders();
            setInterval(checkDeliveryReminders, 60000); // Revisar cada minuto
            
            // Event listeners para modo offline
            window.addEventListener('online', handleOnline);
            window.addEventListener('offline', handleOffline);
        };

        // Modo offline
        function handleOnline() {
            isOnline = true;
            document.getElementById('offline-indicator').style.display = 'none';
            showNotification('Conexión restaurada', 'success');
        }

        function handleOffline() {
            isOnline = false;
            document.getElementById('offline-indicator').style.display = 'block';
            showNotification('Trabajando sin conexión', 'info');
        }

        // Tema oscuro
        function toggleTheme() {
            const currentTheme = document.documentElement.getAttribute('data-theme');
            const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
            
            const themeButton = document.querySelector('.theme-toggle');
            themeButton.textContent = newTheme === 'dark' ? '☀️' : '🌙';
        }

        function loadTheme() {
            const savedTheme = localStorage.getItem('theme') || 'light';
            document.documentElement.setAttribute('data-theme', savedTheme);
            
            const themeButton = document.querySelector('.theme-toggle');
            themeButton.textContent = savedTheme === 'dark' ? '☀️' : '🌙';
        }

        // Manejo de imágenes
        function handleImageUpload(event) {
            const files = Array.from(event.target.files);
            
            if (currentImages.length + files.length > 5) {
                showNotification('Máximo 5 imágenes por reparación', 'error');
                return;
            }

            files.forEach(file => {
                if (file.type.startsWith('image/')) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        currentImages.push({
                            name: file.name,
                            data: e.target.result
                        });
                        displayImagePreview();
                    };
                    reader.readAsDataURL(file);
                }
            });
        }

        function displayImagePreview() {
            const preview = document.getElementById('image-preview');
            preview.innerHTML = currentImages.map((img, index) => `
                <div class="image-item">
                    <img src="${img.data}" alt="${img.name}">
                    <button class="image-remove" onclick="removeImage(${index})">&times;</button>
                </div>
            `).join('');
        }

        function removeImage(index) {
            currentImages.splice(index, 1);
            displayImagePreview();
        }

        // Manejar envío del formulario
        document.getElementById('repair-form').addEventListener('submit', function(e) {
            e.preventDefault();
            saveRepair();
        });

        function saveRepair() {
            const formData = new FormData(document.getElementById('repair-form'));
            const repair = {
                id: editingIndex >= 0 ? repairs[editingIndex].id : Date.now(),
                cliente: formData.get('cliente'),
                contacto: formData.get('contacto'),
                modelo: formData.get('modelo'),
                reparacion: formData.get('reparacion'),
                costo: parseFloat(formData.get('costo')) || 0,
                estado: formData.get('estado'),
                fechaEntrega: formData.get('fechaEntrega'),
                prioridad: formData.get('prioridad'),
                observaciones: formData.get('observaciones'),
                fecha: editingIndex >= 0 ? repairs[editingIndex].fecha : new Date().toLocaleDateString(),
                fechaCreacion: editingIndex >= 0 ? repairs[editingIndex].fechaCreacion : new Date(),
                imagenes: [...currentImages]
            };

            if (editingIndex >= 0) {
                repairs[editingIndex] = repair;
                editingIndex = -1;
                document.getElementById('form-title').textContent = 'Agregar Nueva Reparación';
                document.getElementById('btn-text').textContent = 'Guardar Reparación';
                document.getElementById('btn-cancel').style.display = 'none';
                showNotification('Reparación actualizada correctamente', 'success');
            } else {
                repairs.push(repair);
                showNotification('Reparación guardada correctamente', 'success');
            }

            currentImages = [];
            saveData();
            displayRepairs();
            document.getElementById('repair-form').reset();
            document.getElementById('image-preview').innerHTML = '';
        }

        // Filtros y búsqueda
        function filterRepairs() {
            const searchTerm = document.getElementById('search-term').value.toLowerCase();
            const statusFilter = document.getElementById('status-filter').value;

            filteredRepairs = repairs.filter(repair => {
                const matchesSearch = 
                    repair.cliente.toLowerCase().includes(searchTerm) ||
                    repair.modelo.toLowerCase().includes(searchTerm) ||
                    repair.reparacion.toLowerCase().includes(searchTerm) ||
                    (repair.contacto && repair.contacto.toLowerCase().includes(searchTerm));

                const matchesStatus = !statusFilter || repair.estado === statusFilter;

                return matchesSearch && matchesStatus;
            });

            currentPage = 1;
            sortRepairs();
        }

        // Ordenamiento
        function sortRepairs() {
            const sortBy = document.getElementById('sort-by').value;
            
            filteredRepairs.sort((a, b) => {
                switch(sortBy) {
                    case 'fecha-desc':
                        return new Date(b.fechaCreacion) - new Date(a.fechaCreacion);
                    case 'fecha-asc':
                        return new Date(a.fechaCreacion) - new Date(b.fechaCreacion);
                    case 'cliente-asc':
                        return a.cliente.localeCompare(b.cliente);
                    case 'cliente-desc':
                        return b.cliente.localeCompare(a.cliente);
                    case 'costo-desc':
                        return b.costo - a.costo;
                    case 'costo-asc':
                        return a.costo - b.costo;
                    case 'entrega-asc':
                        if (!a.fechaEntrega && !b.fechaEntrega) return 0;
                        if (!a.fechaEntrega) return 1;
                        if (!b.fechaEntrega) return -1;
                        return new Date(a.fechaEntrega) - new Date(b.fechaEntrega);
                    default:
                        return 0;
                }
            });

            displayRepairs();
        }

        // Paginación
        function updatePagination() {
            itemsPerPage = parseInt(document.getElementById('items-per-page').value);
            currentPage = 1;
            displayRepairs();
        }

        function changePage(page) {
            currentPage = page;
            displayRepairs();
        }

        function displayPagination() {
            const totalItems = filteredRepairs.length;
            const totalPages = Math.ceil(totalItems / itemsPerPage);
            
            if (totalPages <= 1) {
                document.getElementById('pagination-top').innerHTML = '';
                document.getElementById('pagination-bottom').innerHTML = '';
                return;
            }

            const paginationHTML = `
                <button onclick="changePage(1)" ${currentPage === 1 ? 'disabled' : ''}>«</button>
                <button onclick="changePage(${currentPage - 1})" ${currentPage === 1 ? 'disabled' : ''}>‹</button>
                <span>Página ${currentPage} de ${totalPages}</span>
                <button onclick="changePage(${currentPage + 1})" ${currentPage === totalPages ? 'disabled' : ''}>›</button>
                <button onclick="changePage(${totalPages})" ${currentPage === totalPages ? 'disabled' : ''}>»</button>
            `;

            document.getElementById('pagination-top').innerHTML = paginationHTML;
            document.getElementById('pagination-bottom').innerHTML = paginationHTML;
        }

        function displayRepairs() {
            // Si no hay filtros aplicados, mostrar todas las reparaciones
            if (filteredRepairs.length === 0 && repairs.length > 0) {
                filteredRepairs = [...repairs];
                sortRepairs();
                return;
            }

            const container = document.getElementById('repairs-container');
            
            if (filteredRepairs.length === 0) {
                container.innerHTML = `
                    <div class="empty-state">
                        <svg viewBox="0 0 24 24" fill="currentColor">
                            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
                        </svg>
                        <p>No se encontraron reparaciones.<br>${repairs.length === 0 ? 'Agrega tu primera reparación usando el formulario de arriba.' : 'Prueba con otros filtros de búsqueda.'}</p>
                    </div>
                `;
                displayPagination();
                return;
            }

            // Calcular items para la página actual
            const startIndex = (currentPage - 1) * itemsPerPage;
            const endIndex = startIndex + itemsPerPage;
            const pageItems = filteredRepairs.slice(startIndex, endIndex);

            container.innerHTML = pageItems.map((repair, index) => {
                const globalIndex = repairs.findIndex(r => r.id === repair.id);
                const deliveryWarning = getDeliveryWarning(repair);
                
                return `
                    <div class="repair-item">
                        <div class="repair-header">
                            <div class="repair-title">${repair.cliente} - ${repair.modelo}</div>
                            <div class="repair-cost">${repair.costo.toFixed(2)}</div>
                        </div>
                        <div class="repair-details">
                            <p><strong>Contacto:</strong> ${repair.contacto || 'No especificado'}</p>
                            <p><strong>Reparación:</strong> ${repair.reparacion}</p>
                            <p><strong>Estado:</strong> 
                                <span class="status-badge status-${repair.estado}">${repair.estado.charAt(0).toUpperCase() + repair.estado.slice(1)}</span>
                                ${deliveryWarning}
                            </p>
                            <p><strong>Prioridad:</strong> <span style="color: ${getPriorityColor(repair.prioridad)}">${repair.prioridad?.charAt(0).toUpperCase() + repair.prioridad?.slice(1) || 'Media'}</span></p>
                            <p><strong>Fecha:</strong> ${repair.fecha}</p>
                            ${repair.fechaEntrega ? `<p><strong>Entrega:</strong> ${new Date(repair.fechaEntrega).toLocaleDateString()}</p>` : ''}
                            ${repair.observaciones ? `<p><strong>Observaciones:</strong> ${repair.observaciones}</p>` : ''}
                        </div>
                        ${repair.imagenes && repair.imagenes.length > 0 ? `
                            <div class="repair-images">
                                ${repair.imagenes.map(img => `
                                    <img src="${img.data}" alt="${img.name}" onclick="showImageModal('${img.data}', '${img.name}')">
                                `).join('')}
                            </div>
                        ` : ''}
                        <div class="repair-actions">
                            <button class="btn btn-primary" onclick="editRepair(${globalIndex})">✏ Editar</button>
                            <button class="btn btn-danger" onclick="deleteRepair(${globalIndex})">🗑 Eliminar</button>
                            ${repair.estado !== 'completado' ? `<button class="btn btn-success" onclick="markCompleted(${globalIndex})">✓ Completar</button>` : ''}
                        </div>
                    </div>
                `;
            }).join('');

            displayPagination();
        }

        function getPriorityColor(prioridad) {
            switch(prioridad) {
                case 'baja': return '#28a745';
                case 'media': return '#ffc107';
                case 'alta': return '#fd7e14';
                case 'urgente': return '#dc3545';
                default: return '#6c757d';
            }
        }

        function getDeliveryWarning(repair) {
            if (!repair.fechaEntrega || repair.estado === 'completado') return '';
            
            const today = new Date();
            const deliveryDate = new Date(repair.fechaEntrega);
            const diffTime = deliveryDate - today;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

            if (diffDays < 0) {
                return '<span class="delivery-warning">⚠️ Entrega vencida</span>';
            } else if (diffDays <= 2) {
                return '<span class="delivery-warning">🔔 Entrega próxima</span>';
            }
            return '';
        }

        function markCompleted(index) {
            if (confirm('¿Marcar esta reparación como completada?')) {
                repairs[index].estado = 'completado';
                saveData();
                displayRepairs();
                showNotification('Reparación marcada como completada', 'success');
            }
        }

        // Notificaciones y recordatorios
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.textContent = message;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.style.animation = 'slideInRight 0.3s ease-out reverse';
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
        }

        function checkDeliveryReminders() {
            const today = new Date();
            const tomorrow = new Date(today);
            tomorrow.setDate(tomorrow.getDate() + 1);
            
            const upcomingDeliveries = repairs.filter(repair => {
                if (!repair.fechaEntrega || repair.estado === 'completado') return false;
                
                const deliveryDate = new Date(repair.fechaEntrega);
                return deliveryDate.toDateString() === tomorrow.toDateString();
            });

            if (upcomingDeliveries.length > 0) {
                const messages = upcomingDeliveries.map(repair => 
                    `${repair.cliente} - ${repair.modelo}`
                );
                showNotification(`Entregas mañana: ${messages.join(', ')}`, 'info');
            }
        }

        // Calendario de entregas
        function showCalendar() {
            const modal = document.getElementById('calendar-modal');
            const content = document.getElementById('calendar-content');
            
            const deliveries = repairs.filter(repair => 
                repair.fechaEntrega && repair.estado !== 'completado'
            ).sort((a, b) => new Date(a.fechaEntrega) - new Date(b.fechaEntrega));

            if (deliveries.length === 0) {
                content.innerHTML = '<p style="text-align: center; padding: 20px;">No hay entregas programadas</p>';
            } else {
                content.innerHTML = `
                    <div style="max-height: 400px; overflow-y: auto;">
                        ${deliveries.map(repair => {
                            const deliveryDate = new Date(repair.fechaEntrega);
                            const today = new Date();
                            const isOverdue = deliveryDate < today;
                            const diffDays = Math.ceil((deliveryDate - today) / (1000 * 60 * 60 * 24));
                            
                            return `
                                <div style="padding: 15px; border: 1px solid var(--border-color); border-radius: 8px; margin-bottom: 10px; ${isOverdue ? 'border-color: #dc3545; background: rgba(220, 53, 69, 0.1);' : ''}">
                                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 5px;">
                                        <strong>${repair.cliente} - ${repair.modelo}</strong>
                                        <span style="color: ${isOverdue ? '#dc3545' : (diffDays <= 2 ? '#fd7e14' : '#28a745')}; font-weight: bold;">
                                            ${deliveryDate.toLocaleDateString()}
                                        </span>
                                    </div>
                                    <p style="margin: 5px 0; font-size: 14px; opacity: 0.8;">${repair.reparacion}</p>
                                    <p style="margin: 0; font-size: 12px; color: ${isOverdue ? '#dc3545' : (diffDays <= 2 ? '#fd7e14' : '#6c757d')};">
                                        ${isOverdue ? '⚠️ Vencida' : (diffDays === 0 ? '🔔 Hoy' : (diffDays === 1 ? '🔔 Mañana' : `En ${diffDays} días`))}
                                    </p>
                                </div>
                            `;
                        }).join('')}
                    </div>
                `;
            }
            
            modal.style.display = 'block';
        }

        function closeCalendar() {
            document.getElementById('calendar-modal').style.display = 'none';
        }

        // Modal para imágenes
        function showImageModal(src, name) {
            const modal = document.createElement('div');
            modal.className = 'modal';
            modal.innerHTML = `
                <div class="modal-content" style="max-width: 90%; max-height: 90%;">
                    <div class="modal-header">
                        <h3>${name}</h3>
                        <button class="modal-close" onclick="this.parentElement.parentElement.parentElement.remove()">&times;</button>
                    </div>
                    <img src="${src}" style="width: 100%; height: auto; border-radius: 8px;">
                </div>
            `;
            modal.onclick = function(e) {
                if (e.target === modal) {
                    modal.remove();
                }
            };
            document.body.appendChild(modal);
        }

        function editRepair(index) {
            const repair = repairs[index];
            editingIndex = index;
            currentImages = repair.imagenes ? [...repair.imagenes] : [];
            
            document.getElementById('cliente').value = repair.cliente;
            document.getElementById('contacto').value = repair.contacto || '';
            document.getElementById('modelo').value = repair.modelo;
            document.getElementById('reparacion').value = repair.reparacion;
            document.getElementById('costo').value = repair.costo;
            document.getElementById('estado').value = repair.estado;
            document.getElementById('fechaEntrega').value = repair.fechaEntrega || '';
            document.getElementById('prioridad').value = repair.prioridad || 'media';
            document.getElementById('observaciones').value = repair.observaciones || '';
            
            displayImagePreview();
            
            document.getElementById('form-title').textContent = 'Editar Reparación';
            document.getElementById('btn-text').textContent = 'Actualizar Reparación';
            document.getElementById('btn-cancel').style.display = 'inline-block';
            
            document.querySelector('.form-section').scrollIntoView({ behavior: 'smooth' });
        }

        function cancelEdit() {
            editingIndex = -1;
            currentImages = [];
            document.getElementById('form-title').textContent = 'Agregar Nueva Reparación';
            document.getElementById('btn-text').textContent = 'Guardar Reparación';
            document.getElementById('btn-cancel').style.display = 'none';
            document.getElementById('repair-form').reset();
            document.getElementById('image-preview').innerHTML = '';
        }

        function deleteRepair(index) {
            if (confirm('¿Estás seguro de que quieres eliminar esta reparación?')) {
                repairs.splice(index, 1);
                saveData();
                filterRepairs(); // Actualizar filtros después de eliminar
                showNotification('Reparación eliminada correctamente', 'success');
            }
        }

        function saveData() {
            try {
                const data = JSON.stringify(repairs);
                window.repairData = data;
                
                // Si está online, intentar guardar en localStorage también
                if (isOnline) {
                    try {
                        localStorage.setItem('repairData', data);
                    } catch (e) {
                        // Error de localStorage, continuar con memoria
                    }
                }
            } catch (error) {
                showNotification('Error al guardar los datos', 'error');
            }
        }

        function loadData() {
            try {
                // Intentar cargar desde localStorage primero
                let data = null;
                try {
                    data = localStorage.getItem('repairData');
                } catch (e) {
                    // Error de localStorage, usar memoria
                }
                
                if (!data && window.repairData) {
                    data = window.repairData;
                }
                
                if (data) {
                    repairs = JSON.parse(data);
                    // Convertir fechaCreacion a objeto Date si es string
                    repairs.forEach(repair => {
                        if (typeof repair.fechaCreacion === 'string') {
                            repair.fechaCreacion = new Date(repair.fechaCreacion);
                        }
                        if (!repair.fechaCreacion) {
                            repair.fechaCreacion = new Date();
                        }
                    });
                } else {
                    repairs = [];
                }
                
                filteredRepairs = [...repairs];
            } catch (error) {
                repairs = [];
                filteredRepairs = [];
                showNotification('Error al cargar los datos', 'error');
            }
        }

        function exportData() {
            if (repairs.length === 0) {
                showNotification('No hay datos para exportar', 'error');
                return;
            }
            
            const data = JSON.stringify(repairs, null, 2);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `reparaciones_backup_${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showNotification('Copia de seguridad descargada correctamente', 'success');
        }

        function importData() {
            document.getElementById('file-input').click();
        }

        function handleFileImport(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    if (Array.isArray(importedData)) {
                        if (confirm('¿Quieres reemplazar todos los datos actuales con los datos importados?')) {
                            repairs = importedData;
                            // Asegurar que todas las reparaciones tengan fechaCreacion
                            repairs.forEach(repair => {
                                if (!repair.fechaCreacion) {
                                    repair.fechaCreacion = new Date();
                                }
                            });
                            saveData();
                            filterRepairs();
                            showNotification('Datos importados correctamente', 'success');
                        }
                    } else {
                        showNotification('El archivo no tiene el formato correcto', 'error');
                    }
                } catch (error) {
                    showNotification('Error al leer el archivo. Asegúrate de que sea un archivo JSON válido.', 'error');
                }
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        function clearAllData() {
            if (confirm('¿Estás seguro de que quieres borrar todas las reparaciones? Esta acción no se puede deshacer.')) {
                repairs = [];
                filteredRepairs = [];
                currentImages = [];
                saveData();
                displayRepairs();
                showNotification('Todos los datos han sido eliminados', 'success');
            }
        }

        // Cerrar modal al hacer clic fuera
        window.onclick = function(event) {
            const modal = document.getElementById('calendar-modal');
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        };

        // Inicializar filtros al cargar
        window.addEventListener('load', function() {
            setTimeout(filterRepairs, 100);
        });
    </script>
</body>
</html>
