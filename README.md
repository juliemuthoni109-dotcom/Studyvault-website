# Studyvault-website
website for selling exam papers and notes
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>StudyVault | Sell Exam Papers & Notes</title>
  <style>
    body { margin:0; font-family:Arial, Helvetica, sans-serif; background:#f4f6f8; }
    header { background:#1e3a8a; color:#fff; padding:20px; text-align:center; }
    nav { background:#111827; padding:10px; display:flex; justify-content:center; gap:20px; }
    nav a { color:#fff; text-decoration:none; font-weight:bold; }
    .container { max-width:1100px; margin:auto; padding:30px 20px; }
    .products { display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:20px; }
    .card { background:#fff; padding:20px; border-radius:8px; box-shadow:0 4px 10px rgba(0,0,0,0.1); }
    .price { color:#1e3a8a; font-weight:bold; }
    button { background:#1e3a8a; color:#fff; border:none; padding:10px 15px; border-radius:5px; cursor:pointer; }
    button:hover { background:#2563eb; }
    .hidden { display:none; }
    footer { background:#111827; color:#fff; text-align:center; padding:20px; margin-top:40px; }
    input { padding:10px; width:100%; margin:5px 0 15px; }
  </style>
</head>
<body>

<header>
  <h1>StudyVault</h1>
  <p>Buy & Sell Exam Papers and Notes</p>
</header>

<nav>
  <a href="#products">Products</a>
  <a href="#login">Login</a>
  <a href="#cart">Cart</a>
  <a href="#contact">Contact</a>
</nav>

<section class="container" id="products">
  <h2>Available Materials</h2>
  <div class="products">
    <div class="card">
      <h3>Math 120 – Past Papers</h3>
      <p>Past exams with solutions</p>
      <p class="price">KES 100</p>
      <button onclick="addToCart('Math 120',100)">Add to Cart</button>
    </div>
    <div class="card">
      <h3>Physics 113 – Notes</h3>
      <p>Concise revision notes</p>
      <p class="price">KES 100</p>
      <button onclick="addToCart('Physics 113',100)">Add to Cart</button>
    </div>
    <div class="card">
      <h3>ACS 113 – notes</h3>
      <p>Notes </p>
      <p class="price">KES 100</p>
      <button onclick="addToCart('ACS 113',100)">Add to Cart</button>
    </div>
  </div>
</section>

<section class="container" id="login">
  <h2>User Login</h2>
  <input type="email" placeholder="Email" />
  <input type="password" placeholder="Password" />
  <button onclick="alert('Demo login successful')">Login</button>
  <p><i>(Demo login – backend needed for real users)</i></p>
</section>

<section class="container" id="cart">
  <h2>Your Cart</h2>
  <ul id="cartItems"></ul>
  <p><strong>Total: KES <span id="total">0</span></strong></p>
  <button onclick="payMpesa()">Pay with M-Pesa</button>
</section>

<section class="container hidden" id="download">
  <h2>Downloads</h2>
  <p>Payment successful. Download your files:</p>
  <ul>
    <li><a href="#">Math120.pdf</a></li>
    <li><a href="#">Physics113.pdf</a></li>
  </ul>
</section>

<section class="container" id="contact">
  <h2>Contact</h2>
  <p>Email: studyvault@gmail.com</p>
  <p>WhatsApp: +254 7XX XXX XXX</p>
</section>

<footer>
  <p>&copy; 2026 StudyVault</p>
</footer>

<script>
  let total = 0;
  function addToCart(item, price) {
    const li = document.createElement('li');
    li.textContent = item + ' - KES ' + price;
    document.getElementById('cartItems').appendChild(li);
    total += price;
    document.getElementById('total').textContent = total;
  }

  function payMpesa() {
    if (total === 0) {
      alert('Cart is empty');
      return;
    }
    alert('M-Pesa STK Push sent (demo)');
    document.getElementById('download').classList.remove('hidden');
  }
</script>

</body>
</html>
