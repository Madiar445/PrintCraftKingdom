<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrintCraft Kingdom - 3D фигурки на заказ</title>
    <link rel="icon" type="image/x-icon" href="/static/favicon.ico">
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#1E3A8A',
                        secondary: '#DC2626',
                        dark: '#111827',
                        light: '#F3F4F6'
                    }
                }
            }
        }
    </script>
    <script src="https://cdn.jsdelivr.net/npm/feather-icons/dist/feather.min.js"></script>
    <script src="https://accounts.google.com/gsi/client" async defer></script>
    <style>
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        .admin-panel {
            display: none;
        }
        @media (max-width: 768px) {
            header nav ul {
                flex-direction: column;
                gap: 1rem;
                position: fixed;
                top: 0;
                right: -100%;
                width: 70%;
                height: 100vh;
                background: #111827;
                padding-top: 5rem;
                transition: 0.3s;
                z-index: 10;
            }
            header nav ul.show {
                right: 0;
            }
            #mobile-menu-btn {
                display: block;
                z-index: 11;
            }
            .hero {
                padding: 2rem 1rem;
                text-align: center;
            }
            .hero h2 {
                font-size: 2rem;
            }
            #products .grid {
                grid-template-columns: 1fr;
            }
            #contact .grid {
                grid-template-columns: 1fr;
            }
            footer .flex {
                flex-direction: column;
                text-align: center;
            }
            #admin-notes {
                width: 90%;
                right: 5%;
            }
        }
        @media (min-width: 769px) {
            #mobile-menu-btn {
                display: none;
            }
        }
        #mobile-menu-btn {
            display: none;
            background: transparent;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
        }
    </style>
</head>
<body class="bg-light text-dark">
    <header class="bg-dark text-white py-4">
        <div class="container mx-auto px-4 flex justify-between items-center">
            <h1 class="text-2xl font-bold text-red-500">PrintCraft <span class="text-blue-600">Kingdom</span></h1>
            <button id="mobile-menu-btn">
                <i data-feather="menu"></i>
            </button>
            <nav>
                <ul class="flex space-x-6" id="main-menu">
<li><a href="#" class="hover:text-red-500">Главная</a></li>
                    <li><a href="#products" class="hover:text-red-500">Каталог</a></li>
                    <li><a href="#reviews" class="hover:text-red-500">Отзывы</a></li>
                    <li><a href="#contact" class="hover:text-red-500">Контакты</a></li>
                <li id="login-button" class="hover:text-red-500 cursor-pointer flex items-center">
                    <i data-feather="user" class="mr-1"></i> Войти
                </li>
