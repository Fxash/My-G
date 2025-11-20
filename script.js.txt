// ===== POEM ===== //
const poemText =
"Before this world knew your smile 😊,\n" +
"My heart had already been waiting for you ❤️.\n\n" +

"Ashley loves you with a fire that never fades 🔥,\n" +
"A love so deep, even time bows before it 💞.\n\n" +

"Through storms 🌧️, laughter 😂, whispers 💫 and scars,\n" +
"I choose you — yesterday, today and forever ♾️.\n\n" +

"No matter the miles, the noise, the challenges,\n" +
"It's always you. Only you ❤️.\n\n" +

"C & A — written in the sky ☁️, sealed in the heart 💘.\n" +
"Two souls, one destiny ✨.\n\n" +

"Welcome, my love 💋.\n" +
"Our forever starts here ❤️.";

let i = 0;
function typePoem() {
    const box = document.getElementById("poem-text");
    if (i < poemText.length) {
        box.innerHTML += poemText.charAt(i);
        i++;
        setTimeout(typePoem, 50);
    }
}

// ===== Q&A DATA ===== //
const data = {
    favColor: "Pink 🌸",
    favFood: "Chipo/Fries and Smokies 🍟🌭",
    favSong: "Hold You So Tight — Ed Sheeran & Burna Boy 🎶",
    favPlace: "Ashley’s arms 😌❤️",
    hobby: "Hiking ⛰️",
    birthday: "29th September 2002 🎂",
    flower: "Red roses 🌹",
    familyCount: "She comes from a loving family ❤️",
    siblings: "Her brother Philip and her sister Elizabeth Cherop",
    parents: "Her mother Priscillas Amutale and father Mark Kandie",
    herName: "Consolata Jepchumba ❤️",
    nicknames: "Kafatty, Kapumpum, Kanono, Hottie 😘",
    bestNight: "The day her mom went to Kitale and you two were left alone 😉💖",
    worstNight: "The night you sneaked out and got caught 😂",
    bestDay: "The day we hung out in Eldy with 0 disturbance 😍",
    challenges: "The time her mum tried to separate you because of defamation 😔",
    funnyMoment: "When Tarus thought he'd catch the lovebirds… little did he know 😂😂"
};

// ===== RESPOND FUNCTION ===== //
function respond(q) {
    q = q.toLowerCase().trim();

    if (q.includes("color") || q.includes("colour")) return data.favColor;
    if (q.includes("food") || q.includes("eat")) return data.favFood;
    if (q.includes("song") || q.includes("music")) return data.favSong;
    if (q.includes("place")) return data.favPlace;
    if (q.includes("hobby") || q.includes("fun")) return data.hobby;
    if (q.includes("birthday") || q.includes("born")) return data.birthday;
    if (q.includes("flower")) return data.flower;
    if (q.includes("family") || q.includes("how many")) return data.familyCount;
    if (q.includes("siblings") || q.includes("brother") || q.includes("sister")) return data.siblings;
    if (q.includes("parents") || q.includes("mother") || q.includes("father") || q.includes("mom") || q.includes("dad")) return data.parents;
    if (q.includes("name")) return data.herName;
    if (q.includes("nickname")) return data.nicknames;
    if (q.includes("best night")) return data.bestNight;
    if (q.includes("worst night")) return data.worstNight;
    if (q.includes("best day")) return data.bestDay;
    if (q.includes("challenge")) return data.challenges;
    if (q.includes("funny")) return data.funnyMoment;

    return "Hmm my love, I don’t know that yet 🥺💗";
}

// ===== MAIN ===== //
window.onload = () => {
    typePoem();

    // Enter Button
    document.getElementById("enter-btn").onclick = () => {
        document.getElementById("intro-screen").style.display = "none";
        document.getElementById("main-content").style.display = "block";
    };

    // Ask Button
    document.getElementById("ask-btn").onclick = () => {
        const box = document.getElementById("chatbox");
        const q = document.getElementById("question").value;
        if (!q.trim()) return;
        box.innerHTML += `<div class="msg user">You: ${q}</div>`;
        box.innerHTML += `<div class="msg bot">💕 ${respond(q)}</div>`;
        document.getElementById("question").value = "";
        box.scrollTop = box.scrollHeight;
    };

    // Microphone Button
    const micBtn = document.getElementById("mic-btn");
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    const recog = new SpeechRecognition();
    recog.lang = "en-US";
    recog.continuous = false;
    recog.interimResults = false;

    micBtn.onclick = () => {
        recog.start();
        micBtn.innerHTML = "🎙️ Listening...";
    };

    recog.onresult = (event) => {
        const text = event.results[0][0].transcript;
        document.getElementById("question").value = text;
        micBtn.innerHTML = "🎤";
        document.getElementById("ask-btn").click();
    };

    recog.onerror = () => {
        micBtn.innerHTML = "🎤";
    };
};

