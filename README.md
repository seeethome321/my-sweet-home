Final production-ready Howardhome site — all files with your Stripe link, email, and phone

Below are the complete files ready to drop into a single folder and deploy. I replaced the Stripe placeholder with your Stripe checkout URL https://buy.stripe.com/3cIfZb3jjgiLbSZ5C6ew800, set the email to Peggyhoward757@gmail.com, and the phone to 9293361203 (links use tel:+19293361203). Add the referenced images and lease-agreement.pdf, then upload to your host.

---

`index.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <section class="landing">
      <h1>Welcome to Howardhome</h1>
      <p>Your trusted place to find rental homes in Los Angeles and Burbank. Browse listings, apply online, and pay securely.</p>
      <a href="properties.html" class="cta-button">View Properties</a>
    </section>

    <section class="features">
      <div class="feature">
        <h3>Simple Applications</h3>
        <p>Apply online with a $20 non-refundable application fee.</p>
      </div>
      <div class="feature">
        <h3>Secure Payments</h3>
        <p>Payments processed via Stripe for security and convenience.</p>
      </div>
      <div class="feature">
        <h3>Responsive Support</h3>
        <p>Contact us by phone or email for questions and showings.</p>
      </div>
    </section>

    <section class="contact card">
      <h2>Contact</h2>
      <p><strong>Phone:</strong> <a href="tel:+19293361203">9293361203</a></p>
      <p><strong>Email:</strong> <a href="mailto:Peggyhoward757@gmail.com">Peggyhoward757@gmail.com</a></p>
      <p><strong>Application Fee:</strong> $20 (non‑refundable)</p>
      <p><a href="lease-agreement.pdf" target="_blank">📄 View Lease Agreement</a></p>
    </section>
  </main>

  <footer class="footer">
    <p>© <span id="year"></span> Howardhome — All rights reserved.</p>
  </footer>

  <script>
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>


---

`properties.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Howardhome Properties</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <h1>Available Properties</h1>
    <div id="propertiesGrid" class="properties"></div>
  </main>

  <footer class="footer">
    <p>© <span id="year2"></span> Howardhome</p>
  </footer>

  <script src="data.js"></script>
  <script>
    document.getElementById('year2').textContent = new Date().getFullYear();

    const grid = document.getElementById('propertiesGrid');

    function createCard(p) {
      const div = document.createElement('div');
      div.className = 'property-card';
      div.innerHTML = `
        <img src="${p.image}" alt="${p.title}">
        <h3>${p.title}</h3>
        <p class="muted">${p.location}</p>
        <p class="price">Rent: <strong>$${p.rent.toLocaleString()}</strong> / month</p>
        <p class="muted">Deposit: $${p.deposit}</p>
        <div class="card-actions">
          <a class="btn" href="details.html?id=${encodeURIComponent(p.id)}">View Details</a>
          <a class="btn outline" href="apply.html?id=${encodeURIComponent(p.id)}">Apply</a>
          <a class="btn" href="payments.html?id=${encodeURIComponent(p.id)}">Pay</a>
        </div>
      `;
      return div;
    }

    const saved = JSON.parse(localStorage.getItem('howard_properties') || '[]');
    const all = [...propertiesData, ...saved];

    all.forEach(p => grid.appendChild(createCard(p)));
  </script>
</body>
</html>


---

