<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Idhayam Supermarket</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Segoe UI', Arial, sans-serif; background: #f5f5f5; color: #222; }

    /* HERO */
    .hero {
      background: #1a6b2a;
      color: #fff;
      text-align: center;
      padding: 2.5rem 1rem 2rem;
    }
    .hero-logo { font-size: 2.6rem; font-weight: 700; letter-spacing: 3px; }
    .hero-tag { font-size: 0.88rem; opacity: 0.82; margin-top: 6px; letter-spacing: 1.5px; }

    /* NAV */
    nav {
      background: #fff;
      border-bottom: 2px solid #45d261;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
    }
    nav a {
      padding: 0.75rem 1.25rem;
      color: #1a6b2a;
      font-weight: 600;
      font-size: 0.9rem;
      text-decoration: none;
      cursor: pointer;
      border-bottom: 3px solid transparent;
      transition: all 0.15s;
    }
    nav a:hover, nav a.active {
      border-bottom-color: #2d8a40;
      background: #f0faf2;
    }

    /* SECTIONS */
    .section { padding: 1.5rem 1rem; max-width: 960px; margin: 0 auto; }
    .section-title {
      font-size: 1.2rem;
      font-weight: 700;
      color: #1a6b2a;
      border-left: 4px solid #2d8a40;
      padding-left: 0.7rem;
      margin-bottom: 1.1rem;
    }

    /* CATEGORY TABS */
    .cat-row { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-bottom: 1.1rem; }
    .cat-btn {
      padding: 0.4rem 1rem;
      border-radius: 20px;
      border: 1.5px solid #2d8a40;
      background: #fff;
      color: #2d8a40;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.15s;
    }
    .cat-btn:hover, .cat-btn.active { background: #2d8a40; color: #fff; }

    /* PRODUCTS GRID */
    .products-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(148px, 1fr));
      gap: 1rem;
    }
    .product-card {
      background: #fff;
      border-radius: 12px;
      border: 1px solid #c8e6c9;
      overflow: hidden;
      transition: box-shadow 0.15s;
    }
    .product-card:hover { box-shadow: 0 4px 14px rgba(45,138,64,0.15); }
    .product-img {
      width: 100%;
      height: 96px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.6rem;
      background: #f0faf2;
    }
    .product-info { padding: 0.55rem 0.7rem 0.7rem; }
    .product-name { font-size: 0.84rem; font-weight: 700; color: #1a6b2a; }
    .product-price { font-size: 0.8rem; color: #555; margin-top: 2px; }
    .qty-row { display: flex; align-items: center; gap: 0.4rem; margin-top: 0.5rem; }
    .qty-btn {
      width: 26px; height: 26px;
      border-radius: 50%;
      border: 1.5px solid #2d8a40;
      background: #fff;
      color: #2d8a40;
      font-size: 1.1rem;
      font-weight: 700;
      cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      flex-shrink: 0;
      transition: all 0.12s;
    }
    .qty-btn:hover { background: #2d8a40; color: #fff; }
    .qty-num { font-size: 0.9rem; font-weight: 700; color: #1a6b2a; min-width: 18px; text-align: center; }

    /* CART BAR */
    .cart-bar {
      background: #1a6b2a;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0.85rem 1.25rem;
      border-radius: 10px;
      margin-top: 1.5rem;
      cursor: pointer;
      transition: background 0.15s;
    }
    .cart-bar:hover { background: #135220; }
    .cart-label { font-size: 0.95rem; font-weight: 600; margin-left: 0.5rem; }
    .cart-badge {
      background: #fff;
      color: #1a6b2a;
      width: 24px; height: 24px;
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 0.78rem;
      font-weight: 700;
      margin-left: 0.5rem;
    }

    /* MODAL OVERLAY */
    .overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.48);
      z-index: 100;
      align-items: center;
      justify-content: center;
      padding: 1rem;
    }
    .overlay.open { display: flex; }
    .modal {
      background: #fff;
      border-radius: 14px;
      width: 100%;
      max-width: 440px;
      max-height: 90vh;
      overflow-y: auto;
      animation: slideUp 0.2s ease;
    }
    @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: none; opacity: 1; } }
    .modal-head {
      background: #1a6b2a;
      color: #fff;
      padding: 1rem 1.25rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: sticky;
      top: 0;
    }
    .modal-head h2 { font-size: 1rem; font-weight: 700; }
    .modal-close {
      background: none;
      border: none;
      color: #fff;
      font-size: 1.4rem;
      cursor: pointer;
      line-height: 1;
    }
    .modal-body { padding: 1.1rem 1.25rem; }

    /* ORDER SUMMARY */
    .order-summary {
      background: #f0faf2;
      border-radius: 8px;
      padding: 0.8rem;
      margin-bottom: 1rem;
      border: 1px solid #b6dfc2;
    }
    .os-title { font-size: 0.82rem; font-weight: 700; color: #1a6b2a; margin-bottom: 0.5rem; }
    .os-item { display: flex; justify-content: space-between; font-size: 0.82rem; color: #555; padding: 3px 0; }
    .os-total {
      display: flex;
      justify-content: space-between;
      font-size: 0.92rem;
      font-weight: 700;
      color: #1a6b2a;
      border-top: 1px solid #b6dfc2;
      margin-top: 0.45rem;
      padding-top: 0.45rem;
    }

    /* FORM FIELDS */
    .field { margin-bottom: 0.9rem; }
    .field label { display: block; font-size: 0.8rem; color: #555; margin-bottom: 4px; font-weight: 600; }
    .field input,
    .field select,
    .field textarea {
      width: 100%;
      border: 1px solid #c8e6c9;
      border-radius: 8px;
      padding: 0.52rem 0.75rem;
      font-size: 0.88rem;
      color: #222;
      background: #fff;
      font-family: inherit;
      transition: border-color 0.15s;
    }
    .field input:focus,
    .field select:focus,
    .field textarea:focus { outline: none; border-color: #2d8a40; }
    .field textarea { resize: vertical; min-height: 62px; }

    .place-btn {
      width: 100%;
      padding: 0.78rem;
      background: #2d8a40;
      color: #fff;
      border: none;
      border-radius: 8px;
      font-size: 0.95rem;
      font-weight: 700;
      cursor: pointer;
      font-family: inherit;
      transition: background 0.15s;
    }
    .place-btn:hover { background: #1a6b2a; }

    /* SUCCESS */
    .success-box { text-align: center; padding: 1.5rem 1rem; }
    .success-icon { font-size: 3rem; margin-bottom: 0.75rem; }
    .success-title { font-size: 1.1rem; font-weight: 700; color: #1a6b2a; margin-bottom: 0.35rem; }
    .success-sub { font-size: 0.85rem; color: #555; line-height: 1.6; margin-bottom: 0.5rem; }
    .order-id-badge {
      display: inline-block;
      background: #f0faf2;
      color: #2d8a40;
      font-weight: 700;
      font-size: 0.85rem;
      padding: 0.4rem 0.9rem;
      border-radius: 6px;
      margin-bottom: 1rem;
    }
    .done-btn {
      padding: 0.6rem 1.5rem;
      background: #2d8a40;
      color: #fff;
      border: none;
      border-radius: 8px;
      font-size: 0.88rem;
      font-weight: 600;
      cursor: pointer;
      font-family: inherit;
    }
    .done-btn:hover { background: #1a6b2a; }

    /* CONTACT */
    .contact-card {
      background: #f0faf2;
      border-radius: 12px;
      padding: 1.25rem;
      border: 1px solid #b6dfc2;
    }
    .c-item { display: flex; align-items: flex-start; gap: 0.75rem; margin-bottom: 0.9rem; }
    .c-icon {
      width: 36px; height: 36px;
      background: #2d8a40;
      border-radius: 8px;
      display: flex; align-items: center; justify-content: center;
      color: #fff;
      font-size: 1.1rem;
      flex-shrink: 0;
    }
    .c-label { font-size: 0.75rem; color: #777; }
    .c-val { font-size: 0.9rem; color: #1a6b2a; font-weight: 600; }

    footer {
      background: #1a6b2a;
      color: rgba(255,255,255,0.82);
      text-align: center;
      padding: 1rem;
      font-size: 0.82rem;
      margin-top: 2rem;
    }

    .hidden { display: none !important; }

    @media (max-width: 480px) {
      .hero-logo { font-size: 1.9rem; }
      .products-grid { grid-template-columns: repeat(2, 1fr); }
    }
  </style>
</head>
<body>

<!-- HERO -->
<div class="hero">
  <div class="hero-logo">🌿 IDHAYAM</div>
  <div class="hero-tag">YOUR NEIGHBOURHOOD SUPERMARKET</div>
</div>

<!-- NAV -->
<nav>
  <a class="active" onclick="showSection('order', this)">🛒 Order</a>
  <a onclick="showSection('contact', this)">📞 Contact</a>
</nav>

<!-- ORDER SECTION -->
<div id="sec-order">
  <div class="section">
    <div class="section-title">What are you looking for?</div>
    <div class="cat-row">
      <button class="cat-btn active" onclick="filterCat('all', this)">All</button>
      <button class="cat-btn" onclick="filterCat('stationery', this)">✏️ Stationery</button>
      <button class="cat-btn" onclick="filterCat('chocolate', this)">🍫 Chocolates</button>
      <button class="cat-btn" onclick="filterCat('toys', this)">🧸 Toys</button>
      <button class="cat-btn" onclick="filterCat('gifts', this)">🎁 Gifts</button>
    </div>
    <div class="products-grid" id="products-grid"></div>
    <div class="cart-bar" onclick="openCheckout()">
      <div style="display:flex;align-items:center">
        <span>🛒</span>
        <span class="cart-label">View cart</span>
        <span class="cart-badge" id="cart-count">0</span>
      </div>
      <span id="cart-total" style="font-weight:700">₹0.00</span>
    </div>
  </div>
</div>

<!-- CONTACT SECTION -->
<div id="sec-contact" class="hidden">
  <div class="section">
    <div class="section-title">Get in touch</div>
    <div class="contact-card">
      <div class="c-item">
        <div class="c-icon">📍</div>
        <div><div class="c-label">Address</div><div class="c-val">arumugam pillai complex,ECR road,manamelkudi – 614 620</div></div>
      </div>
      <div class="c-item">
        <div class="c-icon">📞</div>
        <div><div class="c-label">Phone</div><div class="c-val">+91 98400 12345</div></div>
      </div>
      <div class="c-item">
        <div class="c-icon">✉️</div>
        <div><div class="c-label">Email</div><div class="c-val">orders@idhayamsupermarket.in</div></div>
      </div>
      <div class="c-item">
        <div class="c-icon">🕐</div>
        <div>
          <div class="c-label">Store hours</div>
          <div class="c-val">Mon – Sat: 8:00 AM – 9:00 PM<br>Sunday: 9:00 AM – 7:00 PM</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- CHECKOUT MODAL -->
<div class="overlay" id="overlay">
  <div class="modal">
    <div class="modal-head">
      <h2 id="modal-title">Complete your order</h2>
      <button class="modal-close" onclick="closeCheckout()">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<footer>© 2026 Idhayam Supermarket · Made with 💚 for you</footer>

<script>
  const PRODUCTS = [
    { id: 1,  cat: 'stationery', name: 'Notebook set',    price: 30,  emoji: '📓' },
    { id: 1,  cat: 'stationery', name: 'Notebook set',    price: 50,  emoji: '📓' },
    { id: 2,  cat: 'stationery', name: 'Pen pack (10)',   price: 45,  emoji: '🖊️' },
    { id: 3,  cat: 'stationery', name: 'Colour pencils',  price: 120, emoji: '🎨' },
    { id: 4,  cat: 'stationery', name: 'Sticky notes',    price: 60,  emoji: '📌' },
    { id: 5,  cat: 'chocolate',  name: 'Dark chocolate',  price: 95,  emoji: '🍫' },
    { id: 6,  cat: 'chocolate',  name: 'Milk choco bar',  price: 55,  emoji: '🍬' },
    { id: 7,  cat: 'chocolate',  name: 'Choco truffles',  price: 180, emoji: '🍭' },
    { id: 8,  cat: 'chocolate',  name: 'Wafer crunch',    price: 70,  emoji: '🍪' },
    { id: 9,  cat: 'toys',       name: 'Building blocks', price: 350, emoji: '🧱' },
    { id: 10, cat: 'toys',       name: 'Teddy bear',      price: 299, emoji: '🧸' },
    { id: 11, cat: 'toys',       name: 'Puzzle 100pc',    price: 225, emoji: '🧩' },
    { id: 12, cat: 'toys',       name: 'Mini car set',    price: 180, emoji: '🚗' },
    { id: 13, cat: 'gifts',      name: 'Gift hamper',     price: 599, emoji: '🎁' },
    { id: 14, cat: 'gifts',      name: 'Greeting cards',  price: 40,  emoji: '💌' },
    { id: 15, cat: 'gifts',      name: 'Scented candle',  price: 250, emoji: '🕯️' },
    { id: 16, cat: 'gifts',      name: 'Photo frame',     price: 195, emoji: '🖼️' },
  ];

  const qty = {};
  PRODUCTS.forEach(p => qty[p.id] = 0);
  let currentCat = 'all';

  function renderProducts() {
    const list = currentCat === 'all' ? PRODUCTS : PRODUCTS.filter(p => p.cat === currentCat);
    document.getElementById('products-grid').innerHTML = list.map(p => `
      <div class="product-card">
        <div class="product-img">${p.emoji}</div>
        <div class="product-info">
          <div class="product-name">${p.name}</div>
          <div class="product-price">₹${p.price}</div>
          <div class="qty-row">
            <button class="qty-btn" onclick="changeQty(${p.id}, -1)">−</button>
            <span class="qty-num" id="q${p.id}">${qty[p.id]}</span>
            <button class="qty-btn" onclick="changeQty(${p.id}, 1)">+</button>
          </div>
        </div>
      </div>`).join('');
  }

  function changeQty(id, delta) {
    qty[id] = Math.max(0, (qty[id] || 0) + delta);
    const el = document.getElementById('q' + id);
    if (el) el.textContent = qty[id];
    updateCart();
  }

  function updateCart() {
    let total = 0, count = 0;
    PRODUCTS.forEach(p => { total += qty[p.id] * p.price; count += qty[p.id]; });
    document.getElementById('cart-count').textContent = count;
    document.getElementById('cart-total').textContent = '₹' + total.toFixed(2);
  }

  function filterCat(cat, btn) {
    currentCat = cat;
    document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    renderProducts();
  }

  function showSection(name, link) {
    document.getElementById('sec-order').classList.toggle('hidden', name !== 'order');
    document.getElementById('sec-contact').classList.toggle('hidden', name !== 'contact');
    document.querySelectorAll('nav a').forEach(a => a.classList.remove('active'));
    link.classList.add('active');
  }

  function cartItems() { return PRODUCTS.filter(p => qty[p.id] > 0); }
  function cartTotal() { return cartItems().reduce((s, p) => s + qty[p.id] * p.price, 0); }

  function openCheckout() {
    const items = cartItems();
    if (!items.length) { alert('Add some products first!'); return; }
    const summary = items.map(p =>
      `<div class="os-item"><span>${p.emoji} ${p.name} ×${qty[p.id]}</span><span>₹${(qty[p.id] * p.price).toFixed(2)}</span></div>`
    ).join('');
    document.getElementById('modal-title').textContent = 'Complete your order';
    document.getElementById('modal-body').innerHTML = `
      <div class="order-summary">
        <div class="os-title">Your items</div>
        ${summary}
        <div class="os-total"><span>Total</span><span>₹${cartTotal().toFixed(2)}</span></div>
      </div>
      <div class="field"><label>Your name</label><input id="f-name" type="text" placeholder="Ravi Kumar"></div>
      <div class="field"><label>Phone number</label><input id="f-phone" type="tel" placeholder="+91 98765 43210"></div>
      <div class="field"><label>Email address</label><input id="f-email" type="email" placeholder="ravi@email.com"></div>
      <div class="field"><label>Delivery address</label><textarea id="f-addr" placeholder="Door no, Street, Area, City, Pincode"></textarea></div>
      <div class="field"><label>Payment method</label>
        <select id="f-pay">
          <option value="">Select payment</option>
          <option>Cash on delivery</option>
          <option>UPI</option>
          <option>Net banking</option>
          <option>Credit / Debit card</option>
        </select>
      </div>
      <div class="field"><label>Special instructions (optional)</label><textarea id="f-note" placeholder="Any special requests..."></textarea></div>
      <button class="place-btn" onclick="placeOrder()">Place order →</button>
    `;
    document.getElementById('overlay').classList.add('open');
  }

  function closeCheckout() {
    document.getElementById('overlay').classList.remove('open');
  }

  function placeOrder() {
    const name  = document.getElementById('f-name').value.trim();
    const phone = document.getElementById('f-phone').value.trim();
    const email = document.getElementById('f-email').value.trim();
    const addr  = document.getElementById('f-addr').value.trim();
    const pay   = document.getElementById('f-pay').value;
    const note  = document.getElementById('f-note').value.trim();

    if (!name)  { alert('Enter your name.'); return; }
    if (!phone) { alert('Enter your phone number.'); return; }
    if (!email) { alert('Enter your email address.'); return; }
    if (!addr)  { alert('Enter your delivery address.'); return; }
    if (!pay)   { alert('Select a payment method.'); return; }

    const items   = cartItems();
    const total   = cartTotal();
    const orderId = 'IDH-' + Date.now().toString().slice(-6);

    document.getElementById('modal-title').textContent = 'Order placed!';
    document.getElementById('modal-body').innerHTML = `
      <div class="success-box">
        <div class="success-icon">✅</div>
        <div class="success-title">Order confirmed, ${name.split(' ')[0]}!</div>
        <div class="order-id-badge">Order ID: ${orderId}</div>
        <div class="success-sub">
          A confirmation will be sent to <strong>${email}</strong>.<br>
          Delivery to: ${addr}.<br>
          Payment: ${pay}.<br>
          Total: ₹${total.toFixed(2)}.
        </div>
        <button class="done-btn" onclick="finishOrder()">Back to shop</button>
      </div>
    `;

    console.log('=== NEW ORDER ===');
    console.log('Order ID:', orderId);
    console.log('Customer:', name);
    console.log('Phone:', phone);
    console.log('Email:', email);
    console.log('Address:', addr);
    console.log('Payment:', pay);
    console.log('Items:', items.map(p => `${p.name} x${qty[p.id]} = ₹${(qty[p.id]*p.price).toFixed(2)}`).join(', '));
    console.log('Total: ₹' + total.toFixed(2));
    if (note) console.log('Note:', note);
    console.log('=================');
  }

  function finishOrder() {
    PRODUCTS.forEach(p => qty[p.id] = 0);
    updateCart();
    renderProducts();
    closeCheckout();
  }

  // Close overlay on background click
  document.getElementById('overlay').addEventListener('click', function(e) {
    if (e.target === this) closeCheckout();
  });

  renderProducts();
</script>
</body>
</html>
