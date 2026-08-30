```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">

  <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

  <meta name="theme-color" content="#05080d">

  <title>JARVIS V1 - Voice AI</title>

  <link rel="manifest" href="manifest.json">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      background:
        radial-gradient(circle at center, #0b2435 0%, #05080d 45%, #020407 100%);
      color: #eaf8ff;
      font-family: Arial, Helvetica, sans-serif;
      overflow-x: hidden;
    }

    .app {
      width: 100%;
      min-height: 100vh;
      padding: 20px;
      display: flex;
      flex-direction: column;
    }

    /* HEADER */

    .header {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 5px 0 15px;
    }

    .logo {
      font-size: 25px;
      font-weight: bold;
      letter-spacing: 4px;
    }

    .version {
      font-size: 11px;
      color: #5c8297;
      letter-spacing: 1px;
    }

    .status {
      font-size: 11px;
      color: #66d9ff;
      letter-spacing: 1px;
    }

    /* MAIN */

    .main {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 20px;
    }

    /* JARVIS CORE */

    .core-container {
      width: 245px;
      height: 245px;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
    }

    .core {
      width: 180px;
      height: 180px;
      border-radius: 50%;

      background:
        radial-gradient(
          circle,
          #baf4ff 0%,
          #4fd9ff 4%,
          #137eaa 14%,
          #092c40 36%,
          #03101a 63%,
          #02070b 100%
        );

      box-shadow:
        0 0 20px #2dd4ff,
        0 0 50px #168bb5,
        inset 0 0 35px #35d7ff;

      position: relative;

      animation: corePulse 3s infinite ease-in-out;
    }

    .core::before {
      content: "";
      position: absolute;

      width: 210px;
      height: 210px;

      top: -15px;
      left: -15px;

      border-radius: 50%;

      border: 1px solid rgba(91, 220, 255, 0.45);

      border-top-color: transparent;

      animation: rotate 8s linear infinite;
    }

    .core::after {
      content: "";

      position: absolute;

      width: 145px;
      height: 145px;

      top: 17px;
      left: 17px;

      border-radius: 50%;

      border: 1px dashed rgba(91, 220, 255, 0.5);

      animation: rotateReverse 5s linear infinite;
    }

    .core-center {
      position: absolute;

      width: 32px;
      height: 32px;

      background: #c7f7ff;

      border-radius: 50%;

      top: 74px;
      left: 74px;

      box-shadow:
        0 0 10px #ffffff,
        0 0 25px #4dddff,
        0 0 50px #2bcfff;

      animation: centerPulse 1.5s infinite;
    }

    /* LISTENING MODE */

    .listening .core {
      animation:
        corePulse 0.8s infinite ease-in-out,
        listeningGlow 0.8s infinite alternate;
    }

    .listening .core-center {
      transform: scale(1.3);
    }

    @keyframes corePulse {
      0%, 100% {
        transform: scale(1);
      }

      50% {
        transform: scale(1.035);
      }
    }

    @keyframes centerPulse {
      0%, 100% {
        transform: scale(1);
      }

      50% {
        transform: scale(1.18);
      }
    }

    @keyframes listeningGlow {
      from {
        filter: brightness(1);
      }

      to {
        filter: brightness(1.6);
      }
    }

    @keyframes rotate {
      from {
        transform: rotate(0deg);
      }

      to {
        transform: rotate(360deg);
      }
    }

    @keyframes rotateReverse {
      from {
        transform: rotate(360deg);
      }

      to {
        transform: rotate(0deg);
      }
    }

    /* TEXT */

    .title {
      font-size: 24px;
      font-weight: bold;
      letter-spacing: 1px;
    }

    .subtitle {
      max-width: 600px;
      text-align: center;
      color: #7895a8;
      font-size: 14px;
      line-height: 1.5;
      min-height: 42px;
    }

    /* BUTTONS */

    .controls {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      justify-content: center;
    }

    button {
      border: 1px solid #24536a;
      background: #08151f;
      color: #e9f8ff;

      padding: 13px 18px;

      border-radius: 13px;

      font-size: 14px;

      cursor: pointer;

      transition: 0.2s;
    }

    button:hover {
      background: #0d2635;
    }

    button:active {
      transform: scale(0.96);
    }

    .primary {
      background: #087da5;
      border-color: #45d8ff;
      box-shadow: 0 0 15px rgba(45, 212, 255, 0.25);
    }

    .primary:hover {
      background: #0b91bd;
    }

    button:disabled {
      opacity: 0.45;
      cursor: not-allowed;
    }

    /* CHAT */

    .chat {
      width: min(750px, 100%);

      background: rgba(5, 13, 21, 0.9);

      border: 1px solid #173446;

      border-radius: 18px;

      padding: 14px;

      max-height: 230px;

      overflow-y: auto;

      box-shadow: inset 0 0 30px rgba(20, 100, 130, 0.05);
    }

    .message {
      padding: 9px 4px;

      border-bottom: 1px solid #102532;

      font-size: 14px;

      line-height: 1.5;
    }

    .message:last-child {
      border-bottom: none;
    }

    .you {
      color: #72dcff;
    }

    .jarvis {
      color: #eaf8ff;
    }

    /* INPUT */

    .input-area {
      width: min(750px, 100%);

      display: flex;

      gap: 8px;
    }

    .input-area input {
      flex: 1;

      min-width: 0;

      background: #060c13;

      border: 1px solid #1a3b4d;

      color: white;

      border-radius: 12px;

      padding: 13px;

      outline: none;

      font-size: 14px;
    }

    .input-area input:focus {
      border-color: #35c9f5;
    }

    /* FOOTER */

    .footer {
      text-align: center;

      color: #40596a;

      font-size: 10px;

      padding-top: 15px;
    }

    /* MOBILE */

    @media (max-width: 600px) {

      .app {
        padding: 15px;
      }

      .logo {
        font-size: 21px;
      }

      .core-container {
        width: 220px;
        height: 220px;
      }

      .core {
        width: 160px;
        height: 160px;
      }

      .core-center {
        top: 64px;
        left: 64px;
      }

      .title {
        font-size: 21px;
      }

      button {
        padding: 12px 14px;
      }
    }
  </style>
</head>

<body>

<div class="app">

  <!-- HEADER -->

  <header class="header">

    <div>
      <div class="logo">
        JARVIS
      </div>

      <div class="version">
        VOICE AI • V1
      </div>
    </div>

    <div id="status" class="status">
      SYSTEM READY
    </div>

  </header>


  <!-- MAIN -->

  <main class="main">

    <!-- JARVIS CORE -->

    <div id="coreContainer" class="core-container">

      <div class="core">

        <div class="core-center"></div>

      </div>

    </div>


    <div class="title">
      Voice AI Assistant
    </div>


    <div id="subtitle" class="subtitle">

      Tap the microphone and speak.
      JARVIS will listen and respond with voice.

    </div>


    <!-- CONTROLS -->

    <div class="controls">

      <button
        id="micButton"
        class="primary">
        🎙️ Start Listening
      </button>

      <button
        id="stopButton">
        🔇 Stop Voice
      </button>

      <button
        id="clearButton">
        Clear Chat
      </button>

    </div>


    <!-- CHAT -->

    <div
      id="chat"
      class="chat">

      <div class="message jarvis">

        <b>JARVIS:</b>

        Voice system initialized.
        Say "Hello Jarvis" to begin.

      </div>

    </div>


    <!-- TEXT INPUT -->

    <div class="input-area">

      <input
        id="textInput"
        type="text"
        placeholder="Or type a message..."
        autocomplete="off"
      >

      <button id="sendButton">
        Send
      </button>

    </div>

  </main>


  <footer class="footer">

    JARVIS V1 • Voice Interface Prototype

  </footer>

</div>


<script>

/* =====================================================
   JARVIS V1
   VOICE SYSTEM
===================================================== */

const micButton =
  document.getElementById("micButton");

const stopButton =
  document.getElementById("stopButton");

const clearButton =
  document.getElementById("clearButton");

const sendButton =
  document.getElementById("sendButton");

const textInput =
  document.getElementById("textInput");

const chat =
  document.getElementById("chat");

const status =
  document.getElementById("status");

const subtitle =
  document.getElementById("subtitle");

const coreContainer =
  document.getElementById("coreContainer");


/* =====================================================
   CHAT
===================================================== */

function addMessage(sender, text) {

  const message =
    document.createElement("div");

  message.className =
    "message " +
    (sender === "You" ? "you" : "jarvis");

  const label =
    document.createElement("b");

  label.textContent =
    sender + ":";

  message.appendChild(label);

  message.appendChild(
    document.createTextNode(" " + text)
  );

  chat.appendChild(message);

  chat.scrollTop =
    chat.scrollHeight;
}


/* =====================================================
   TEXT TO SPEECH
===================================================== */

function speak(text) {

  if (!("speechSynthesis" in window)) {

    addMessage(
      "JARVIS",
      "Voice output is not supported by this browser."
    );

    return;

  }

  speechSynthesis.cancel();

  const voice =
    new SpeechSynthesisUtterance(text);

  voice.rate = 0.95;

  voice.pitch = 0.82;

  voice.volume = 1;

  voice.onstart = function() {

    status.textContent =
      "JARVIS SPEAKING";

  };

  voice.onend = function() {

    status.textContent =
      "SYSTEM READY";

  };

  speechSynthesis.speak(voice);

}


/* =====================================================
   JARVIS BRAIN - V1 DEMO
===================================================== */

function generateResponse(text) {

  const message =
    text.toLowerCase().trim();

  let response;


  if (
    message.includes("hello") ||
    message.includes("hi") ||
    message.includes("salam") ||
    message.includes("assalam")
  ) {

    response =
      "Hello. JARVIS is online and ready.";

  }

  else if (
    message.includes("who are you") ||
    message.includes("what are you")
  ) {

    response =
      "I am JARVIS, your voice AI assistant.";

  }

  else if (
    message.includes("time")
  ) {

    response =
      "The current time is " +
      new Date().toLocaleTimeString();

  }

  else if (
    message.includes("date") ||
    message.includes("today")
  ) {

    response =
      "Today is " +
      new Date().toLocaleDateString();

  }

  else if (
    message.includes("thank")
  ) {

    response =
      "You're welcome.";

  }

  else if (
    message.includes("your name")
  ) {

    response =
      "My name is JARVIS.";

  }

  else if (
    message.includes("how are you")
  ) {

    response =
      "All systems are operational.";

  }

  else {

    response =
      "I heard you say: " +
      text +
      ". My full offline AI brain will be connected in the next version.";

  }


  addMessage(
    "JARVIS",
    response
  );

  speak(response);

}


/* =====================================================
   SPEECH RECOGNITION
===================================================== */

const SpeechRecognition =
  window.SpeechRecognition ||
  window.webkitSpeechRecognition;


let recognition = null;

let listening = false;


if (SpeechRecognition) {

  recognition =
    new SpeechRecognition();

  recognition.lang =
    "en-US";

  recognition.interimResults =
    false;

  recognition.continuous =
    false;


  recognition.onstart =
    function() {

      listening = true;

      status.textContent =
        "LISTENING...";

      subtitle.textContent =
        "I'm listening. Speak now...";

      coreContainer.classList.add(
        "listening"
      );

      micButton.textContent =
        "🎙️ Listening...";

    };


  recognition.onresult =
    function(event) {

      const text =
        event.results[0][0].transcript;

      addMessage(
        "You",
        text
      );

      generateResponse(text);

    };


  recognition.onerror =
    function(event) {

      addMessage(
        "JARVIS",
        "Microphone error: " +
        event.error
      );

    };


  recognition.onend =
    function() {

      listening = false;

      status.textContent =
        "SYSTEM READY";

      subtitle.textContent =
        "Tap the microphone and speak.";

      coreContainer.classList.remove(
        "listening"
      );

      micButton.textContent =
        "🎙️ Start Listening";

    };

}


/* =====================================================
   MICROPHONE BUTTON
===================================================== */

micButton.onclick =
  function() {

    if (!recognition) {

      addMessage(
        "JARVIS",
        "Speech recognition is not supported in this browser. Please try Google Chrome."
      );

      return;

    }


    if (listening) {

      return;

    }


    try {

      recognition.start();

    }

    catch (error) {

      console.log(error);

    }

  };


/* =====================================================
   STOP VOICE
===================================================== */

stopButton.onclick =
  function() {

    if (
      recognition &&
      listening
    ) {

      recognition.stop();

    }


    if (
      "speechSynthesis"
      in window
    ) {

      speechSynthesis.cancel();

    }


    status.textContent =
      "SYSTEM READY";

  };


/* =====================================================
   CLEAR CHAT
===================================================== */

clearButton.onclick =
  function() {

    chat.innerHTML = "";

  };


/* =====================================================
   TEXT MESSAGE
===================================================== */

function sendTextMessage() {

  const text =
    textInput.value.trim();


  if (!text) {

    return;

  }


  addMessage(
    "You",
    text
  );


  textInput.value =
    "";


  generateResponse(text);

}


sendButton.onclick =
  sendTextMessage;


/* ENTER KEY */

textInput.addEventListener(
  "keydown",
  function(event) {

    if (event.key === "Enter") {

      sendTextMessage();

    }

  }
);


/* =====================================================
   BROWSER SUPPORT MESSAGE
===================================================== */

if (!SpeechRecognition) {

  status.textContent =
    "VOICE CHECK";

  subtitle.textContent =
    "Voice recognition is not available in this browser. Try Chrome on Android or Chrome desktop.";

  micButton.disabled =
    true;

}


/* =====================================================
   WELCOME
===================================================== */

console.log(
  "JARVIS V1 Voice System Initialized"
);

</script>

</body>
</html>
```