`details.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Property Details - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <div id="detailContainer"></div>
  </main>

  <footer class="footer">
    <p>© <span id="year3"></span> Howardhome</p>
  </footer>

  <script src="data.js"></script>
  <script>
    document.getElementById('year3').textContent = new Date().getFullYear();

    function getParam(name) {
      const url = new URL(window.location.href);
      return url.searchParams.get(name) || (location.hash ? location.hash.replace('#','') : null);
    }

    const id = getParam('id');
    const saved = JSON.parse(localStorage.getItem('howard_properties') || '[]');
    const all = [...propertiesData, ...saved];
    const prop = all.find(p => p.id === id);

    const container = document.getElementById('detailContainer');

    if (!prop) {
      container.innerHTML = `
        <div class="card">
          <h2>Property not found</h2>
          <p>We couldn't find that listing. <a href="properties.html">Return to listings</a>.</p>
        </div>`;
    } else {
      container.innerHTML = `
        <article class="details card">
          <img src="${prop.image}" alt="${prop.title}">
          <h2>${prop.title}</h2>
          <p class="muted">${prop.location}</p>
          <p><strong>Rent:</strong> $${prop.rent.toLocaleString()} / month</p>
          <p><strong>Deposit:</strong> $${prop.deposit}</p>
          <p><strong>Description:</strong> ${prop.description}</p>
          <p><a href="${prop.zillow || '#'}" target="_blank">View on Zillow</a></p>

          <section class="contact-block">
            <h3>Contact & Apply</h3>
            <p><strong>Phone:</strong> <a href="tel:+19293361203">9293361203</a></p>
            <p><strong>Email:</strong> <a href="mailto:Peggyhoward757@gmail.com">Peggyhoward757@gmail.com</a></p>
            <p><strong>Application Fee:</strong> $20 (non‑refundable)</p>
            <p><a href="lease-agreement.pdf" target="_blank">📄 View Lease Agreement</a></p>
            <div class="card-actions">
              <a class="btn" href="apply.html?id=${encodeURIComponent(prop.id)}">Apply Now</a>
              <a class="btn" href="https://buy.stripe.com/3cIfZb3jjgiLbSZ5C6ew800">Pay with Stripe</a>
            </div>
          </section>
        </article>
      `;
    }
  </script>
</body>
</html>


---

`apply.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Apply - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <h1>Rental Application</h1>
    <div class="card">
      <form id="applicationForm">
        <input type="hidden" id="propId" name="propId">
        <label>Full name<input type="text" id="appName" required></label>
        <label>Email<input type="email" id="appEmail" required></label>
        <label>Phone<input type="tel" id="appPhone" required></label>
        <label>Current address<input type="text" id="appAddress"></label>
        <label>Message / Notes<textarea id="appNotes" rows="4"></textarea></label>
        <p class="muted">Application fee: <strong>$20</strong> (non‑refundable). After submitting, click the Pay button to complete the fee via Stripe.</p>
        <div class="card-actions">
          <button type="submit" class="btn">Submit Application</button>
          <a id="payNow" class="btn outline" href="#">Pay $20</a>
        </div>
      </form>
      <div id="appMessage" class="muted" style="margin-top:12px;"></div>
    </div>
  </main>

  <script src="data.js"></script>
  <script>
    function getParam(name) {
      const url = new URL(window.location.href);
      return url.searchParams.get(name) || (location.hash ? location.hash.replace('#','') : null);
    }
    const id = getParam('id');
    document.getElementById('propId').value = id || '';

    const stripeLink = 'https://buy.stripe.com/3cIfZb3jjgiLbSZ5C6ew800';
    document.getElementById('payNow').href = stripeLink + '?amount=20&purpose=application&property=' + encodeURIComponent(id || '');

    document.getElementById('applicationForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const app = {
        id: 'app_' + Date.now(),
        propertyId: document.getElementById('propId').value,
        name: document.getElementById('appName').value,
        email: document.getElementById('appEmail').value,
        phone: document.getElementById('appPhone').value,
        address: document.getElementById('appAddress').value,
        notes: document.getElementById('appNotes').value,
        submittedAt: new Date().toISOString()
      };
      const apps = JSON.parse(localStorage.getItem('howard_applications') || '[]');
      apps.push(app);
      localStorage.setItem('howard_applications', JSON.stringify(apps));
      document.getElementById('appMessage').textContent = 'Application saved locally. Please complete the $20 application fee via the Pay button.';
    });
  </script>
</body>
</html>


---

