<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rambax Singh Inter College - Admin Portal</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: #f4f6f9;
      color: #333;
      min-height: 100vh;
    }

    /* Header & Banner Section */
    .header-banner {
      position: relative;
      background: linear-gradient(rgba(15, 32, 67, 0.8), rgba(15, 32, 67, 0.8)), 
                  url('https://via.placeholder.com/1200x400?text=Rambax+Singh+Inter+College') center/cover no-repeat;
      height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #ffffff;
      text-align: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.15);
    }

    .header-banner h1 {
      font-size: 2.2rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      font-weight: 700;
      padding: 0 15px;
    }

    /* Layout */
    .main-container {
      max-width: 1000px;
      margin: -30px auto 40px auto;
      padding: 0 20px;
      display: grid;
      grid-template-columns: 300px 1fr;
      gap: 25px;
      position: relative;
      z-index: 10;
    }

    /* Manager Card */
    .manager-card {
      background: #ffffff;
      border-radius: 12px;
      padding: 25px 20px;
      text-align: center;
      box-shadow: 0 8px 20px rgba(0,0,0,0.08);
      border-top: 5px solid #1a365d;
    }

    .manager-img-wrapper {
      width: 120px;
      height: 120px;
      margin: 0 auto 15px auto;
    }

    .manager-img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid #1a365d;
    }

    .manager-card h3 {
      font-size: 1.2rem;
      color: #1a365d;
      margin-bottom: 5px;
    }

    .manager-card p {
      font-size: 0.85rem;
      color: #666;
      font-weight: 600;
    }

    /* Login Box */
    .login-card {
      background: #ffffff;
      border-radius: 12px;
      padding: 30px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.08);
    }

    .login-card h2 {
      font-size: 1.5rem;
      color: #1a365d;
      margin-bottom: 20px;
      border-bottom: 2px solid #e2e8f0;
      padding-bottom: 10px;
    }

    .form-group {
      margin-bottom: 20px;
    }

    .form-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: #4a5568;
    }

    .confidential-badge {
      display: inline-block;
      background-color: #edf2f7;
      color: #4a5568;
      padding: 8px 12px;
      border-radius: 6px;
      font-size: 0.85rem;
    }

    .password-field-wrapper {
      position: relative;
    }

    .form-control {
      width: 100%;
      padding: 12px 45px 12px 15px;
      border: 1px solid #cbd5e0;
      border-radius: 6px;
      font-size: 1rem;
      outline: none;
    }

    .toggle-password-btn {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      font-size: 1.2rem;
      user-select: none;
    }

    .submit-btn {
      width: 100%;
      background-color: #1a365d;
      color: #ffffff;
      border: none;
      padding: 12px;
      font-size: 1rem;
      font-weight: 600;
      border-radius: 6px;
      cursor: pointer;
    }

    .submit-btn:hover {
      background-color: #2b6cb0;
    }

    @media (max-width: 768px) {
      .main-container {
        grid-template-columns: 1fr;
        margin-top: 20px;
      }
    }
  </style>
</head>
<body>

  <!-- Header Section -->
  <header class="header-banner">
    <h1>Rambax Singh Inter College</h1>
  </header>

  <!-- Main Container -->
  <div class="main-container">
    
    <!-- Manager Profile -->
    <aside class="manager-card">
      <div class="manager-img-wrapper">
        <img src="https://via.placeholder.com/150?text=Manager" alt="Manager Photo" class="manager-img">
      </div>
      <h3>Manager Name</h3>
      <p>Management / Administration</p>
    </aside>

    <!-- Admin Security Portal -->
    <main class="login-card">
      <h2>Admin Security Portal</h2>

      <form id="adminLoginForm" onsubmit="handleLogin(event)">
        <!-- Admin ID Hidden -->
        <input type="hidden" id="adminId" name="admin_id" value="CONFIDENTIAL_ADMIN_ID">

        <div class="form-group">
          <label>Admin Identification Status</label>
          <div class="confidential-badge">
            🔒 Admin ID Verified & Encrypted (Hidden)
          </div>
        </div>

        <!-- Password Field -->
        <div class="form-group">
          <label for="passwordInput">Enter Password</label>
          <div class="password-field-wrapper">
            <input type="password" id="passwordInput" class="form-control" placeholder="••••••••" required>
            <span class="toggle-password-btn" id="toggleIcon" onclick="togglePasswordVisibility()">👁️</span>
          </div>
        </div>

        <button type="submit" class="submit-btn">Login to Dashboard</button>
      </form>
    </main>

  </div>

  <script>
    function togglePasswordVisibility() {
      const passwordInput = document.getElementById('passwordInput');
      const toggleIcon = document.getElementById('toggleIcon');

      if (passwordInput.type === 'password') {
        passwordInput.type = 'text';
        toggleIcon.textContent = '🙈';
      } else {
        passwordInput.type = 'password';
        toggleIcon.textContent = '👁️';
      }
    }

    function handleLogin(event) {
      event.preventDefault();
      alert("Login attempt successful!");
    }
  </script>

</body>
</html>
