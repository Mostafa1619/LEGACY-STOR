<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mo2men Store - إكسسوارات الأيفون الفاخرة</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Google Font Cairo -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: 'Cairo', sans-serif; }
        .glass { background: rgba(17, 24, 39, 0.75); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .glass-card { background: rgba(31, 41, 55, 0.6); backdrop-filter: blur(8px); border: 1px solid rgba(255, 255, 255, 0.05); }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col selection:bg-amber-500 selection:text-black">

    <!-- Header -->
    <header class="sticky top-0 z-50 glass border-b border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-3 space-x-reverse cursor-pointer" onclick="switchTab('shop')">
                <div class="w-11 h-11 rounded-xl bg-gradient-to-tr from-amber-500 to-yellow-300 flex items-center justify-center text-slate-950 font-black text-xl shadow-lg shadow-amber-500/20">
                    M
                </div>
                <div>
                    <span class="text-xl font-black tracking-wider bg-gradient-to-r from-white via-slate-200 to-amber-400 bg-clip-text text-transparent">MO2MEN STORE</span>
                    <span class="block text-[10px] text-amber-400 font-semibold tracking-widest uppercase">iPhone Accessories</span>
                </div>
            </div>

            <div class="flex items-center gap-3">
                <button onclick="openCart()" class="relative p-2.5 rounded-xl bg-slate-900 border border-slate-800 hover:border-amber-500/50 transition text-slate-300 hover:text-white">
                    <i class="fa-solid fa-bag-shopping text-lg"></i>
                    <span id="cart-badge" class="absolute -top-1.5 -right-1.5 bg-amber-500 text-slate-950 text-xs font-bold w-5 h-5 rounded-full flex items-center justify-center hidden">0</span>
                </button>
                <button onclick="checkAdminAccess()" class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-800 hover:border-amber-500/50 text-slate-300 hover:text-white text-sm font-bold transition">
                    <i class="fa-solid fa-lock text-amber-400"></i>
                    <span class="hidden sm:inline">لوحة التحكم</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 w-full">
        
        <!-- Shop View -->
        <div id="view-shop" class="space-y-8">
            <!-- Hero Banner -->
            <div class="relative overflow-hidden rounded-3xl glass border border-amber-500/20 p-8 sm:p-12 text-center sm:text-right flex flex-col sm:flex-row items-center justify-between gap-8 bg-gradient-to-r from-slate-900 via-slate-900 to-amber-950/30">
                <div class="space-y-4 max-w-xl">
                    <span class="inline-block px-3 py-1 rounded-full bg-amber-500/10 border border-amber-500/20 text-amber-400 text-xs font-bold tracking-wider uppercase">أحدث إصدارات الأيفون</span>
                    <h1 class="text-3xl sm:text-5xl font-black text-white leading-tight">فخامة الحماية والأناقة لجهازك</h1>
                    <p class="text-slate-400 text-sm sm:text-base">تشكيلة حصرية من أغطية الحماية الأصلية، حمايات الشاشة النانو، والشواحن السريعة المصممة خصيصاً لهواتف الأيفون.</p>
                </div>
                <div class="w-32 h-32 sm:w-48 sm:h-48 rounded-2xl bg-gradient-to-br from-amber-500/20 to-transparent border border-amber-500/30 flex items-center justify-center shrink-0">
                    <i class="fa-brands fa-apple text-6xl sm:text-8xl text-amber-400 animate-pulse"></i>
                </div>
            </div>

            <!-- Filters -->
            <div class="flex items-center justify-between flex-wrap gap-4 border-b border-slate-800 pb-4">
                <h2 class="text-xl font-bold text-white flex items-center gap-2">
                    <i class="fa-solid fa-fire text-amber-400"></i> المنتجات المتوفرة
                </h2>
                <div class="flex gap-2 overflow-x-auto w-full sm:w-auto pb-2 sm:pb-0" id="categories-filter">
                    <button onclick="filterCategory('all')" class="cat-btn px-4 py-2 rounded-xl text-xs font-bold bg-amber-500 text-slate-950 transition">الكل</button>
                    <button onclick="filterCategory('كفرات')" class="cat-btn px-4 py-2 rounded-xl text-xs font-bold bg-slate-900 text-slate-400 hover:text-white transition">كفرات وحافظات</button>
                    <button onclick="filterCategory('شاشات')" class="cat-btn px-4 py-2 rounded-xl text-xs font-bold bg-slate-900 text-slate-400 hover:text-white transition">حماية شاشة</button>
                    <button onclick="filterCategory('شواحن')" class="cat-btn px-4 py-2 rounded-xl text-xs font-bold bg-slate-900 text-slate-400 hover:text-white transition">شواحن وإكسسوارات</button>
                </div>
            </div>

            <!-- Products Grid -->
            <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Dynamically Rendered -->
            </div>
        </div>

        <!-- Admin View -->
        <div id="view-admin" class="hidden space-y-8">
            <div class="flex items-center justify-between flex-wrap gap-4 bg-slate-900/60 p-6 rounded-3xl border border-slate-800">
                <div>
                    <h2 class="text-2xl font-black text-white">لوحة تحكم الأدمن (Mo2men)</h2>
                    <p class="text-slate-400 text-sm">إدارة الأسعار، تفعيل حالة النفاذ (Sold Out)، وإضافة المنتجات.</p>
                </div>
                <div class="flex items-center gap-3">
                    <button onclick="openAddModal()" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm transition flex items-center gap-2 shadow-lg shadow-amber-500/20">
                        <i class="fa-solid fa-plus"></i> إضافة منتج جديد
                    </button>
                    <button onclick="switchTab('shop')" class="px-5 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-white font-bold text-sm transition">
                        <i class="fa-solid fa-store ml-2"></i> العودة للمتجر
                    </button>
                </div>
            </div>

            <!-- Admin Products Table -->
            <div class="glass rounded-3xl overflow-hidden border border-slate-800">
                <div class="overflow-x-auto">
                    <table class="w-full text-right border-collapse">
                        <thead>
                            <tr class="border-b border-slate-800 text-slate-400 text-xs uppercase bg-slate-900/80">
                                <th class="p-4">المنتج</th>
                                <th class="p-4">القسم</th>
                                <th class="p-4">السعر (ج.م)</th>
                                <th class="p-4">الحالة</th>
                                <th class="p-4 text-center">الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="admin-products-table" class="divide-y divide-slate-800/60 text-sm">
                            <!-- Dynamically Rendered -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- Cart Modal -->
    <div id="cart-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="glass w-full max-w-lg rounded-3xl p-6 space-y-6 border border-slate-800 shadow-2xl animate-in fade-in zoom-in duration-200">
            <div class="flex items-center justify-between border-b border-slate-800 pb-4">
                <h3 class="text-lg font-black text-white flex items-center gap-2">
                    <i class="fa-solid fa-bag-shopping text-amber-400"></i> سلة المشتريات
                </h3>
                <button onclick="closeCart()" class="text-slate-400 hover:text-white p-2">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            
            <div id="cart-items-container" class="space-y-3 max-h-72 overflow-y-auto pr-1">
                <!-- Cart Items -->
            </div>

            <div class="border-t border-slate-800 pt-4 space-y-4">
                <div class="flex items-center justify-between font-bold text-base">
                    <span class="text-slate-400">الإجمالي الكلي:</span>
                    <span id="cart-total" class="text-amber-400 text-xl">0 ج.م</span>
                </div>
                <button onclick="checkoutWhatsApp()" class="w-full py-3.5 rounded-2xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold transition flex items-center justify-center gap-2 shadow-lg shadow-emerald-600/20">
                    <i class="fa-brands fa-whatsapp text-xl"></i> إتمام الطلب عبر الواتساب
                </button>
            </div>
        </div>
    </div>

    <!-- Add/Edit Product Modal -->
    <div id="product-modal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="glass w-full max-w-md rounded-3xl p-6 space-y-6 border border-slate-800 shadow-2xl">
            <div class="flex items-center justify-between border-b border-slate-800 pb-4">
                <h3 id="modal-title" class="text-lg font-black text-white">إضافة منتج جديد</h3>
                <button onclick="closeProductModal()" class="text-slate-400 hover:text-white p-2"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <form id="product-form" onsubmit="saveProduct(event)" class="space-y-4">
                <input type="hidden" id="product-id">
                <div>
                    <label class="block text-xs font-bold text-slate-400 mb-1">اسم المنتج</label>
                    <input type="text" id="p-name" required class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-3 text-white text-sm focus:border-amber-500 focus:outline-none">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 mb-1">السعر (ج.م)</label>
                        <input type="number" id="p-price" required class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-3 text-white text-sm focus:border-amber-500 focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 mb-1">القسم</label>
                        <select id="p-category" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-3 text-white text-sm focus:border-amber-500 focus:outline-none">
                            <option value="كفرات">كفرات وحافظات</option>
                            <option value="شاشات">حماية شاشة</option>
                            <option value="شواحن">شواحن وإكسسوارات</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-400 mb-1">رابط الصورة (URL)</label>
                    <input type="url" id="p-image" required placeholder="https://images.unsplash.com/..." class="w-full bg-slate-900 border border-slate-800 rounded-xl px-4 py-3 text-white text-sm focus:border-amber-500 focus:outline-none">
                </div>
                <div class="flex items-center gap-2 pt-2">
                    <input type="checkbox" id="p-sold" class="w-4 h-4 accent-amber-500 rounded">
                    <label for="p-sold" class="text-sm font-semibold text-slate-300">المنتج نفذ (Sold Out)</label>
                </div>
                <button type="submit" class="w-full py-3.5 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold transition shadow-lg shadow-amber-500/20">حفظ المنتج</button>
            </form>
        </div>
    </div>

    <!-- Footer -->
    <footer class="border-t border-slate-900 py-6 text-center text-xs text-slate-500">
        جميع الحقوق محفوظة © 2026 - <span class="text-amber-400 font-bold">Mo2men Store</span>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        // Initial Default Products Data
        const defaultProducts = [
            { id: 1, name: 'كفر سيليكون فاخر ماجسيف - أيفون 15 برو', price: 350, category: 'كفرات', image: 'https://images.unsplash.com/photo-1601784551446-20c9e07cdbdb?auto=format&fit=crop&q=80&w=600', soldOut: false },
            { id: 2, name: 'استيكر زجاجي نانو حماية كاملة - أيفون 14', price: 200, category: 'شاشات', image: 'https://images.unsplash.com/photo-1585060544812-6b45742d762f?auto=format&fit=crop&q=80&w=600', soldOut: false },
            { id: 3, name: 'شاحن سريـع نوع C قوة 20 واط أصلي', price: 450, category: 'شواحن', image: 'https://images.unsplash.com/photo-1583863788434-e58a36330cf0?auto=format&fit=crop&q=80&w=600', soldOut: true },
            { id: 4, name: 'كفر شفاف مقاوم للصدمات - أيفون 13', price: 250, category: 'كفرات', image: 'https://images.unsplash.com/photo-1541872703-74c5e44368f9?auto=format&fit=crop&q=80&w=600', soldOut: false }
        ];

        let products = JSON.parse(localStorage.getItem('mo2men_products')) || defaultProducts;
        let cart = JSON.parse(localStorage.getItem('mo2men_cart')) || [];
        let currentFilter = 'all';

        function saveData() {
            localStorage.setItem('mo2men_products', JSON.stringify(products));
            localStorage.setItem('mo2men_cart', JSON.stringify(cart));
            renderProducts();
            renderAdminTable();
            updateCartBadge();
        }

        function checkAdminAccess() {
            const pass = prompt("أدخل كلمة مرور لوحة التحكم (الافتراضية: mo2men 0000):");
            if (pass === "mo2men 0000") {
                switchTab('admin');
            } else if (pass !== null) {
                alert("كلمة المرور غير صحيحة!");
            }
        }

        function switchTab(tab) {
            document.getElementById('view-shop').classList.add('hidden');
            document.getElementById('view-admin').classList.add('hidden');
            if(tab === 'shop') {
                document.getElementById('view-shop').classList.remove('hidden');
                renderProducts();
            } else if(tab === 'admin') {
                document.getElementById('view-admin').classList.remove('hidden');
                renderAdminTable();
            }
            window.scrollTo({top: 0, behavior: 'smooth'});
        }

        function filterCategory(cat) {
            currentFilter = cat;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                btn.classList.remove('bg-amber-500', 'text-slate-950');
                btn.classList.add('bg-slate-900', 'text-slate-400');
            });
            event.target.classList.remove('bg-slate-900', 'text-slate-400');
            event.target.classList.add('bg-amber-500', 'text-slate-950');
            renderProducts();
        }

        function renderProducts() {
            const grid = document.getElementById('products-grid');
            grid.innerHTML = '';
            
            const filtered = currentFilter === 'all' ? products : products.filter(p => p.category === currentFilter);

            if(filtered.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center py-12 text-slate-500">لا توجد منتجات متاحة في هذا القسم حالياً.</div>`;
                return;
            }

            filtered.forEach(p => {
                grid.innerHTML += `
                    <div class="glass-card rounded-3xl overflow-hidden border border-slate-800/80 group hover:border-amber-500/40 transition duration-300 flex flex-col justify-between">
                        <div class="relative h-60 overflow-hidden bg-slate-900">
                            <img src="${p.image}" alt="${p.name}" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                            ${p.soldOut ? '<div class="absolute inset-0 bg-slate-950/70 backdrop-blur-xs flex items-center justify-center"><span class="px-4 py-1.5 rounded-full bg-red-600 text-white font-black text-xs tracking-wider uppercase shadow-xl">نفذت الكمية (Sold Out)</span></div>' : ''}
                            <span class="absolute top-3 right-3 px-3 py-1 rounded-xl bg-slate-950/70 backdrop-blur-md text-amber-400 text-xs font-bold border border-slate-800">${p.category}</span>
                        </div>
                        <div class="p-5 space-y-4 flex flex-col justify-between flex-grow">
                            <div>
                                <h3 class="font-bold text-white text-base group-hover:text-amber-400 transition">${p.name}</h3>
                                <div class="mt-2 text-xl font-black text-amber-400">${p.price} <span class="text-xs font-normal text-slate-400">ج.م</span></div>
                            </div>
                            <button onclick="addToCart(${p.id})" ${p.soldOut ? 'disabled' : ''} class="w-full py-3 rounded-xl font-bold text-xs transition ${p.soldOut ? 'bg-slate-900 text-slate-600 cursor-not-allowed border border-slate-800' : 'bg-slate-900 hover:bg-amber-500 text-white hover:text-slate-950 border border-slate-800 hover:border-amber-500 shadow-sm'}">
                                ${p.soldOut ? 'غير متوفر حالياً' : 'إضافة إلى السلة'}
                            </button>
                        </div>
                    </div>
                `;
            });
        }

        function renderAdminTable() {
            const tbody = document.getElementById('admin-products-table');
            tbody.innerHTML = '';
            products.forEach(p => {
                tbody.innerHTML += `
                    <tr class="hover:bg-slate-900/40 transition">
                        <td class="p-4 flex items-center gap-3">
                            <img src="${p.image}" class="w-10 h-10 rounded-lg object-cover bg-slate-900 shrink-0">
                            <span class="font-bold text-white">${p.name}</span>
                        </td>
                        <td class="p-4 text-slate-400">${p.category}</td>
                        <td class="p-4">
                            <input type="number" value="${p.price}" onchange="quickUpdatePrice(${p.id}, this.value)" class="w-24 bg-slate-900 border border-slate-800 rounded-lg px-2.5 py-1 text-white font-bold text-sm focus:border-amber-500 focus:outline-none">
                        </td>
                        <td class="p-4">
                            <button onclick="toggleSoldOut(${p.id})" class="px-3 py-1 rounded-full text-xs font-bold transition ${p.soldOut ? 'bg-red-500/10 text-red-500 border border-red-500/20' : 'bg-emerald-500/10 text-emerald-400 border border-emerald-500/20'}">
                                ${p.soldOut ? 'Sold Out' : 'متوفر'}
                            </button>
                        </td>
                        <td class="p-4 text-center space-x-2 space-x-reverse">
                            <button onclick="openEditModal(${p.id})" class="p-2 rounded-lg bg-slate-900 hover:bg-slate-800 text-amber-400 transition" title="تعديل"><i class="fa-solid fa-pen"></i></button>
                            <button onclick="deleteProduct(${p.id})" class="p-2 rounded-lg bg-slate-900 hover:bg-slate-800 text-red-400 transition" title="حذف"><i class="fa-solid fa-trash"></i></button>
                        </td>
                    </tr>
                `;
            });
        }

        function quickUpdatePrice(id, newPrice) {
            const p = products.find(item => item.id === id);
            if(p) {
                p.price = Number(newPrice);
                saveData();
            }
        }

        function toggleSoldOut(id) {
            const p = products.find(item => item.id === id);
            if(p) {
                p.soldOut = !p.soldOut;
                saveData();
            }
        }

        function deleteProduct(id) {
            if(confirm('هل أنت متأكد من حذف هذا المنتج؟')) {
                products = products.filter(item => item.id !== id);
                saveData();
            }
        }

        function openAddModal() {
            document.getElementById('modal-title').innerText = 'إضافة منتج جديد';
            document.getElementById('product-id').value = '';
            document.getElementById('p-name').value = '';
            document.getElementById('p-price').value = '';
            document.getElementById('p-image').value = '';
            document.getElementById('p-sold').checked = false;
            document.getElementById('product-modal').classList.remove('hidden');
        }

        function openEditModal(id) {
            const p = products.find(item => item.id === id);
            if(p) {
                document.getElementById('modal-title').innerText = 'تعديل المنتج';
                document.getElementById('product-id').value = p.id;
                document.getElementById('p-name').value = p.name;
                document.getElementById('p-price').value = p.price;
                document.getElementById('p-category').value = p.category;
                document.getElementById('p-image').value = p.image;
                document.getElementById('p-sold').checked = p.soldOut;
                document.getElementById('product-modal').classList.remove('hidden');
            }
        }

        function closeProductModal() {
            document.getElementById('product-modal').classList.add('hidden');
        }

        function saveProduct(e) {
            e.preventDefault();
            const id = document.getElementById('product-id').value;
            const name = document.getElementById('p-name').value;
            const price = Number(document.getElementById('p-price').value);
            const category = document.getElementById('p-category').value;
            const image = document.getElementById('p-image').value;
            const soldOut = document.getElementById('p-sold').checked;

            if(id) {
                const p = products.find(item => item.id == id);
                if(p) {
                    p.name = name;
                    p.price = price;
                    p.category = category;
                    p.image = image;
                    p.soldOut = soldOut;
                }
            } else {
                const newId = products.length > 0 ? Math.max(...products.map(p => p.id)) + 1 : 1;
                products.push({ id: newId, name, price, category, image, soldOut });
            }

            closeProductModal();
            saveData();
        }

        // Cart Logic
        function addToCart(id) {
            const p = products.find(item => item.id === id);
            if(p && !p.soldOut) {
                const existing = cart.find(item => item.id === id);
                if(existing) {
                    existing.qty += 1;
                } else {
                    cart.push({ ...p, qty: 1 });
                }
                saveData();
                openCart();
            }
        }

        function updateCartQty(id, change) {
            const item = cart.find(i => i.id === id);
            if(item) {
                item.qty += change;
                if(item.qty <= 0) {
                    cart = cart.filter(i => i.id !== id);
                }
                saveData();
                renderCart();
            }
        }

        function openCart() {
            renderCart();
            document.getElementById('cart-modal').classList.remove('hidden');
        }

        function closeCart() {
            document.getElementById('cart-modal').classList.add('hidden');
        }

        function renderCart() {
            const container = document.getElementById('cart-items-container');
            container.innerHTML = '';
            let total = 0;

            if(cart.length === 0) {
                container.innerHTML = `<div class="text-center py-8 text-slate-500 text-sm">سلة المشتريات فارغة.</div>`;
                document.getElementById('cart-total').innerText = '0 ج.م';
                updateCartBadge();
                return;
            }

            cart.forEach(item => {
                total += item.price * item.qty;
                container.innerHTML += `
                    <div class="flex items-center justify-between bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                        <div class="flex items-center gap-3">
                            <img src="${item.image}" class="w-12 h-12 rounded-xl object-cover bg-slate-900 shrink-0">
                            <div>
                                <h4 class="text-sm font-bold text-white">${item.name}</h4>
                                <div class="text-xs text-amber-400 font-semibold">${item.price} ج.م</div>
                            </div>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="updateCartQty(${item.id}, -1)" class="w-7 h-7 rounded-lg bg-slate-800 hover:bg-slate-700 text-white flex items-center justify-center font-bold text-sm">-</button>
                            <span class="text-sm font-bold w-5 text-center">${item.qty}</span>
                            <button onclick="updateCartQty(${item.id}, 1)" class="w-7 h-7 rounded-lg bg-slate-800 hover:bg-slate-700 text-white flex items-center justify-center font-bold text-sm">+</button>
                        </div>
                    </div>
                `;
            });

            document.getElementById('cart-total').innerText = total + ' ج.م';
            updateCartBadge();
        }

        function updateCartBadge() {
            const badge = document.getElementById('cart-badge');
            const totalCount = cart.reduce((sum, item) => sum + item.qty, 0);
            if(totalCount > 0) {
                badge.innerText = totalCount;
                badge.classList.remove('hidden');
            } else {
                badge.classList.add('hidden');
            }
        }

        function checkoutWhatsApp() {
            if(cart.length === 0) return;
            let message = "مرحباً Mo2men Store، أرغب في طلب المنتجات التالية:\n\n";
            let total = 0;
            cart.forEach((item, index) => {
                message += `${index + 1}. ${item.name} (العدد: ${item.qty}) - السعر: ${item.price * item.qty} ج.م\n`;
                total += item.price * item.qty;
            });
            message += `\n*الإجمالي الكلي: ${total} ج.م*`;
            
            // استبدل الرقم برقم واتساب الخاص بك (مفتاح الدولة ورقم الهاتف)
            const phone = "201000000000"; 
            const url = `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;
            window.open(url, '_blank');
        }

        // Initialize App on Load
        renderProducts();
        updateCartBadge();
    </script>
</body>
</html>