`payments.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Payments - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <div class="payment-box card">
      <h2>Payment Portal</h2>
      <p class="muted">Application Fee: <strong>$20</strong> (non‑refundable)</p>
      <form id="payForm">
        <label>Tenant Name<input type="text" id="payName" required></label>
        <label>Property Address / ID<input type="text" id="payProperty" required></label>
        <label>Amount (USD)<input type="number" id="payAmount" value="20" min="1" required></label>
        <label>Payment Type
          <select id="payType">
            <option>Application Fee</option>
            <option>Rent</option>
            <option>Deposit</option>
            <option>Late Fee</option>
          </select>
        </label>
        <div class="card-actions">
          <button type="submit" class="btn">Pay with Stripe</button>
        </div>
      </form>
      <p id="payNote" class="muted" style="margin-top:12px;">You will be redirected to Stripe to complete the payment.</p>
    </div>
  </main>

  <script>
    const stripeCheckout = 'https://buy.stripe.com/3cIfZb3jjgiLbSZ5C6ew800';

    document.getElementById('payForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const name = encodeURIComponent(document.getElementById('payName').value);
      const property = encodeURIComponent(document.getElementById('payProperty').value);
      const amount = encodeURIComponent(document.getElementById('payAmount').value);
      const type = encodeURIComponent(document.getElementById('payType').value);

      const url = `${stripeCheckout}?amount=${amount}&name=${name}&property=${property}&type=${type}`;
      window.location.href = url;
    });
  </script>
</body>
</html>


---

`confirmation.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Payment Confirmation - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <div class="confirmation-box card">
      <h2>✅ Payment Successful</h2>
      <p>Thank you — your payment was processed securely via Stripe.</p>
      <p>If this was an application fee, please complete the rental application form if you haven't already.</p>
      <p>Questions? Contact <a href="mailto:Peggyhoward757@gmail.com">Peggyhoward757@gmail.com</a> or call <a href="tel:+19293361203">9293361203</a>.</p>
      <a class="btn" href="properties.html">Back to Properties</a>
    </div>
  </main>
</body>
</html>


---

