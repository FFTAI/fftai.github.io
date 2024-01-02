# Network Communication

To initiate communication with the GR robot, all applications leverage a network connection employing WebSocket and HTTP protocols. A comprehensive understanding of these protocols is imperative for effective troubleshooting and ensuring the robust functionality of applications.

RoCS APIs manage two categories of instructions: continuous and instantaneous, exchanged with the GR robot. Continuous instructions utilize WebSocket for real-time communication, ensuring immediate feedback and reliability. Conversely, instantaneous instructions use HTTP for simpler communication when real-time feedback is not essential. The SDK provides tools for actively monitoring pushed messages and handling different instruction types accordingly.

## WebSocket Connection

The primary mode of communication for GR robot is WebSocket, a real-time, bidirectional protocol facilitating near real-time data exchange between applications and the robot. This approach is particularly suitable for scenarios requiring low latency and high responsiveness, such as those involving continuous instructions.

**Continuous Instructions:**

- Actions like robot walking and head movement, which require real-time control of parameters like speed and angle, fall under continuous instructions.
- During the SDK coding and debugging stage, continuous instructions are packaged, and WebSocket is selected for continuous execution through sending and listening.
- Examples of continuous instructions include commands like `human.walk(angle, speed)`, where maintaining a long-lived connection is crucial for immediate feedback, response, and active state push from the GR robot.
- The SDK includes message monitoring, allowing users to utilize the `on_message` function during initialization to listen actively to pushed content from the GR, such as the current position, state, and real-time movement trajectory.

### WebSocket Libraries

To communicate with the GR robot via WebSocket, you need WebSocket libraries in your programming language of choice. These libraries facilitate the creation and management of WebSocket connections. Choose a WebSocket library compatible with your preferred programming language.

### Sample WebSocket Connection (Python)

Below is a simplified Python code snippet demonstrating how to establish a WebSocket connection to your GR robot using the `websockets` library:

```python
import asyncio
import websockets

async def connect_to_gr1():
    uri = "wss://your_gr1_ip_or_hostname:443/your_websocket_endpoint"

    async with websockets.connect(uri) as websocket:
        # Perform WebSocket operations here
        await websocket.send("Hello, GR-1!")
        response = await websocket.recv()
        print(f"GR-1 says: {response}")

if __name__ == "__main__":
    asyncio.get_event_loop().run_until_complete(connect_to_gr1())
```

In this example, replace `wss://your_gr1_ip_or_hostname:443/your_websocket_endpoint` with the appropriate WebSocket URL of your GR robot product. This URL should include the IP address or hostname, the port (443 for secure WebSocket), and the WebSocket endpoint you wish to communicate with.

## HTTP Connection

**Instantaneous Instructions:**

- Instantaneous instructions, like `human.start()`, communicate via HTTP at that moment.
- These commands may not necessitate real-time feedback, and reading the state within an acceptable range is sufficient.
- HTTP communication is chosen for instantaneous instructions as it offers a more straightforward way to communicate when real-time feedback is not critical.
- Examples of instantaneous instructions include functions like `human.stand()` and `human.stop()`, where the focus is on the success or failure of execution and error reasons in case of failure.

### HTTP Libraries

Similar to WebSocket communication, establishing communication with the GR robot via HTTP requires the use of HTTP libraries in your chosen programming language. These libraries simplify the handling of HTTP requests and responses, making it easier to interact with the GR robot's Server APIs.

### Sample HTTP Connection (Python)

Here's a basic Python code snippet that illustrates how to initiate an HTTP connection to your GR robot using the `requests` library:

```Python
import requests

def send_http_request():
    url = "http://your_gr1_ip_or_hostname:80/your_http_endpoint"

    # Customize the payload as needed for your specific HTTP request
    payload = {"key": "value"}

    try:
        response = requests.post(url, json=payload)
        response.raise_for_status()

        # Process the HTTP response here
        print(f"HTTP Response: {response.text}")

    except requests.exceptions.RequestException as err:
        print(f"Error: {err}")

if __name__ == "__main__":
    send_http_request()

```

In this example, replace `http://your_gr1_ip_or_hostname:80/your_http_endpoint` with the appropriate HTTP URL of your GR robot. This URL should include the IP address or hostname, the port (80 for standard HTTP), and the specific HTTP endpoint you want to communicate with. Customize the payload as needed for your specific HTTP request.

Choose an HTTP library compatible with your programming language to streamline your interactions with the GR robot's Server API through the HTTP protocol.

## Network Choice

GR offers various networking options to support diverse applications and environments. Options include:

* **GR as a connected peer:** Deploy applications on computers physically connected to GR via the rear RJ-45 port. This provides a reliable, high-rate communications link without infrastructure requirements but limits the application's deployment location.
* **GR as a WiFi access point:** Applications in physical proximity to GR can connect to the WiFi access point and communicate directly without any networking infrastructure.
* **GR as a WiFi client:** GR can join an existing WiFi network, allowing applications to communicate over the same WiFi network. This increases the possible range between application and GR but requires attention to network dead zones and handoff times between access points.
* **GR via custom communications links:** Custom communication links can act as a bridge between GR and applications, useful when standard cases are insufficient for network design.

While the application-layer protocol for the GR API works across any IP-based network connection, the examples above highlight that networking choice significantly impacts application performance, reliability, and deployment strategies.

## Network Configuration

To establish a WebSocket connection with GR, configure the network appropriately. Key steps include:

1. **GR Network Connection:** Ensure GR is connected to the network via Ethernet or Wi-Fi, depending on requirements.
2. **IP Address or Hostname:** Determine the IP address or hostname of your GR robot for WebSocket connection.
3. **Port Configuration:** WebSocket communication typically occurs over port 80 (HTTP) or port 443 (HTTPS). Ensure the required port is accessible for WebSocket communication.
4. **Security Considerations:** Implement proper security measures, such as encryption (WSS) for sensitive data transmission. Consider authentication and authorization mechanisms to control access to the GR robot.

## Error Handling

Robust applications communicating with the GR robot over WebSocket must handle errors gracefully. WebSocket libraries often provide mechanisms for error handling, allowing for the graceful management of issues like connection failures or timeouts. Implement error-handling logic in your application to ensure reliability.

## Robot Discovery

To communicate with GR, a client application must specify the IP address where a GR is running. Possible options for robot discovery include:

- **Fixed IP address**: Reliable when connecting directly to GR as a WiFi access point or over Ethernet. No name lookup infrastructure is required.
- **DNS name:** Configure a DNS server or HOSTS file to statically point to a fixed IP address that GR listens on, specifying a DNS name to reach.
- **Custom Discovery mechanism:** Develop custom approaches, such as using a cloud-based discovery endpoint, to map a specific GR to an IP address.
