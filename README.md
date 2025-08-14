<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gửi em một món quà mà anh dành tặng cho em</title>
<style>
    body {
        background: linear-gradient(135deg, #f9d423, #ff4e50);
        font-family: 'Segoe UI', Arial, sans-serif;
        text-align: center;
        padding-top: 80px;
        overflow-x: hidden;
        min-height: 100vh;
    }
    h1 {
        font-size: 2.5em;
        margin-bottom: 0.5em;
        animation: fadeIn 2s;
        letter-spacing: 1px;
        text-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }
    .heart { color: #ff4e50; font-size: 1.2em; animation: heartbeat 1s infinite; }
    @keyframes heartbeat { 0%,100%{transform:scale(1);} 50%{transform:scale(1.3);} }
    @keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
    .message {
        font-size: 1.3em;
        margin: 30px auto;
        animation: fadeIn 3s;
        color: #fff;
        max-width: 600px;
        line-height: 1.6;
        background: rgba(255,255,255,0.08);
        border-radius: 16px;
        box-shadow: 0 2px 12px rgba(0,0,0,0.06);
        padding: 18px 10px;
    }
    .btn {
        background: linear-gradient(90deg, #ff4e50 0%, #f9d423 100%);
        color: #fff;
        border: none;
        padding: 15px 40px;
        font-size: 1.2em;
        border-radius: 30px;
        cursor: pointer;
        margin-top: 30px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        transition: background 0.3s, transform 0.2s;
        font-weight: bold;
    }
    .btn:hover { background: linear-gradient(90deg, #f9d423 0%, #ff4e50 100%); transform: scale(1.05); }
    .overlay {
        display: none; position: fixed; top:0; left:0;
        width:100vw; height:100vh; background: rgba(0,0,0,0.25);
        z-index: 10; animation: fadeIn 0.8s;
    }
    #surprise {
        display:none; position:fixed; top:50%; left:50%;
        transform:translate(-50%,-50%) scale(0.7);
        background: rgba(255,255,255,0.95);
        color: #ff4e50; font-size: 1.2em;
        border-radius: 24px;
        box-shadow: 0 8px 32px rgba(0,0,0,0.18);
        max-width: 90vw; width: 370px;
        padding: 32px 18px 24px 18px;
        z-index: 20; text-align: center;
        opacity: 0; transition: all 0.4s ease;
    }
    #surprise.show {
        transform: translate(-50%,-50%) scale(1);
        opacity: 1;
    }
    #surprise img {
        display: block; margin: 24px auto 0 auto;
        max-width: 90%; max-height: 220px;
        border-radius: 18px;
        box-shadow: 0 4px 16px rgba(0,0,0,0.12);
        border: 3px solid #ff4e50;
    }
    #surprise .gift-text {
        font-size: 1.25em; color: #ff4e50;
        margin-top: 15px; margin-bottom: 10px;
        font-weight: bold; letter-spacing: 1px;
    }
    #close-btn {
        margin-top: 18px; background: #ff4e50; color: #fff;
        border: none; border-radius: 20px; padding: 8px 28px;
        font-size: 1em; cursor: pointer;
        box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        transition: background 0.3s;
    }
    #close-btn:hover { background: #f9d423; color: #ff4e50; }
    .hearts {
        position: fixed; top: 0; left: 0;
        width: 100vw; height: 100vh;
        pointer-events: none; z-index: 0;
    }
    .heart-piece {
        position: absolute; font-size: 2em; opacity: 0.7;
        animation: heart-fall 5s linear forwards;
    }
    @keyframes heart-fall {
        0% { transform: translateY(-40px) scale(1) rotate(0deg);}
        80% { transform: translateY(80vh) scale(1.2) rotate(360deg);}
        100% { transform: translateY(100vh) scale(0.8) rotate(720deg);}
        opacity: 1;
    }
    .input-date, .input-place, .input-days {
        width: 80%; padding: 10px 14px; margin: 12px 0 8px 0;
        border: 2px solid #ff4e50; border-radius: 12px; font-size: 1em;
        outline: none; transition: border 0.2s; background: #fff8f0;
    }
    .input-date:focus, .input-place:focus, .input-days:focus {
        border: 2px solid #f9d423; background: #fff;
    }
    .input-btn, .choice-btn {
        background: linear-gradient(90deg, #ff4e50 0%, #f9d423 100%);
        color: #fff; border: none; font-weight: bold;
        cursor: pointer; box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        transition: background 0.3s, transform 0.2s;
    }
    .input-btn { padding: 8px 22px; border-radius: 18px; margin-left: 8px; margin-bottom: 8px; font-size: 1em; }
    .choice-group { margin: 14px 0 8px 0; display: flex; gap: 18px; flex-wrap: wrap; }
    .choice-btn { padding: 10px 28px; border-radius: 20px; font-size: 1.08em; }
    .input-btn:hover, .choice-btn:hover {
        background: linear-gradient(90deg, #f9d423 0%, #ff4e50 100%);
        transform: scale(1.05);
    }
</style>
</head>
<body>
<div class="hearts"></div>
<h1>Chúc mừng tốt nghiệp, em yêu! <span class="heart">❤️</span></h1>
<div class="message">
    Trước khi nhận quà, mình cùng chơi một trò nhỏ nhé!<br>
    Trả lời hết các câu hỏi bên dưới để mở quà bất ngờ nha!
</div>
<div id="quiz" style="max-width:400px;margin:30px auto;text-align:left;background:rgba(255,255,255,0.85);border-radius:18px;box-shadow:0 2px 12px rgba(0,0,0,0.08);padding:24px 18px;">
    <div id="q1">
        <b>1. Anh có đẹp trai không?</b><br>
        <div class="choice-group">
            <button class="choice-btn" onclick="nextQ(1,true)">Có 😎</button>
            <button class="choice-btn" onclick="nextQ(1,false)">Không 😝</button>
        </div>
    </div>
    <div id="q2" style="display:none;">
        <b>2. Ngày kỷ niệm của mình là ngày mấy? 🎂</b><br>
        <input type="text" id="dateInput" placeholder="" class="input-date">
        <button class="input-btn" onclick="nextQ(2)">Trả lời</button>
    </div>
    <div id="q3" style="display:none;">
        <b>3. Lúc tỏ tình với nhau ngồi ở đâu? 🪑</b><br>
        <input type="text" id="placeInput" placeholder="Nhập địa điểm" class="input-place">
        <button class="input-btn" onclick="nextQ(3)">Trả lời</button>
    </div>
    <div id="q4" style="display:none;">
        <b>4. Mình quen nhau bao nhiêu ngày rồi? 📅</b><br>
        <input type="number" id="daysInput" placeholder="Nhập số ngày" class="input-days">
        <button class="input-btn" onclick="nextQ(4)">Trả lời</button>
    </div>
    <div id="q5" style="display:none;">
        <b>5. Em có hay giận anh vô lý không?</b><br>
        <div class="choice-group">
            <button class="choice-btn" onclick="nextQ(5,true)">Có 😆</button>
            <button class="choice-btn" onclick="nextQ(5,false)">Không 😇</button>
        </div>
    </div>
    <div id="q6" style="display:none;">
        <b>6. Em có yêu anh nhiều không?</b><br>
        <div class="choice-group">
            <button class="choice-btn" onclick="nextQ(6,true)">Có 💖</button>
            <button class="choice-btn" onclick="nextQ(6,false)">Không 😜</button>
        </div>
    </div>
    <div id="q7" style="display:none;">
        <b>7. Lần gần nhất anh nói dối em là chuyện gì? 🤫</b><br>
        <input type="text" id="lieInput" placeholder="Nhập câu chuyện" class="input-place">
        <button class="input-btn" onclick="nextQ(7)">Trả lời</button>
    </div>
    <div id="promise" style="display:none; text-align:center; margin:24px 0; color:#ff4e50; font-size:1.15em;">
        💌 Anh hứa sẽ luôn thành thật và yêu em nhiều hơn nữa 💌
        <br><br>
        <button class="btn" id="giftBtnPromise" onclick="showSurprise()">Nhấn vào đây để nhận bất ngờ 🎉</button>
    </div>
</div>
<div class="overlay" id="overlay"></div>
<div id="surprise">
    🎓 Em là niềm tự hào lớn nhất của anh!<br>
    <span style="font-size:1.3em;">💖 Mãi bên nhau nhé! 💖</span>
    <br><br>
    <img src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4gHYSUNDX1BST0ZJTEUAAQEAAAHIAAAAAAQwAABtbnRyUkdCIFhZWiAH4AABAAEAAAAAAABhY3NwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAA9tYAAQAAAADTLQAAAAAAAAAAAAAAAAAAA..." alt="Món quà của anh">
    <div class="gift-text">Món quà của anh</div>
    <button id="close-btn" onclick="closeSurprise()">Đóng lại</button>
</div>

<script>
function nextQ(q, answer) {
    document.getElementById('q'+q).style.display = 'none';
    if(q === 1) {
        if(!answer) alert('Khịa anh thế là không được nha!');
        document.getElementById('q2').style.display = 'block';
    }
    if(q === 2) {
        let val = document.getElementById('dateInput').value.trim().replace(/[-.]/g,"/");
        if(val === "") { alert("Nhập ngày kỷ niệm đi em!"); document.getElementById('q2').style.display = 'block'; return;}
        if(val !== "16/04/2024" && val !== "16/4/2024") { alert("Sai rồi nha, ngày kỷ niệm là 16/04/2024 cơ!"); document.getElementById('q2').style.display = 'block'; return;}
        document.getElementById('q3').style.display = 'block';
    }
    if(q === 3) {
        let val = document.getElementById('placeInput').value.trim();
        if(val === "") { alert("Nhập địa điểm tỏ tình đi em!"); document.getElementById('q3').style.display = 'block'; return;}
        document.getElementById('q4').style.display = 'block';
    }
    if(q === 4) {
        let val = document.getElementById('daysInput').value.trim();
        if(val === "" || isNaN(val) || Number(val) <= 0) { alert("Nhập số ngày yêu nhau đi em!"); document.getElementById('q4').style.display = 'block'; return;}
        document.getElementById('q5').style.display = 'block';
    }
    if(q === 5) {
        if(answer) alert('Thừa nhận rồi nhé, anh sẽ không giận đâu 😘');
        document.getElementById('q6').style.display = 'block';
    }
    if(q === 6) {
        if(!answer) alert('Khịa anh nữa rồi, nhưng vẫn được nhận quà nha!');
        document.getElementById('q7').style.display = 'block';
    }
    if(q === 7) {
        let val = document.getElementById('lieInput').value.trim();
        if(val === "") { alert("Nhập câu chuyện đi em!"); document.getElementById('q7').style.display = 'block'; return;}
        document.getElementById('promise').style.display = 'block';
    }
}

function showSurprise() {
    document.getElementById('overlay').style.display = 'block';
    const s = document.getElementById('surprise');
    s.style.display = 'block';
    setTimeout(()=> s.classList.add('show'), 10);
}
function closeSurprise() {
    const s = document.getElementById('surprise');
    s.classList.remove('show');
    setTimeout(()=> {
        s.style.display = 'none';
        document.getElementById('overlay').style.display = 'none';
    }, 300);
}

// Heart generator liên tục
const colors = ['#ff4e50', '#f9d423', '#fff', '#ff6f91', '#f7cac9', '#92a8d1', '#b5ead7'];
const hearts = document.querySelector('.hearts');
function createHeart() {
    const piece = document.createElement('div');
    piece.classList.add('heart-piece');
    piece.style.left = Math.random() * 100 + 'vw';
    piece.style.animationDelay = '0s';
    piece.style.color = colors[Math.floor(Math.random() * colors.length)];
    piece.innerHTML = '❤️';
    hearts.appendChild(piece);
    setTimeout(()=> piece.remove(), 5000);
}
setInterval(createHeart, 300); // trái tim rơi liên tục
</script>
</body>
</html>