`error.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Payment Error - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <div class="error-box card">
      <h2>❌ Payment Failed or Canceled</h2>
      <p>We couldn't complete your payment. Please try again or contact support.</p>
      <p>📞 <a href="tel:+19293361203">9293361203</a> | 📧 <a href="mailto:Peggyhoward757@gmail.com">Peggyhoward757@gmail.com</a></p>
      <a class="btn" href="payments.html">Try Again</a>
    </div>
  </main>
</body>
</html>


---

`admin.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Admin - Howardhome</title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="navbar">
    <div class="nav-logo">Howardhome</div>
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="properties.html">Properties</a></li>
      <li><a href="apply.html">Apply</a></li>
      <li><a href="payments.html">Payments</a></li>
      <li><a href="admin.html">Admin</a></li>
    </ul>
  </nav>

  <main class="container">
    <h1>Admin Dashboard</h1>

    <div class="card">
      <form id="addPropertyForm">
        <label>Property ID (unique)<input type="text" id="propId" required></label>
        <label>Title<input type="text" id="propTitle" required></label>
        <label>Location<input type="text" id="propLocation" required></label>
        <label>Rent (USD)<input type="number" id="propRent" required></label>
        <label>Deposit (USD)<input type="number" id="propDeposit" required></label>
        <label>Image URL<input type="text" id="propImage" placeholder="e.g., images/myprop.jpg"></label>
        <label>Description<textarea id="propDesc" rows="4"></textarea></label>
        <label>Zillow Link (optional)<input type="url" id="propZillow"></label>
        <div class="card-actions">
          <button type="submit" class="btn">Add Property</button>
          <button type="button" id="clearStorage" class="btn outline">Clear Added Properties</button>
        </div>
      </form>
      <p class="muted">Properties added here are stored in your browser's localStorage (demo). For production, connect to your backend.</p>
    </div>

    <section id="adminList" class="properties" style="margin-top:20px;"></section>
  </main>

  <script src="data.js"></script>
  <script>
    const adminList = document.getElementById('adminList');

    function renderAdminList() {
      adminList.innerHTML = '';
      const saved = JSON.parse(localStorage.getItem('howard_properties') || '[]');
      if (!saved.length) {
        adminList.innerHTML = '<p class="muted">No properties added yet.</p>';
        return;
      }
      saved.forEach(p => {
        const card = document.createElement('div');
        card.className = 'property-card';
        card.innerHTML = `
          <img src="${p.image}" alt="${p.title}">
          <h3>${p.title}</h3>
          <p class="muted">${p.location}</p>
          <p class="price">Rent: <strong>$${p.rent.toLocaleString()}</strong></p>
          <div class="card-actions">
            <a class="btn outline" href="details.html?id=${encodeURIComponent(p.id)}">View</a>
            <button class="btn remove" data-id="${p.id}">Remove</button>
          </div>
        `;
        adminList.appendChild(card);
      });
    }

    document.getElementById('addPropertyForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const p = {
        id: document.getElementById('propId').value.trim(),
        title: document.getElementById('propTitle').value.trim(),
        location: document.getElementById('propLocation').value.trim(),
        rent: Number(document.getElementById('propRent').value),
        deposit: Number(document.getElementById('propDeposit').value),
        image: document.getElementById('propImage').value || 'default.jpg',
        description: document.getElementById('propDesc').value.trim(),
        zillow: document.getElementById('propZillow').value || ''
      };
      if (!p.id || !p.title) return alert('Please provide ID and title.');
      const saved = JSON.parse(localStorage.getItem('howard_properties') || '[]');
      if (saved.some(x => x.id === p.id)) return alert('Property ID already exists in local storage.');
      saved.push(p);
      localStorage.setItem('howard_properties', JSON.stringify(saved));
      renderAdminList();
      e.target.reset();
    });

    adminList.addEventListener('click', function(e) {
      if (e.target.matches('.remove')) {
        const id = e.target.dataset.id;
        let saved = JSON.parse(localStorage.getItem('howard_properties') || '[]');
        saved = saved.filter(p => p.id !== id);
        localStorage.setItem('howard_properties', JSON.stringify(saved));
        renderAdminList();
      }
    });

    document.getElementById('clearStorage').addEventListener('click', function() {
      if (!confirm('Clear all properties added via admin? This cannot be undone.')) return;
      localStorage.removeItem('howard_properties');
      renderAdminList();
    });

    renderAdminList();
  </script>
</body>
</html>


---

`data.js`