</ul>
            </nav>
        </div>
    </header>

    <main class="container mx-auto px-4 py-8">
        <section class="hero bg-blue-600 text-white rounded-lg p-8 mb-8">
            <h2 class="text-4xl font-bold mb-4">Уникальные 3D фигурки на заказ</h2>
            <p class="text-xl mb-6">Высококачественная печать персонажей, статуэток и декора</p>
            <a href="#products" class="bg-red-500 hover:bg-red-600 text-white px-6 py-3 rounded-lg font-bold">Посмотреть каталог</a>
        </section>

        <section id="products" class="mb-12">
            <h2 class="text-3xl font-bold mb-6 text-center">Наши работы</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Пример товара -->
                <div class="product-card bg-white rounded-lg overflow-hidden shadow-lg transition duration-300">
                    <img src="http://static.photos/technology/640x360/1" alt="3D фигурка" class="w-full h-64 object-cover">
                    <div class="p-4">
                        <h3 class="text-xl font-bold mb-2">Имя фигурки</h3>
                        <p class="text-gray-600 mb-4">Описание фигурки</p>
                        <div class="flex justify-between items-center">
                            <span class="text-lg font-bold text-red-500">999₽</span>
                            <button class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded">В корзину</button>
                        </div>
                    </div>
                </div>
                <!-- Конец примера -->
            </div>
            
            <!-- Кнопка для добавления товара (видна только админу) -->
            <div id="add-product-btn" class="mt-6 text-center hidden">
                <button onclick="showAdminPanel()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-3 rounded-lg font-bold">
                    Добавить товар
                </button>
            </div>
            
            <!-- Админ панель -->
            <div id="admin-panel" class="admin-panel mt-8 bg-white p-6 rounded-lg shadow">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-2xl font-bold">Управление товарами</h3>
                    <button onclick="toggleAdminMode()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded">
                        Переключить режим
                    </button>
                </div>

                <div id="add-product-section">
                    <h4 class="text-xl font-bold mb-4">Добавить новый товар</h4>
                    <form id="product-form">
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Название</label>
                            <input type="text" id="product-name" class="w-full p-2 border rounded" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Описание</label>
                            <textarea id="product-desc" class="w-full p-2 border rounded" rows="3" required></textarea>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Цена (₽)</label>
                            <input type="number" id="product-price" class="w-full p-2 border rounded" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Изображение</label>
                            <input type="file" id="product-image" class="w-full p-2 border rounded" accept="image/*" required>
                        </div>
                        <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded font-bold">
                            Сохранить товар
                        </button>
                    </form>
                </div>

                <div id="edit-products-section" class="mt-8 hidden">
                    <h4 class="text-xl font-bold mb-4">Редактировать товары</h4>
                    <div id="products-list" class="space-y-4">
                        <!-- Товары будут загружаться здесь -->
                    </div>
                </div>
            </div>
        </section>

        <section id="reviews" class="mb-12">
            <h2 class="text-3xl font-bold mb-6 text-center">Отзывы покупателей</h2>
            <div class="bg-white rounded-lg shadow p-6">
                <div id="reviews-container">
                    <!-- Отзывы будут загружаться здесь -->
                </div>
                <div id="review-form" class="mt-6 hidden">
                    <h3 class="text-xl font-bold mb-4">Оставить отзыв</h3>
                    <form>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Ваше имя</label>
                            <input type="text" id="review-name" class="w-full p-2 border rounded" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Ваш отзыв</label>
                            <textarea id="review-text" class="w-full p-2 border rounded" rows="3" required></textarea>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 mb-2">Оценка</label>
                            <select id="review-rating" class="w-full p-2 border rounded" required>
                                <option value="5">5 ★</option>
                                <option value="4">4 ★</option>
                                <option value="3">3 ★</option>
                                <option value="2">2 ★</option>
                                <option value="1">1 ★</option>
                            </select>
                        </div>
                        <button type="submit" class="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded font-bold">
                            Отправить отзыв
                        </button>
                    </form>
                </div>
                <button id="write-review-btn" class="mt-4 bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded font-bold">
                    Написать отзыв
                </button>
            </div>
        </section>

        <section id="contact" class="mb-12">
            <h2 class="text-3xl font-bold mb-6 text-center">Связаться с нами</h2>
            <div class="bg-white rounded-lg shadow p-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-xl font-bold mb-4">Контактная информация</h3>
                        <p class="mb-2"><i data-feather="mail" class="inline mr-2"></i> PrintCraftKingdom@mail.ru</p>
                        <p class="mb-2"><i data-feather="phone" class="inline mr-2"></i> +7 (908) 114-60-57</p>
                        <p><i data-feather="map-pin" class="inline mr-2"></i> Россия, г. Омск</p>
                    </div>
                    <div>
                        <h3 class="text-xl font-bold mb-4">Написать сообщение</h3>
                        <form>
                            <div class="mb-4">
                                <label class="block text-gray-700 mb-2">Ваше имя</label>
                                <input type="text" class="w-full p-2 border rounded" required>
                            </div>
                            <div class="mb-4">
                                <label class="block text-gray-700 mb-2">Email</label>
                                <input type="email" class="w-full p-2 border rounded" required>
                            </div>
                            <div class="mb-4">
                                <label class="block text-gray-700 mb-2">Сообщение</label>
                                <textarea class="w-full p-2 border rounded" rows="3" required></textarea>
                            </div>
                            <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded font-bold">
                                Отправить
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-dark text-white py-6">
        <div class="container mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="mb-4 md:mb-0">
                    <h2 class="text-2xl font-bold text-red-500">PrintCraft <span class="text-blue-600">Kingdom</span></h2>
                    <p>© 2023 Все права защищены</p>
                </div>
                <div class="flex space-x-4">
                    <a href="#" class="hover:text-red-500"><i data-feather="instagram"></i></a>
                    <a href="#" class="hover:text-red-500"><i data-feather="facebook"></i></a>
                    <a href="#" class="hover:text-red-500"><i data-feather="twitter"></i></a>
                </div>
            </div>
        </div>
    </footer>

    <!-- Google Auth -->
    <div id="g_id_onload"
         data-client_id="YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com"
         data-login_uri="https://yourdomain.com/login"
         data-auto_prompt="false">
    </div>
    <div class="g_id_signin"
         data-type="standard"
         data-size="large"
         data-theme="dark"
         data-text="sign_in_with"
         data-shape="rectangular"
         data-logo_alignment="left">
    </div>

    <!-- Заметки для администратора -->
    <div id="admin-notes" class="fixed bottom-4 right-4 bg-white p-4 rounded-lg shadow-lg hidden">
        <h3 class="font-bold mb-2">Доступ к админ панели:</h3>
        <ol class="list-decimal pl-5">
            <li>Нажмите кнопку "Войти" в шапке сайта</li>
            <li>Выберите аккаунт Google с правами администратора</li>
            <li>После авторизации появится кнопка "Добавить товар"</li>
            <li>Нажмите её для открытия панели управления</li>
        </ol>
        <button onclick="hideAdminNotes()" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">
            Закрыть
        </button>
    </div>

    <script>
        // Мобильное меню
        document.getElementById('mobile-menu-btn').addEventListener('click', function() {
            document.getElementById('main-menu').classList.toggle('show');
        });

        // Закрытие меню при клике на ссылку
        document.querySelectorAll('#main-menu a').forEach(link => {
            link.addEventListener('click', function() {
                document.getElementById('main-menu').classList.remove('show');
            });
        });

        // Показать заметки администратора
        function showAdminNotes() {
            document.getElementById('admin-notes').classList.remove('hidden');
        }

        // Скрыть заметки администратора
        function hideAdminNotes() {
            document.getElementById('admin-notes').classList.add('hidden');
        }

        // Инициализация иконок
        feather.replace();

        // Адаптация формы товара для мобильных
        if (window.innerWidth < 768) {
            document.getElementById('product-form').classList.add('space-y-4');
            document.querySelectorAll('#product-form input, #product-form textarea, #product-form select').forEach(el => {
                el.classList.add('text-base', 'py-3');
            });
        }
