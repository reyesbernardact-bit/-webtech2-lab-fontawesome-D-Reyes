<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Login</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      padding: 0;
      font-family: sans-serif;
      background-color: #f5f7fa;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .login-container {
      background: grey;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 320px;
    }
    .login-container h2 {
      margin-top: 0;
      margin-bottom: 1.5rem;
      font-size: 1.5rem;
      text-align: center;
    }
    .form-group {
      margin-bottom: 1rem;
    }
    .form-group label {
      display: block;
      margin-bottom: 0.25rem;
      font-size: 0.9rem;
      color: #333;
    }
    .form-group input {
      width: 100%;
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
    }
    .form-group input:focus {
      outline: none;
      border-color: #00FFFF;
      box-shadow: 0 0 0 2px rgba(0, 225, 255, 0.2);
    }
    .login-btn {
      width: 100%;
      padding: 0.75rem;
      background-color: #00FFFF;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 1rem;
      cursor: pointer;
    }
    .login-btn:hover {
      background-color: #FF00FF;
    }
    .error {
      color: red;
      margin-top: 0.5rem;
      font-size: 0.9rem;
      display: none;
    }
  </style>
</head>
<body>
  <div class="login-container">
    <h2>Login</h2>
    <form id="loginForm">
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" id="email" name="email" required />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" id="password" name="password" required minlength="6" />
      </div>
      <button type="submit" class="login-btn">Log In</button>
      <div class="error" id="errorMsg">Invalid credentials</div>
    </form>
  </div>

  <script>
    document.getElementById('loginForm').addEventListener('submit', function (e) {
      e.preventDefault();
      const email = document.getElementById('email').value.trim();
      const password = document.getElementById('password').value;

      // Example minimal validation
      if (!email || password.length < 6) {
        showError('Please enter valid email and password (min 6 characters).');
        return;
      }

      // Simulate login request (replace with real API call)
      fakeLogin(email, password)
        .then(res => {
          if (res.success) {
            // Redirect or do something on success
            alert('Login successful!'); 
            // window.location.href = '/dashboard';
          } else {
            showError(res.message || 'Login failed');
          }
        })
        .catch(err => {
          showError('Something went wrong');
        });
    });

    function showError(msg) {
      const errDiv = document.getElementById('errorMsg');
      errDiv.textContent = msg;
      errDiv.style.display = 'block';
    }

    // Fake login for demo (always fails except for a test account)
    function fakeLogin(email, password) {
      return new Promise((resolve) => {
        setTimeout(() => {
          if (email === 'test@example.com' && password === 'password123') {
            resolve({ success: true });
          } else {
            resolve({ success: false, message: 'Email or password incorrect' });
          }
        }, 500);
      });
    }
  </script>
</body>
</html>
