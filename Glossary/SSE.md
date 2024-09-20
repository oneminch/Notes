---
alias: Server-Sent Events
---

- Allows servers to push data to clients in real-time over a single [[HTTP]] connection.
- Useful for providing real-time data updates.
    - Live news / social media feeds
    - Live sports scores
    - System monitoring and logging
    - Progress updates
    - Notification systems
- **Features**
    - *Unidirectional* - Data flows only from server to client.
    - *Auto-reconnection* - Browsers automatically try to reconnect if the connection is lost.
    - *Event IDs* - Allows resuming the event stream from where it left off.
    - *Standard-based* - Uses regular HTTP, making it firewall-friendly.
- **How It Works**
    - Client establishes a connection to Server using the `EventSource` API.
    - Server keeps the connection open and sends events as they occur.
    - Client receives these events in real-time without having to poll the server.

```js
// Server
const app = express();

app.get('/events', (req, res) => {
    res.writeHead(200, {
        'Content-Type': 'text/event-stream',
        'Cache-Control': 'no-cache',
        'Connection': 'keep-alive'
    });

    const sendEvent = (data, eventType = 'message', id = null) => {
        let eventString = `Event: ${eventType}\n`;
        if (id) 
            eventString += `ID: ${id}\n`;
        eventString += `Data: ${JSON.stringify(data)}\n\n`;
        
        res.write(eventString);
    };

    // Send an event every 5 seconds
    const intervalId = setInterval(() => {
        const timestamp = new Date().toISOString();
        sendEvent({ status: 'update' }, 'update', timestamp);
    }, 5000);

    // Clean up on client disconnect
    req.on('close', () => {
        clearInterval(intervalId);
    });
});
```

```js
// Client
const eventSource = new EventSource('/events');

eventSource.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received event:', data);
};

eventSource.onerror = (error) => {
    console.error('EventSource failed:', error);
    eventSource.close();
};
```

- **Limitations**
    - No built-in binary support.
    - 6 concurrent connections per browser/domain.
    - Unidirectional (Server to Client only)
- **Best Practices**
    - Use [[HTTP|HTTPS]].
    - Implement proper [[authentication]] & [[Authentication#Authorization (AuthZ)|authorization]].