// propertiesData: built-in sample properties (15 entries)
const propertiesData = [
  {
    id: "MountainView",
    title: "1 Bed, 1 Bath ADU",
    location: "437 ½ N Mountain View Ave, Los Angeles, CA",
    rent: 1550,
    deposit: 500,
    image: "mountainview.jpg",
    description: "Compact ADU near Sunset Blvd with modern finishes.",
    zillow: "https://www.zillow.com/homedetails/437-N-Mountain-View-Ave-Los-Angeles-CA-90026/"
  },
  {
    id: "LyricAve",
    title: "2 Bed, 2 Bath Home",
    location: "2516 Lyric Ave, Los Angeles, CA",
    rent: 4775,
    deposit: 500,
    image: "lyric.jpg",
    description: "Spacious 2 bed, 2 bath Los Feliz home with hardwood floors.",
    zillow: "https://www.zillow.com/homedetails/2516-Lyric-Ave-Los-Angeles-CA-90027/"
  },
  {
    id: "SecurityAve",
    title: "2 Bed, 2 Bath ADU",
    location: "7619 Security Ave, Burbank, CA",
    rent: 2200,
    deposit: 500,
    image: "security.jpg",
    description: "Modern ADU built in 2023 with in-unit laundry.",
    zillow: "https://www.zillow.com/homedetails/7619-Security-Ave-Burbank-CA-91504/"
  },
  {
    id: "SunsetStudio",
    title: "Studio",
    location: "1208 Sunset Blvd, Los Angeles, CA",
    rent: 1250,
    deposit: 500,
    image: "sunset.jpg",
    description: "Cozy studio close to shops and transit on Sunset Blvd."
  },
  {
    id: "SilverLakeCottage",
    title: "1 Bed, 1 Bath Cottage",
    location: "2048 Silver Lake Blvd, Los Angeles, CA",
    rent: 1900,
    deposit: 500,
    image: "silverlake.jpg",
    description: "Charming cottage with private yard and updated kitchen."
  },
  {
    id: "EchoParkDuplex",
    title: "2 Bed, 1 Bath Duplex",
    location: "101 Echo Park Ave, Los Angeles, CA",
    rent: 2100,
    deposit: 500,
    image: "echo.jpg",
    description: "Bright duplex unit with hardwood floors and street views."
  },
  {
    id: "HighlandBungalow",
    title: "3 Bed, 2 Bath Bungalow",
    location: "512 Highland Park Dr, Los Angeles, CA",
    rent: 3250,
    deposit: 1000,
    image: "highland.jpg",
    description: "Spacious bungalow with garden and garage."
  },
  {
    id: "VeniceFlat",
    title: "1 Bed, 1 Bath Flat",
    location: "45 Ocean Front Walk, Venice, CA",
    rent: 2800,
    deposit: 1000,
    image: "venice.jpg",
    description: "Beachside flat steps from the boardwalk and cafes."
  },
  {
    id: "CulverTownhome",
    title: "2 Bed, 2 Bath Townhome",
    location: "3300 Culver Blvd, Culver City, CA",
    rent: 3100,
    deposit: 1000,
    image: "culver.jpg",
    description: "Modern townhome in a quiet complex near downtown Culver City."
  },
  {
    id: "StudioCityCondo",
    title: "1 Bed, 1 Bath Condo",
    location: "1400 Studio City Ln, Studio City, CA",
    rent: 2350,
    deposit: 800,
    image: "studio_city.jpg",
    description: "Updated condo with in-unit laundry and reserved parking."
  },
  {
    id: "NoHoADU",
    title: "1 Bed, 1 Bath ADU",
    location: "900 N Hollywood Way, Burbank, CA",
    rent: 1650,
    deposit: 500,
    image: "north_hollywood.jpg",
    description: "Compact ADU near studios and transit, ideal for single occupant."
  },
  {
    id: "PasadenaHome",
    title: "3 Bed, 2 Bath Home",
    location: "78 Pasadena Ave, Pasadena, CA",
    rent: 3400,
    deposit: 1200,
    image: "pasadena.jpg",
    description: "Classic Pasadena home with large living spaces and yard."
  },
  {
    id: "BurbankCottage",
    title: "2 Bed, 1 Bath Cottage",
    location: "220 Magnolia Blvd, Burbank, CA",
    rent: 2050,
    deposit: 700,
    image: "burbank_cottage.jpg",
    description: "Quaint cottage close to shops and restaurants on Magnolia Blvd."
  },
  {
    id: "GlendaleApartment",
    title: "2 Bed, 1 Bath Apartment",
    location: "410 Glendale Blvd, Glendale, CA",
    rent: 2300,
    deposit: 800,
    image: "glendale.jpg",
    description: "Well-maintained apartment in a secure building with elevator access."
  },
  {
    id: "NorthLAHome",
    title: "4 Bed, 3 Bath Family Home",
    location: "1500 N La Brea Ave, Los Angeles, CA",
    rent: 4200,
    deposit: 1500,
    image: "north_la.jpg",
    description: "Large family home with multiple living areas and a backyard."
  }
];


---

`style.css`

