<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>AutoConnect STUN Chat</title>
<style>
    body { background:#222; color:white; font-family:Arial; padding:20px; }
    input, button { width:100%; padding:10px; margin-top:10px; font-size:16px; }
    #chat { height:250px; background:#000; color:#0f0; padding:10px; margin-top:15px; overflow-y:auto; }
</style>
</head>
<body>

<h2>Auto-Connect STUN Chat</h2>

<input id="room" placeholder="Enter Room ID">
<button onclick="joinRoom()">Join Room</button>

<div id="chat"></div>
<input id="msg" placeholder="Type message..." style="display:none;">
<button id="send" onclick="sendMsg()" style="display:none;">Send</button>

<script>
const SIGNAL = {};
let pc, channel;
let connected = false;

async function joinRoom() {
    let room = room.value.trim();
    if(!room) return alert("Enter a room ID");

    setupConnection(room);
}

function setupConnection(roomID) {
    pc = new RTCPeerConnection({
        iceServers: [{ urls: "stun:stun.l.google.com:19302" }]
    });

    pc.ondatachannel = e => {
        channel = e.channel;
        startChat();
    };

    channel = pc.createDataChannel("chat");
    startChat();

    pc.onicecandidate = e => {
        if (e.candidate) {
            SIGNAL[roomID].push(JSON.stringify(e.candidate));
        }
    };

    if (!SIGNAL[roomID]) SIGNAL[roomID] = [];

    autoSignal(roomID);
}

async function autoSignal(roomID) {
    const offer = await pc.createOffer();
    await pc.setLocalDescription(offer);
    SIGNAL[roomID].push(JSON.stringify(offer));

    let check = setInterval(async () => {
        if (connected) { clearInterval(check); return; }

        for (let data of SIGNAL[roomID]) {
            try {
                let obj = JSON.parse(data);

                if (obj.type === "offer" && !pc.remoteDescription) {
                    await pc.setRemoteDescription(obj);
                    const answer = await pc.createAnswer();
                    await pc.setLocalDescription(answer);
                    SIGNAL[roomID].push(JSON.stringify(answer));
                }

                if (obj.type === "answer" && pc.signalingState === "have-local-offer") {
                    await pc.setRemoteDescription(obj);
                }

                if (obj.candidate) {
                    await pc.addIceCandidate(obj);
                }

            } catch {}
        }
    }, 400);
}

function startChat() {
    channel.onopen = () => {
        connected = true;
        msg.style.display = "block";
        send.style.display = "block";
        show("Connected!");
    };

    channel.onmessage = e => show("Friend: " + e.data);
}

function sendMsg() {
    let text = msg.value.trim();
    if(!text) return;
    channel.send(text);
    show("You: " + text);
    msg.value = "";
}

function show(text) {
    chat.innerHTML += text + "<br>";
    chat.scrollTop = chat.scrollHeight;
}
</script>
</body>
</html>
