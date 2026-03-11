[index.html](https://github.com/user-attachments/files/25914794/index.html)
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SmerfMc.pl • Doładowania</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600&family=VT323&display=swap" rel="stylesheet">
    <style>
        :root {
            --smerf-blue: #2E94E3;
            --smerf-green: #55FF88;
            --gold: #FFDD55;
            --dark: #0a1421;
            --card: #142233;
        }
        body {
            margin:0; padding:0;
            font-family: 'Fredoka', sans-serif;
            background: linear-gradient(to bottom, #0a1421, #0f1f35);
            color: #e0f7ff;
            overflow-x: hidden;
        }
        #entry-screen {
            position: fixed; inset:0;
            background: radial-gradient(circle, #1e3a8a, #0a1421);
            display: flex; flex-direction:column; justify-content:center; align-items:center;
            z-index: 9999; transition: opacity 1s;
        }
        #entry-screen h1 {
            font-family: 'VT323', monospace;
            font-size: 7rem;
            color: var(--smerf-green);
            text-shadow: 0 0 30px var(--smerf-green);
        }
        .container { max-width: 1100px; margin: 0 auto; padding: 40px 15px; display: none; }
        .shop-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(235px, 1fr));
            gap: 18px;
        }
        .card {
            background: var(--card); border: 5px solid var(--smerf-blue);
            border-radius: 16px; padding: 22px; text-align:center;
            transition: all 0.3s; box-shadow: 0 8px 0 #000;
        }
        .card:hover {
            transform: translateY(-12px);
            border-color: var(--smerf-green);
            box-shadow: 0 20px 0 #000, 0 0 35px rgba(85,255,136,0.6);
        }
        .card h3 { font-family:'VT323',monospace; font-size:2.3rem; color:white; margin:8px 0; }
        .card .price { font-size:3rem; color:var(--gold); font-weight:bold; }
        .card .desc { font-size:1.05rem; color:#bbffdd; margin:15px 0; min-height:85px; }
        .btn-mc {
            background:var(--smerf-green); color:#000; border:none;
            border-radius:10px; border-bottom:7px solid #2e9944;
            padding:14px 40px; font-family:'VT323',monospace; font-size:1.9rem;
            cursor:pointer; width:100%;
        }
        .btn-mc:active { transform:translateY(5px); border-bottom:3px solid #2e9944; }

        /* MODAL */
        #payment-modal {
            display:none; position:fixed; inset:0;
            background:rgba(0,0,0,0.9); z-index:10000;
            justify-content:center; align-items:center;
        }
        .modal-content {
            background:#0f1a2b; border:6px solid var(--smerf-green);
            border-radius:20px; padding:35px; width:92%; max-width:460px;
            text-align:center; position:relative; box-shadow:0 0 50px rgba(85,255,136,0.7);
        }
        .step1, .step2 { transition: all 0.4s; }
        .close-modal { position:absolute; top:12px; right:25px; font-size:3.5rem; cursor:pointer; color:#777; }

        input { width:100%; padding:16px; margin:20px 0; border:4px solid var(--smerf-blue);
            border-radius:12px; background:#0a1421; color:white; font-size:1.3rem; }
        .methods { display:flex; flex-wrap:wrap; gap:12px; justify-content:center; margin:25px 0; }
        .method-btn {
            background:#1e2a3c; border:4px solid var(--smerf-blue); border-radius:12px;
            padding:16px 28px; cursor:pointer; font-size:1.45rem; transition:0.3s;
        }
        .method-btn:hover { background:var(--smerf-green); color:black; transform:scale(1.05); }

        .next-step { display:none; font-size:1.3rem; color:#bbffdd; margin-top:20px; }
    </style>
</head>
<body>

<div id="entry-screen">
    <h1>SMERFMC.PL</h1>
    <button class="btn-mc" style="font-size:3rem;padding:22px 90px;" onclick="startShop()">WEJDŹ DO SKLEPU</button>
</div>

<div class="container" id="main-shop">
    <h2 style="font-family:'VT323',monospace;font-size:4.8rem;color:#FFDD55;text-align:center;text-shadow:5px 5px 0 #664400;margin-bottom:40px;">
        DOŁADUJ SMERFA!
    </h2>

    <div class="shop-grid">
        <!-- 1 zł -->
        <div class="card">
            <h3>1 zł</h3>
            <div class="price">1 zł</div>
            <div class="desc">+1 home • prefix [Smerf] • podziękowanie na czacie</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 1 zł', '1.00')">DOŁADUJ</button>
        </div>
        <!-- 5 zł -->
        <div class="card">
            <h3>5 zł</h3>
            <div class="price">5 zł</div>
            <div class="desc">+2 home • boost exp ×1.2 (3 dni) • kolorowy nick + zielone particle</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 5 zł', '5.00')">DOŁADUJ</button>
        </div>
        <!-- 10 zł -->
        <div class="card">
            <h3>10 zł</h3>
            <div class="price">10 zł</div>
            <div class="desc">+4 home • boost exp×1.5 + money×1.3 (7 dni) • pelerynka + 50 vote key</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 10 zł', '10.00')">DOŁADUJ</button>
        </div>
        <!-- 15 zł -->
        <div class="card">
            <h3>15 zł</h3>
            <div class="price">15 zł</div>
            <div class="desc">+6 home • boost ×1.8 (10 dni) • wyłączone reklamy + custom particle</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 15 zł', '15.00')">DOŁADUJ</button>
        </div>
        <!-- 20 zł -->
        <div class="card">
            <h3>20 zł</h3>
            <div class="price">20 zł</div>
            <div class="desc">+8 home • boost ×2.0 (14 dni) • pelerynka + 120 vote key + legendarny klucz</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 20 zł', '20.00')">DOŁADUJ</button>
        </div>
        <!-- 30 zł -->
        <div class="card">
            <h3>30 zł</h3>
            <div class="price">30 zł</div>
            <div class="desc">+10 home • boost ×2.5 (21 dni) • firework na join + 200 vote key</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 30 zł', '30.00')">DOŁADUJ</button>
        </div>
        <!-- 50 zł -->
        <div class="card">
            <h3>50 zł</h3>
            <div class="price">50 zł</div>
            <div class="desc">+15 home • boost ×3.0 (30 dni) • tag [SMERF LEGENDA] + mythic key</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 50 zł', '50.00')">DOŁADUJ</button>
        </div>
        <!-- 100 zł -->
        <div class="card">
            <h3>100 zł</h3>
            <div class="price">100 zł</div>
            <div class="desc">∞ home • boost ×4.0 (60 dni) • permanentna peleryna + [SMERF BOSS] + 10 mythic</div>
            <button class="btn-mc" onclick="openPayment('Doładowanie 100 zł', '100.00')">DOŁADUJ</button>
        </div>
    </div>
</div>

<!-- MODAL Z DWOMA KROKAMI -->
<div id="payment-modal">
    <div class="modal-content">
        <span class="close-modal" onclick="closePayment()">×</span>
        
        <!-- KROK 1 -->
        <div id="step1">
            <h2 id="modal-title" style="font-family:'VT323',monospace;font-size:3rem;color:#FFDD55;">DOŁADOWANIE</h2>
            <p id="modal-price" style="color:#55FF88;font-size:2.4rem;margin:15px 0;">0.00 zł</p>
            <input type="text" id="nickname" placeholder="Twój nick w grze..." style="font-size:1.4rem;">
            
            <div class="methods">
                <div class="method-btn" onclick="selectMethod('BLIK')">BLIK</div>
                <div class="method-btn" onclick="selectMethod('Przelew')">Przelew</div>
                <div class="method-btn" onclick="selectMethod('PSC')">PSC</div>
                <div class="method-btn" onclick="selectMethod('SMS')">SMS</div>
            </div>
        </div>

        <!-- KROK 2 (pojawia się po wyborze metody) -->
        <div id="step2" class="next-step">
            <h2 id="method-name" style="color:#55FF88;font-size:2.6rem;margin-bottom:20px;"></h2>
            <p id="instruction" style="font-size:1.35rem;line-height:1.5;"></p>
            <button onclick="finishPurchase()" class="btn-mc" style="margin-top:25px;width:auto;padding:14px 50px;">ZAKOŃCZ I ZAPŁAĆ</button>
        </div>
    </div>
</div>

<script>
function startShop() {
    document.getElementById('entry-screen').style.opacity = '0';
    setTimeout(() => {
        document.getElementById('entry-screen').style.display = 'none';
        document.getElementById('main-shop').style.display = 'block';
    }, 900);
}

let currentItem = '';
let currentPrice = '';

function openPayment(name, price) {
    currentItem = name;
    currentPrice = price;
    document.getElementById('modal-title').innerText = name;
    document.getElementById('modal-price').innerText = price + ' zł';
    document.getElementById('step1').style.display = 'block';
    document.getElementById('step2').style.display = 'none';
    document.getElementById('payment-modal').style.display = 'flex';
}

function closePayment() {
    document.getElementById('payment-modal').style.display = 'none';
}

function selectMethod(method) {
    const nick = document.getElementById('nickname').value.trim();
    if (!nick) return alert("Wpisz swój nick z Minecrafta!");

    document.getElementById('step1').style.display = 'none';
    document.getElementById('step2').style.display = 'block';

    document.getElementById('method-name').innerText = method;

    let instr = '';
    if (method === 'BLIK') instr = 'Otwórz aplikację bankową → wpisz kod BLIK 6-cyfrowy → zatwierdź';
    else if (method === 'Przelew') instr = 'Przelej dokładnie ' + currentPrice + ' zł na konto podane po kliknięciu „ZAKOŃCZ”';
    else if (method === 'PSC') instr = 'Wpisz kod PaySafeCard i zatwierdź';
    else if (method === 'SMS') instr = 'Wyślij SMS o treści SMERF ' + nick + ' na numer, który zaraz pokażę';

    document.getElementById('instruction').innerHTML = instr + '<br><br><strong>Nick:</strong> ' + nick;
}

function finishPurchase() {
    alert('✅ Płatność rozpoczęta! Nick: ' + document.getElementById('nickname').value + ' | ' + currentItem);
    closePayment();
    // Tutaj w przyszłości wstawisz prawdziwe przekierowanie do bramki
}
</script>
</body>
</html>