/* Base */
:root{
  --primary:#0078d7;
  --accent:#28a745;
  --muted:#6b7280;
  --bg:#f5f7fb;
  --card:#ffffff;
  --radius:10px;
  --max-width:1100px;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  background:var(--bg);
  color:#222;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}
.container{max-width:var(--max-width);margin:28px auto;padding:0 16px}

/* Navbar */
.navbar{
  background:var(--card);
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding:12px 20px;
  box-shadow:0 2px 6px rgba(16,24,40,0.06);
  position:sticky;top:0;z-index:50;
}
.nav-logo{font-weight:700;color:var(--primary)}
.nav-links{list-style:none;display:flex;gap:14px;margin:0;padding:0}
.nav-links a{color:#111;text-decoration:none;padding:8px 10px;border-radius:8px}
.nav-links a:hover{background:rgba(0,120,215,0.06)}

/* Landing */
.landing{background:linear-gradient(90deg, rgba(0,120,215,0.06), transparent);padding:36px;border-radius:var(--radius);text-align:center;margin-bottom:18px}
.landing h1{margin:0 0 8px;font-size:28px}
.landing p{margin:0 0 16px;color:var(--muted)}
.cta-button{display:inline-block;background:var(--primary);color:#fff;padding:12px 18px;border-radius:8px;text-decoration:none}
.cta-button:hover{background:#005a9e}

/* Features */
.features{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px;margin-bottom:18px}
.feature{background:var(--card);padding:16px;border-radius:10px;box-shadow:0 2px 6px rgba(16,24,40,0.04)}

/* Cards */
.card{background:var(--card);padding:18px;border-radius:var(--radius);box-shadow:0 6px 18px rgba(16,24,40,0.06)}
.properties{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px;padding:8px 0}
.property-card{background:var(--card);border-radius:10px;overflow:hidden;box-shadow:0 6px 18px rgba(16,24,40,0.06);transition:transform .18s}
.property-card:hover{transform:translateY(-6px)}
.property-card img{width:100%;height:170px;object-fit:cover;display:block}
.property-card h3{margin:12px 12px 6px;font-size:18px}
.property-card p{margin:6px 12px;color:var(--muted)}
.price{margin:6px 12px;color:#111}
.card-actions{display:flex;gap:8px;padding:12px}
.btn{display:inline-block;background:var(--primary);color:#fff;padding:8px 12px;border-radius:8px;text-decoration:none;border:none;cursor:pointer}
.btn.outline{background:transparent;color:var(--primary);border:1px solid rgba(0,120,215,0.12)}
.btn:hover{opacity:.95}

/* Details */
.details img{width:100%;height:360px;object-fit:cover;border-radius:8px;margin-bottom:12px}
.details .contact-block{margin-top:18px;padding-top:12px;border-top:1px dashed rgba(0,0,0,0.06)}

/* Forms */
label{display:block;margin:8px 0;font-size:14px}
input[type="text"],input[type="email"],input[type="tel"],input[type="number"],textarea,select{
  width:100%;padding:10px;border-radius:8px;border:1px solid #e6e9ef;background:#fff;margin-top:6px;font-size:14px
}
textarea{resize:vertical}
.payment-box{max-width:480px;margin:0 auto}

/* Confirmation / Error */
.confirmation-box,.error-box{max-width:640px;margin:40px auto;text-align:center}

/* Footer */
.footer{text-align:center;padding:18px;color:var(--muted);font-size:14px;margin-top:28px}

/* Utilities */
.muted{color:var(--muted)}
.card-actions{display:flex;gap:8px;flex-wrap:wrap}

/* Responsive */
@media (max-width:640px){
  .nav-links{display:none}
  .landing h1{font-size:22px}
  .details img{height:220px}
}


---

Quick deployment checklist

• Stripe: Stripe link already embedded: https://buy.stripe.com/3cIfZb3jjgiLbSZ5C6ew800. Configure Stripe Checkout success/cancel redirects to:• Success → https://your-domain/confirmation.html
• Cancel → https://your-domain/error.html

• Images: Add the images referenced in data.js (or replace with hosted URLs).
• Lease PDF: Upload lease-agreement.pdf to the same folder if you want the lease link to work.
• Host: Deploy to Netlify, Vercel, or GitHub Pages (push this folder to a repo and enable Pages).


If you want, I’ll now:

• (A) produce a ZIP-style folder tree listing for easy copy/paste, or
• (B) walk you step-by-step through deploying to Netlify or GitHub Pages, or
• (C) replace image paths with placeholder hosted images for immediate testing.


Which next step do you want me to do now?
