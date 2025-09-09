<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>I Love You Alfa ❤️</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #f8f0fc, #e0d4ff);
      font-family: Arial, sans-serif;
      color: #fff;
      text-align: center;
      overflow: hidden;
    }

    h1 {
      font-size: 2.5rem;
      text-shadow: 2px 2px 10px rgba(0,0,0,0.2);
      cursor: pointer;
    }

    .particle {
      position: absolute;
      width: 5px;
      height: 5px;
      background: rgba(255,255,255,0.8);
      border-radius: 50%;
      animation: float linear infinite;
    }

    @keyframes float {
      0% { transform: translateY(0); }
      100% { transform: translateY(-100vh); }
    }
  </style>
</head>
<body>

<h1 onclick="nextPage()">I love you Alfa ❤️<br>Click to see more...</h1>

<script>
let page = 1;

function nextPage() {
  page++;
  if(page === 2) {
    document.querySelector('h1').innerHTML = `
      Masttt guru chl gaya Alfa, tu ne jo itni baar sorry bola na,<br>
      usse mujhe aur yakin ho gaya ki mera pyar sachme duniya ka sabse khoobsurat tohfa hai.<br>
      Saza puri karke bhi tu muskura rahi thi… aur wahi teri muskaan meri zindagi ka sabse bada inaam hai.<br>
      Mujhe maafi ki zaroorat nahi thi, mujhe bas tera saath chahiye tha.<br>
      Aur ab lagta hai tera pyar meri rooh tak utar gaya hai.<br>
      Tu meri zindagi ka woh hissa ban gayi hai jise main kabhi khona nahi chahta.<br>
      I love you more than ever, meri Alfa. 🌹✨
    `;
  } else if(page === 3) {
    document.querySelector('h1').innerHTML = `
      Meri Alfa, tu meri zindagi ka noor hai 🌹✨<br>
      Hamesha mere saath rehna…
    `;
  }
}

// Create floating particles
for(let i=0; i<30; i++) {
  let p = document.createElement('div');
  p.className = 'particle';
  p.style.left = Math.random() * 100 + 'vw';
  p.style.top = Math.random() * 100 + 'vh';
  p.style.width = 2 + Math.random()*4 + 'px';
  p.style.height = 2 + Math.random()*4 + 'px';
  p.style.animationDuration = 6 + Math.random()*6 + 's';
  document.body.appendChild(p);
}
</script>

</body>
</html>
