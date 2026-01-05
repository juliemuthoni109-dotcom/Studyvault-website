# Studyvault-website
website for selling exam papers and notes
index.html
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
      <p class="price">KES 300</p>
      <button onclick="addToCart('Math 120',300)">Add to Cart</button>
    </div>
    <div class="card">
      <h3>Physics 113 – Notes</h3>
      <p>Concise revision notes</p>
      <p class="price">KES 250</p>
      <button onclick="addToCart('Physics 113',250)">Add to Cart</button>
    </div>
    <div class="card">
      <h3>ACS 113 – Full Pack</h3>
      <p>Notes + Past Papers</p>
      <p class="price">KES 400</p>
      <button onclick="addToCart('ACS 113',400)">Add to Cart</button>
    </div>
  </div>
</section>

<section class="container" id="login">
  <h2>User Login / Signup</h2>
  <input type="email" id="email" placeholder="Email" />
  <input type="password" id="password" placeholder="Password" />
  <button onclick="signup(document.getElementById('email').value, document.getElementById('password').value)">Sign Up</button>
  <button onclick="login(document.getElementById('email').value, document.getElementById('password').value)">Login</button>
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
  <ul id="downloadList"></ul>
</section>

<section class="container" id="contact">
  <h2>Contact</h2>
  <p>Email: studyvault@gmail.com</p>
  <p>WhatsApp: +254 7XX XXX XXX</p>
</section>

<footer>
  <p>&copy; 2026 StudyVault</p>
</footer>

<!-- Firebase SDKs -->
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-storage.js"></script>

<script>
  // Firebase config (replace with your config)
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "studyvault.firebaseapp.com",
    projectId: "studyvault",
    storageBucket: "studyvault.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  const app = firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();
  const storage = firebase.storage();

  // Signup
  function signup(email, password){
    auth.createUserWithEmailAndPassword(email, password)
      .then(userCredential => { alert('Signup successful'); })
      .catch(error => alert(error.message));
  }

  // Login
  function login(email, password){
    auth.signInWithEmailAndPassword(email, password)
      .then(userCredential => { alert('Login successful'); })
      .catch(error => alert(error.message));
  }

  // Cart
  let total = 0;
  let cart = [];
  function addToCart(item, price) {
    cart.push({item, price});
    total += price;
    document.getElementById('cartItems').innerHTML = '';
    cart.forEach(c => {
      const li = document.createElement('li');
      li.textContent = c.item + ' - KES ' + c.price;
      document.getElementById('cartItems').appendChild(li);
    });
    document.getElementById('total').textContent = total;
  }

  // M-Pesa Payment (Demo)
  function payMpesa() {
    if(total === 0){ alert('Cart is empty'); return; }
    alert('M-Pesa STK Push sent!'); // Replace with real API call later
    showDownloads();
    document.getElementById('download').classList.remove('hidden');
  }

  // Show downloads after payment
  function showDownloads(){
    const downloadList = document.getElementById('downloadList');
    downloadList.innerHTML = '';
    cart.forEach(c => {
      let path = c.item.replace(/\s/g,'') + '.pdf'; // Example: Math120.pdf
      storage.ref(path).getDownloadURL()
        .then(url => {
          const li = document.createElement('li');
          const a = document.createElement('a');
          a.href = url;
          a.target = '_blank';
          a.textContent = c.item + ' Download';
          li.appendChild(a);
          downloadList.appendChild(li);
        }).catch(()=>{
          const li = document.createElement('li');
          li.textContent = c.item + ' (File not available yet)';
          downloadList.appendChild(li);
        });
    });
  }
</script>

</body>
</html>
