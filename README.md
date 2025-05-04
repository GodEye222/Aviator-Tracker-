# Aviator-Tracker-

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Aviator Crash Tracker</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #000;
      color: #0f0;
    }
    #tracker {
      padding: 10px;
      background: #111;
      text-align: center;
      font-size: 18px;
    }
    #crashValue {
      font-size: 36px;
      color: #f00;
      margin-top: 5px;
    }
    iframe {
      width: 100%;
      height: 90vh;
      border: none;
    }
  </style>
</head>
<body>
  <div id="tracker">
    <div>Latest Crash Value:</div>
    <div id="crashValue">Waiting...</div>
  </div>

  <iframe id="aviatorFrame" src="https://www.sportybet.com/gh/m/games" sandbox="allow-scripts allow-same-origin allow-forms"></iframe>

  <script>
    const crashValueEl = document.getElementById("crashValue");
    const iframe = document.getElementById("aviatorFrame");

    function injectScraper() {
      try {
        const frameDoc = iframe.contentDocument || iframe.contentWindow.document;
        const crashEl = frameDoc.querySelector('[class*=crash], [class*=multiplier]');
        if (crashEl) {
          const value = crashEl.textContent.trim();
          if (value.match(/^[0-9.]+x$/)) {
            crashValueEl.textContent = value;
          }
        }
      } catch (err) {
        console.warn("Unable to inject into iframe due to cross-origin restrictions.");
      }
    }

    setInterval(injectScraper, 1000);
  </script>
</body>
</html>
