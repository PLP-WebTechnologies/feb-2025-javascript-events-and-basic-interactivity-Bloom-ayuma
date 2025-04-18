# feb-2025-avasjcript-events-and-basic-interactivity
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Interactive JavaScript Form</title>
  <link rel="stylesheet" href="style.css" />
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f0f2f5;
    }

    form {
      max-width: 400px;
      background-color: #fff;
      padding: 15px;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    label {
      display: block;
      margin-top: 10px;
    }

    input[type="text"],
    input[type="password"],
    input[type="email"] {
      width: 100%;
      padding: 8px;
      margin-top: 5px;
    }

    button {
      margin-top: 15px;
      padding: 10px 15px;
      cursor: pointer;
    }

    .error {
      color: red;
      font-size: 0.9em;
    }

    #form-result.success {
      animation: fadeIn 0.8s ease-in-out;
      color: green;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }
  </style>
</head>
<body>

  <header>
    <h1>Interactive Form with LocalStorage</h1>
  </header>

  <main>
    <section>
      <form id="signup-form">
        <label for="username">Username:</label>
        <input type="text" id="username" required value="bloom" />
        <span class="error" id="username-error"></span>

        <label for="email">Email:</label>
        <input type="email" id="email" required />
        <span class="error" id="email-error"></span>

        <label for="password">Password:</label>
        <input type="password" id="password" required value="Lbuluma01@" />
        <button type="button" id="toggle-password">👁️</button>
        <span class="error" id="password-error"></span>

        <button type="submit">Sign Up</button>
      </form>
      <button id="clear-storage">🧹 Clear LocalStorage</button>
      <p id="form-result"></p>
    </section>

    <section>
      <button id="toggle-info-btn">Toggle Extra Info</button>
      <div id="extra-info" style="display: none;">
        <p>🎉 You found the hidden content! Nice job exploring interactive JavaScript.</p>
      </div>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 JS Interaction Playground</p>
  </footer>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const form = document.getElementById('signup-form');
      const username = document.getElementById('username');
      const email = document.getElementById('email');
      const password = document.getElementById('password');

      const usernameError = document.getElementById('username-error');
      const emailError = document.getElementById('email-error');
      const passwordError = document.getElementById('password-error');
      const formResult = document.getElementById('form-result');

      const togglePasswordBtn = document.getElementById('toggle-password');
      const toggleInfoBtn = document.getElementById('toggle-info-btn');
      const clearStorageBtn = document.getElementById('clear-storage');
      const extraInfo = document.getElementById('extra-info');

      // Toggle password visibility
      togglePasswordBtn.addEventListener('click', () => {
        password.type = password.type === 'password' ? 'text' : 'password';
      });

      // Toggle extra info
      toggleInfoBtn.addEventListener('click', () => {
        extraInfo.style.display = extraInfo.style.display === 'none' ? 'block' : 'none';
      });

      // Greet if data is stored
      const savedUser = localStorage.getItem('username');
      if (savedUser) {
        formResult.textContent = `👋 Welcome back, ${savedUser}!`;
        formResult.classList.add('success');
      }

      // Clear localStorage
      clearStorageBtn.addEventListener('click', () => {
        localStorage.clear();
        formResult.textContent = '🧹 LocalStorage cleared!';
        formResult.style.color = 'orange';
      });

      // Form validation and save
      form.addEventListener('submit', (e) => {
        e.preventDefault();
        let valid = true;

        // Username validation
        if (username.value.trim() === '') {
          usernameError.textContent = 'Username is required.';
          valid = false;
        } else {
          usernameError.textContent = '';
        }

        // Email validation
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email.value)) {
          emailError.textContent = 'Please enter a valid email address.';
          valid = false;
        } else {
          emailError.textContent = '';
        }

        // Password validation
        if (password.value.length < 8) {
          passwordError.textContent = 'Password must be at least 8 characters.';
          valid = false;
        } else {
          passwordError.textContent = '';
        }

        if (valid) {
          localStorage.setItem('username', username.value.trim());
          localStorage.setItem('email', email.value.trim());
          localStorage.setItem('password', password.value); // 🔐 for demo only!

          formResult.textContent = `🎉 Welcome, ${username.value}! Your data has been saved.`;
          formResult.className = 'success';
          form.reset();
        } else {
          formResult.textContent = '';
          formResult.className = '';
        }
      });
    });
  </script>
</body>
</html>
