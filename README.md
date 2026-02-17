<!DOCTYPE html>
<html>
<head>
    <title>Ticket Conversation - Bonic Support</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0f0f0f; }
    </style>
</head>

<body class="text-white font-sans">

<div class="max-w-3xl mx-auto py-10 px-6">

    <h1 class="text-2xl font-bold mb-2">Ticket Conversation</h1>
    <p id="ticketInfo" class="text-gray-400 mb-6"></p>

    <div id="chatBox" class="bg-gray-900 rounded-2xl p-6 h-96 overflow-y-auto space-y-4">
    </div>

    <div class="mt-4 flex gap-3">
        <input id="messageInput" type="text"
            placeholder="Type your message..."
            class="flex-1 p-3 rounded-xl bg-gray-800 border border-gray-700">
        <button onclick="sendMessage()"
            class="bg-orange-500 hover:bg-orange-600 px-6 rounded-xl">
            Send
        </button>
    </div>

    <button onclick="closeTicket()"
        class="mt-6 w-full bg-red-600 hover:bg-red-700 p-3 rounded-xl">
        Close Ticket
    </button>

</div>

<script>
    const urlParams = new URLSearchParams(window.location.search);
    const ticketID = urlParams.get('id');
    const description = localStorage.getItem(ticketID);

    document.getElementById("ticketInfo").innerText =
        "Ticket ID: " + ticketID + " | Status: Open";

    const chatBox = document.getElementById("chatBox");

    function addMessage(sender, text) {
        const msg = document.createElement("div");
        msg.className = sender === "customer"
            ? "text-right"
            : "text-left";

        msg.innerHTML = `
            <div class="inline-block px-4 py-2 rounded-xl 
                ${sender === "customer" ? "bg-orange-500" : "bg-gray-700"}">
                ${text}
            </div>
        `;

        chatBox.appendChild(msg);
        chatBox.scrollTop = chatBox.scrollHeight;
    }

    addMessage("customer", description);

    function sendMessage() {
        const input = document.getElementById("messageInput");
        const text = input.value.trim();
        if (!text) return;

        addMessage("support", text);
        input.value = "";
    }

    function closeTicket() {
        document.getElementById("ticketInfo").innerText =
            "Ticket ID: " + ticketID + " | Status: Closed";
    }
</script>

</body>
</html>
# chat.html
