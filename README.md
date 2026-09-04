<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Garuda Store | Grocery & Electronics</title>

  <!-- EmailJS -->
  <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: #f5f7fa;
      color: #111827;
    }

    header {
      position: sticky;
      top: 0;
      z-index: 1000;
      background: white;
      padding: 15px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px #0001;
    }

    .logo {
      font-size: 20px;
      font-weight: 800;
    }

    .cart-btn {
      border: none;
      background: #111827;
      color: white;
      width: 45px;
      height: 45px;
      border-radius: 50%;
      font-size: 20px;
      cursor: pointer;
      position: relative;
    }

    #cartCount {
      position: absolute;
      top: -4px;
      right: -4px;
      background: #ef4444;
      color: white;
      border-radius: 50%;
      font-size: 11px;
      padding: 4px 6px;
    }

    .hero {
      min-height: 500px;
      background:
        linear-gradient(#0008, #0008),
        url("https://i.ibb.co/LDNjLgn5/Screenshot-20260904-155832.jpg")
        center/cover no-repeat;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 30px 20px;
      color: white;
    }

    .hero h1 {
      font-size: clamp(34px, 8vw, 65px);
      margin-bottom: 15px;
    }

    .hero p {
      font-size: 18px;
      margin-bottom: 25px;
    }

    .shop-now {
      display: inline-block;
      background: #22c55e;
      color: white;
      padding: 14px 28px;
      border-radius: 30px;
      text-decoration: none;
      font-weight: bold;
    }

    section {
      padding: 45px 18px;
    }

    .section-title {
      text-align: center;
      font-size: 30px;
      margin-bottom: 25px;
    }

    .products {
      display: flex;
      gap: 18px;
      overflow-x: auto;
      scroll-behavior: smooth;
      padding: 10px 3px 20px;
    }

    .products::-webkit-scrollbar {
      height: 6px;
    }

    .products::-webkit-scrollbar-thumb {
      background: #bbb;
      border-radius: 10px;
    }

    .product {
      min-width: 220px;
      background: white;
      border-radius: 18px;
      overflow: hidden;
      box-shadow: 0 5px 20px #00000012;
      flex-shrink: 0;
    }

    .product img {
      width: 100%;
      height: 180px;
      object-fit: cover;
    }

    .product-info {
      padding: 15px;
    }

    .product h3 {
      margin-bottom: 8px;
    }

    .price {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 12px;
    }

    .add {
      width: 100%;
      border: none;
      padding: 11px;
      border-radius: 10px;
      background: #111827;
      color: white;
      cursor: pointer;
      font-weight: bold;
    }

    .add:hover {
      background: #22c55e;
    }

    /* Cart */
    .overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: #0008;
      z-index: 2000;
    }

    .cart {
      position: fixed;
      right: -100%;
      top: 0;
      height: 100%;
      width: min(400px, 100%);
      background: white;
      z-index: 3000;
      padding: 22px;
      transition: .3s;
      overflow-y: auto;
    }

    .cart.open {
      right: 0;
    }

    .cart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }

    .close {
      border: none;
      background: #eee;
      width: 35px;
      height: 35px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 18px;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      border-bottom: 1px solid #ddd;
      padding: 12px 0;
    }

    .remove {
      border: none;
      background: #fee2e2;
      color: #dc2626;
      padding: 6px 9px;
      border-radius: 7px;
      cursor: pointer;
    }

    .total {
      font-size: 22px;
      font-weight: bold;
      margin: 20px 0;
    }

    .order-form input,
    .order-form textarea {
      width: 100%;
      padding: 13px;
      margin-bottom: 12px;
      border: 1px solid #ddd;
      border-radius: 10px;
      outline: none;
    }

    .order-form textarea {
      min-height: 80px;
      resize: vertical;
    }

    .send-order {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 12px;
      background: #22c55e;
      color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    /* WhatsApp */
    .whatsapp {
      position: fixed;
      right: 18px;
      bottom: 18px;
      width: 58px;
      height: 58px;
      border-radius: 50%;
      background: #25D366;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      text-decoration: none;
      font-size: 28px;
      z-index: 1500;
      box-shadow: 0 5px 20px #0004;
    }

    footer {
      background: #111827;
      color: white;
      text-align: center;
      padding: 30px 15px;
    }

    @media (max-width: 600px) {
      .hero {
        min-height: 450px;
      }

      section {
        padding: 35px 14px;
      }

      .product {
        min-width: 200px;
      }
    }
  </style>
</head>

<body>

<header>
  <div class="logo">🦅 Garuda Store</div>

  <button class="cart-btn" onclick="openCart()">
    🛒
    <span id="cartCount">0</span>
  </button>
</header>

<!-- HERO -->
<section class="hero">
  <div>
    <h1>Garuda Store</h1>
    <p>Fresh Finds, Best Prices</p>
    <p>Grocery & Electronics</p>
    <a href="#products" class="shop-now">Shop Now</a>
  </div>
</section>

<!-- PRODUCTS -->
<section id="products">
  <h2 class="section-title">Our Products</h2>

  <div class="products">

    <div class="product">
      <img src="https://images.unsplash.com/photo-1542838132-92c53300491e?auto=format&fit=crop&w=600&q=80">
      <div class="product-info">
        <h3>Fresh Groceries</h3>
        <div class="price">₹99</div>
        <button class="add" onclick="addToCart('Fresh Groceries',99)">Add to Cart</button>
      </div>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1601050690597-df0568f70950?auto=format&fit=crop&w=600&q=80">
      <div class="product-info">
        <h3>Daily Essentials</h3>
        <div class="price">₹149</div>
        <button class="add" onclick="addToCart('Daily Essentials',149)">Add to Cart</button>
      </div>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1593642532744-d377ab507dc8?auto=format&fit=crop&w=600&q=80">
      <div class="product-info">
        <h3>Electronics</h3>
        <div class="price">₹499</div>
        <button class="add" onclick="addToCart('Electronics',499)">Add to Cart</button>
      </div>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1585386959984-a4155224a1ad?auto=format&fit=crop&w=600&q=80">
      <div class="product-info">
        <h3>Home Products</h3>
        <div class="price">₹199</div>
        <button class="add" onclick="addToCart('Home Products',199)">Add to Cart</button>
      </div>
    </div>

    <div class="product">
      <img src="https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?auto=format&fit=crop&w=600&q=80">
      <div class="product-info">
        <h3>Accessories</h3>
        <div class="price">₹299</div>
        <button class="add" onclick="addToCart('Accessories',299)">Add to Cart</button>
      </div>
    </div>

  </div>
</section>

<!-- FOOTER -->
<footer>
  <h3>Garuda Store and Grocery & Electronics</h3>
  <p>Fresh Finds, Best Prices</p>
  <p>📧 anikettakarasbusiness@gmail.com</p>
</footer>

<!-- OVERLAY -->
<div class="overlay" id="overlay" onclick="closeCart()"></div>

<!-- CART -->
<div class="cart" id="cart">

  <div class="cart-header">
    <h2>Your Cart 🛒</h2>
    <button class="close" onclick="closeCart()">×</button>
  </div>

  <div id="cartItems"></div>

  <div class="total">
    Total: ₹<span id="cartTotal">0</span>
  </div>

  <!-- CUSTOMER ORDER FORM -->
  <form class="order-form" onsubmit="sendOrder(event)">

    <input
      type="text"
      id="customerName"
      placeholder="Your Name"
      required
    >

    <input
      type="tel"
      id="customerPhone"
      placeholder="Phone Number"
      required
    >

    <textarea
      id="customerAddress"
      placeholder="Delivery Address"
      required
    ></textarea>

    <button class="send-order" type="submit">
      📧 Send Order
    </button>

  </form>

</div>

<!-- WHATSAPP -->
<a
  class="whatsapp"
  href="https://wa.me/917020259952"
  target="_blank"
  aria-label="WhatsApp"
>
  ☎
</a>

<script>

  /* =========================
     EMAILJS CONFIGURATION
     ========================= */

  const EMAILJS_PUBLIC_KEY = "YOUR_PUBLIC_KEY";
  const EMAILJS_SERVICE_ID = "YOUR_SERVICE_ID";
  const EMAILJS_TEMPLATE_ID = "YOUR_TEMPLATE_ID";

  emailjs.init({
    publicKey: EMAILJS_PUBLIC_KEY
  });


  /* =========================
     CART SYSTEM
     ========================= */

  let cart = [];

  function addToCart(name, price) {

    const existing = cart.find(item => item.name === name);

    if (existing) {
      existing.quantity++;
    } else {
      cart.push({
        name: name,
        price: price,
        quantity: 1
      });
    }

    updateCart();

    openCart();
  }


  function removeFromCart(index) {

    cart.splice(index, 1);

    updateCart();
  }


  function updateCart() {

    const cartItems = document.getElementById("cartItems");
    const cartCount = document.getElementById("cartCount");
    const cartTotal = document.getElementById("cartTotal");

    cartItems.innerHTML = "";

    let total = 0;
    let count = 0;

    cart.forEach((item, index) => {

      const itemTotal = item.price * item.quantity;

      total += itemTotal;
      count += item.quantity;

      cartItems.innerHTML += `
        <div class="cart-item">

          <div>
            <strong>${item.name}</strong><br>
            ₹${item.price} × ${item.quantity}
          </div>

          <button
            class="remove"
            onclick="removeFromCart(${index})"
          >
            Remove
          </button>

        </div>
      `;
    });

    cartCount.textContent = count;
    cartTotal.textContent = total;
  }


  function openCart() {

    document.getElementById("cart").classList.add("open");
    document.getElementById("overlay").style.display = "block";
  }


  function closeCart() {

    document.getElementById("cart").classList.remove("open");
    document.getElementById("overlay").style.display = "none";
  }


  /* =========================
     SEND ORDER USING EMAILJS
     ========================= */

  function sendOrder(event) {

    event.preventDefault();

    if (cart.length === 0) {
      alert("Please add at least one product.");
      return;
    }

    const name =
      document.getElementById("customerName").value;

    const phone =
      document.getElementById("customerPhone").value;

    const address =
      document.getElementById("customerAddress").value;


    let itemsText = "";
    let total = 0;

    cart.forEach(item => {

      const itemTotal = item.price * item.quantity;

      itemsText +=
        `${item.name} - ₹${item.price} × ${item.quantity} = ₹${itemTotal}\n`;

      total += itemTotal;
    });


    const templateParams = {

      customer_name: name,

      customer_phone: phone,

      customer_address: address,

      order_items: itemsText,

      order_total: `₹${total}`,

      owner_email: "anikettakarasbusiness@gmail.com"

    };


    const button =
      document.querySelector(".send-order");

    button.disabled = true;

    button.textContent = "Sending...";


    emailjs.send(
      EMAILJS_SERVICE_ID,
      EMAILJS_TEMPLATE_ID,
      templateParams
    )

    .then(() => {

      alert(
        "✅ Order sent successfully!\n\nGaruda Store will contact you soon."
      );

      cart = [];

      updateCart();

      document.querySelector(".order-form").reset();

      closeCart();

    })

    .catch((error) => {

      console.error(error);

      alert(
        "❌ Order could not be sent.\nPlease check your EmailJS settings."
      );

    })

    .finally(() => {

      button.disabled = false;

      button.textContent = "📧 Send Order";

    });

  }

</script>

</body>
</html>
