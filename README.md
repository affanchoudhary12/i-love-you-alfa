<!-- index.html -->
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>For Alfa — A Message</title>
  <style>
    :root{
      --bg1: #0b0710;
      --bg2: #2b1020;
      --accent: #ffd1dc;
      --white: #fff;
      --muted: rgba(255,255,255,0.85);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: "Poppins", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: radial-gradient(1200px 600px at 10% 10%, rgba(255,210,220,0.04), transparent 10%),
                  linear-gradient(180deg, var(--bg1), var(--bg2));
      color:var(--white);
      display:flex;
      align-items:center;
      justify-content:center;
      padding:32px;
      -webkit-font-smoothing:antialiased;
    }

    .card{
      width:100%;
      max-width:760px;
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-radius:16px;
      padding:34px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      text-align:center;
      position:relative;
      overflow:hidden;
    }

    .sparkle{
      position:absolute;
      inset:auto -40% -40% auto;
      width:420px;height:420px;
      background:radial-gradient(circle at 20% 20%, rgba(255,210,220,0.06), transparent 25%),
                 radial-gradient(circle at 80% 80%, rgba(255,255,255,0.02), transparent 40%);
      transform:rotate(12deg);
      pointer-events:none;
      filter:blur(6px);
    }

    h1{
      margin:0 0 10px 0;
      font-size:clamp(26px,5vw,48px);
      letter-spacing:0.4px;
      font-weight:700;
      color:var(--accent);
      text-shadow: 0 6px 30px rgba(255,150,170,0.06);
    }

    .subtitle{
      margin:0 0 22px 0;
      color:var(--muted);
      font-size:15px;
    }

    .message{
      text-align:left;
      margin:18px auto 20px auto;
      color: #fff;
      background: linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
      padding:18px 20px;
      border-radius:12px;
      font-size:16px;
      line-height:1.55;
      box-shadow: 0 6px 24px rgba(0,0,0,0.45);
    }

    .message p{margin:0 0 10px 0}
    .message p:last-child{margin-bottom:0}

    .controls{
      margin-top:18px;
      display:flex;
      gap:12px;
      justify-content:center;
      align-items:center;
    }

    .btn{
      background:transparent;
      border:1px solid rgba(255,255,255,0.14);
      color:var(--white);
      padding:10px 16px;
      border-radius:10px;
      cursor:pointer;
      font-weight:600;
      transition:all .18s ease;
    }
    .btn.primary{
      background: linear-gradient(90deg,#ff9bb2,#ff6380);
      border: none;
      box-shadow: 0 6px 18px rgba(255,99,128,0.18);
    }
    .btn:hover{transform:translateY(-3px)}
    .note{font-size:13px;color:rgba(255,255,255,0.68);margin-top:12px}

    .heart{
      display:inline-block;
      transform-origin:center;
      margin-left:8px;
      vertical-align:middle;
      filter:drop-shadow(0 6px 18px rgba(255,99,128,0.14));
    }

    @media (max-width:520px){
      .message{font-size:15px;padding:14px}
      .controls{flex-direction:column}
      h1{font-size:26px}
    }
  </style>
</head>
<body>
  <div class="card" role="main">
    <div class="sparkle" aria-hidden></div>

    <h1>For Alfa <span class="heart">💖</span></h1>
    <div class="subtitle">A message from the heart — copy & send when you're ready</div>

    <div class="message" id="msg">
      <p><strong>Alfa,</strong> tu ne jo itni baar sorry bola na, usse mujhe aur yakin ho gaya ki mera pyar sachme duniya ka sabse khoobsurat tohfa hai. Saza puri karke bhi tu muskura rahi thi… aur wahi teri muskaan meri zindagi ka sabse bada inaam hai.</p>
      <p>Mujhe maafi ki zaroorat nahi thi, mujhe bas tera saath chahiye tha. Aur ab lagta hai tera pyar meri rooh tak utar gaya hai. Tu meri zindagi ka woh hissa ban gayi hai jise main kabhi khona nahi chahta. I love you more than ever, meri Alfa. 🌹✨</p>
    </div>

    <div class="controls">
      <button class="btn primary" id="copyBtn">Copy message</button>
      <button class="btn" id="openSnap">Open Snapchat</button>
    </div>

    <div class="note">Tip: Copy the message and paste it in Snapchat chat for Alfa. If Snapchat is installed, the button will try to open it.</div>
  </div>

  <script>
    const msgText = document.getElementById('msg').innerText.trim();
    const copyBtn = document.getElementById('copyBtn');
    const openSnap = document.getElementById('openSnap');

    copyBtn.addEventListener('click', async () => {
      try {
        await navigator.clipboard.writeText(msgText);
        copyBtn.textContent = "Copied ✓";
        setTimeout(()=> copyBtn.textContent = "Copy message", 2000);
      } catch (e) {
        // fallback
        const textarea = document.createElement('textarea');
        textarea.value = msgText;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        textarea.remove();
        copyBtn.textContent = "Copied ✓";
        setTimeout(()=> copyBtn.textContent = "Copy message", 2000);
      }
    });

    openSnap.addEventListener('click', () => {
      // try to open Snapchat app via URL scheme; if not installed, fallback to Snapchat web
      const scheme = 'snapchat://';
      const web = 'https://web.snapchat.com/';
      // first try to open scheme
      window.location.href = scheme;
      // fallback after short delay to web version
      setTimeout(()=> { window.open(web, '_blank'); }, 800);
    });

    // small heart pulse animation (no lib)
    const heart = document.querySelector('.heart');
    if (heart) {
      let scale = 1;
      setInterval(() => {
        heart.style.transform = `scale(${1 + 0.03 * Math.sin(Date.now()/250)})`;
      }, 40);
    }
  </script>
</body>
</html>