// Обработчик для кнопки отзыва
        document.getElementById('write-review-btn').addEventListener('click', function() {
            document.getElementById('review-form').classList.toggle('hidden');
        });
        
        // Функция показа админ панели
        function showAdminPanel() {
            document.getElementById('admin-panel').classList.toggle('hidden');
            loadProductsForEdit();
        }

        // Переключение между режимами добавления и редактирования
        function toggleAdminMode() {
            document.getElementById('add-product-section').classList.toggle('hidden');
            document.getElementById('edit-products-section').classList.toggle('hidden');
        }

        // Загрузка товаров для редактирования
        function loadProductsForEdit() {
            const products = [
                {id: 1, name: "Имя фигурки", description: "Описание фигурки", price: 999, image: "http://static.photos/technology/640x360/1"}
            ];
            
            let html = '';
            products.forEach(product => {
                html += `
                <div class="bg-gray-50 p-4 rounded-lg">
                    <div class="flex items-start space-x-4">
                        <img src="${product.image}" alt="${product.name}" class="w-24 h-24 object-cover rounded">
                        <div class="flex-1">
                            <h5 class="font-bold">${product.name}</h5>
                            <p class="text-sm text-gray-600 mb-2">${product.description}</p>
                            <p class="text-red-500 font-bold">${product.price}₽</p>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="editProduct(${product.id})" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">
                                <i data-feather="edit-2" class="w-4 h-4"></i>
                            </button>
                            <button onclick="deleteProduct(${product.id})" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">
                                <i data-feather="trash-2" class="w-4 h-4"></i>
                            </button>
                        </div>
                    </div>
                </div>
                `;
            });
            
            document.getElementById('products-list').innerHTML = html;
            feather.replace();
        }

        // Редактирование товара
        function editProduct(id) {
            // В реальном приложении здесь будет запрос к серверу
            alert(`Редактирование товара с ID: ${id}`);
        }

        // Удаление товара
        function deleteProduct(id) {
            if(confirm('Вы уверены, что хотите удалить этот товар?')) {
                // В реальном приложении здесь будет запрос к серверу
                alert(`Товар с ID: ${id} удален`);
                loadProductsForEdit();
            }
        }
        
        // Показать заметки при нажатии Ctrl+Alt+A
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey && e.altKey && e.key === 'a') {
                showAdminNotes();
            }
        });

        // Проверка авторизации Google (заглушка)
        function handleCredentialResponse(response) {
            console.log("Google auth response:", response);
            // Проверка, является ли пользователь администратором
            if (response.credential) {
                const adminEmails = ["admin@printcraftkingdom.ru", "your-email@gmail.com"];
                const payload = JSON.parse(atob(response.credential.split('.')[1]));
                
                if (payload.email === "PrintCraftKingdom@mail.ru") {
                    // Показать кнопку админа
                    document.getElementById('add-product-btn').classList.remove('hidden');
                    document.getElementById('login-button').textContent = "Выйти";
                }
            }
        }
        }
        
        // Назначаем обработчик для кнопки входа
        document.getElementById('login-button').addEventListener('click', function() {
            if(this.textContent === "Выйти") {
                // Выход
                google.accounts.id.disableAutoSelect();
                this.textContent = "Войти";
                document.getElementById('add-product-btn').classList.add('hidden');
                document.getElementById('admin-panel').classList.add('hidden');
            } else {
                // Показать Google Sign-In
                google.accounts.id.prompt();
            }
        });
        
        // Загрузка отзывов (заглушка)
        function loadReviews() {
            const reviews = [
                {name: "Иван", text: "Отличное качество печати! Фигурка точно соответствует описанию.", rating: 5},
                {name: "Анна", text: "Быстрая доставка, приятные цены. Рекомендую!", rating: 4},
                {name: "Дмитрий", text: "Заказывал персонажа для подарка - остался доволен.", rating: 5}
            ];
            
            let html = '';
            reviews.forEach(review => {
                html += `
                <div class="mb-6 pb-6 border-b">
                    <div class="flex justify-between items-center mb-2">
                        <h4 class="font-bold">${review.name}</h4>
                        <div>${'★'.repeat(review.rating)}${'☆'.repeat(5 - review.rating)}</div>
                    </div>
                    <p>${review.text}</p>
                </div>
                `;
            });
            
            document.getElementById('reviews-container').innerHTML = html;
        }
        
        // Загрузка отзывов при загрузке страницы
        window.onload = function() {
            loadReviews();
            
            // Инициализация Google Sign-In
            google.accounts.id.initialize({
                client_id: "YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com",
                callback: handleCredentialResponse,
                ux_mode: "popup" // Изменено для мобильных
            });

            // Адаптация кнопки Google Sign-In для мобильных
            if (window.innerWidth < 768) {
                document.querySelector('.g_id_signin').setAttribute('data-size', 'medium');
            }
        };

        // Обработчик изменения размера окна
        window.addEventListener('resize', function() {
            if (window.innerWidth >= 768) {
                document.getElementById('main-menu').classList.remove('show');
            }
        });
// Обработчик формы товара
        document.getElementById('product-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const name = document.getElementById('product-name').value;
            const desc = document.getElementById('product-desc').value;
            const price = document.getElementById('product-price').value;
            
            alert(`Товар "${name}" добавлен!\nОписание: ${desc}\nЦена: ${price}₽`);
            this.reset();
            loadProductsForEdit();
            document.getElementById('add-product-section').classList.add('hidden');
            document.getElementById('edit-products-section').classList.remove('hidden');
        });
    </script>
</body>
</html>
