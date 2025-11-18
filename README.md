<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>P2P STUN Chat</title>
<style>
    body { font-family: Arial; background:#222; color:white; padding:20px; }
    textarea, input { width:100%; padding:10px; }
    button { padding:10px; width:100%; margin-top:10px; }
    #chat { width:100%; height:200px; background:#111; color:#0f0; padding:10px; overflow-y:auto; }
</style>
</head>
<body>

<h2>STUN Peer-to-Peer Chat</h2>

<div>
    <h3>Step 1: Host Chat</h3>
    <button onclick="createOffer()">Create Chat</button>
    <textarea id="offer" placeholder="Offer (send to your friend)"></textarea>
</div>

<div>
    <h3>Step 2: Join Chat</h3>
    <textarea id="answer" placeholder="Paste friend's Offer, then click Join"></textarea>
    <button onclick="createAnswer()">Join Chat</button>
</div>

<div>
    <h3>Step 3: Send This Back</h3>
    <textarea id="myAnswer" placeholder="Your answer to send back"></textarea>
</div>

<hr>

<div id="chat"></div>

<input id="msg" placeholder="Type message...">
<button onclick="sendMsg()">Send</button>

<script>
let pc = new RTCPeerConnection({
    iceServers: [{ urls:"stun:stun.l.google.com:19302" }]
});
let channel;

pc.ondatachannel = (event)=> {
    channel = event.channel;
    channel.onmessage = (e)=> show("Friend: " + e.data);
};

function createOffer() {
    channel = pc.createDataChannel("chat");
    channel.onmessage = (e)=> show("Friend: " + e.data);

    pc.createOffer().then(o=>{
        pc.setLocalDescription(o);
        offer.value = JSON.stringify(o);
    });
}

function createAnswer() {
    let offerObj = JSON.parse(answer.value);
    pc.setRemoteDescription(offerObj);

    pc.createAnswer().then(a=>{
        pc.setLocalDescription(a);
        myAnswer.value = JSON.stringify(a);
    });
}

function sendMsg() {
    let text = msg.value;
    channel.send(text);
    show("You: " + text);
    msg.value = "";
}

function show(txt) {
    chat.innerHTML += txt + "<br>";
}
</script>

</body>
</html>
