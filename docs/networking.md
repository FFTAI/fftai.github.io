<!--
Copyright (c) 2023 Boston Dynamics, Inc.  All rights reserved.

Downloading, reproducing, distributing or otherwise using the SDK Software
is subject to the terms and conditions of the Boston Dynamics Software
Development Kit License (20191101-BDSDK-SL).
-->

# Networking

All applications communicate with the GR-1 robot via a network connection using WebSocket. A solid understanding of WebSocket protocols is crucial for effective troubleshooting and ensuring robust, high-performance applications.

## WebSocket Connection

GR-1 relies on WebSocket communication as the primary protocol for interaction. WebSocket is a real-time, bidirectional protocol that allows your applications to exchange data with the robot in near real-time. This approach is highly suitable for scenarios that require low latency and responsiveness.

## Network Choice

GR-1 offers a variety of networking options to support a diverse set of applications and environments. Options include:

* **GR-1 as a connected peer**. Applications can be deployed on computers that physically connect to GR-1 via the rear RJ-45 port. This provides a reliable, high-rate communications link without infrastructure requirements, but limits where the application can be run.
* **GR-1 as a WiFi access point**. Applications with physical proximity to GR-1 can connect to the WiFi access point and communicate directly without any networking infrastructure.
* **GR-1 as a WiFi client**. Spot can join an existing WiFi network, and applications can also join the same WiFi network to talk to GR-1. This approach increases the possible range between application and GR-1, but attention needs to be paid to dead zones in the network, handoff times between access points, and other considerations.
* **GR-1 via custom communications links**. Custom communication links can act as a bridge between GR-1 and applications. These can be useful when the above cases are insufficient for network design.

While the application-layer protocol for the GR-1 API works across any IP-based network connection, the examples above show that networking choice can have a significant impact on the performance and reliability of an application as well as deployment strategies.

## Network Configuration

To establish a WebSocket connection with GR-1, you'll need to configure the network appropriately. Here are the key steps:

1. **GR-1 Network Connection:** Ensure that your GR-1 robot is connected to the network. GR-1 can be connected via Ethernet or Wi-Fi, depending on your requirements.
2. **IP Address or Hostname:** Determine the IP address or hostname of your GR-1 robot. You will use this information to connect to the robot product via WebSocket.
3. **Port Configuration:** WebSocket communication typically occurs over port 80 (HTTP) or port 443 (HTTPS). Ensure that the required port is accessible for WebSocket communication.
4. **Security Considerations:** While WebSocket is a secure protocol, it's important to implement proper security measures. Ensure that your WebSocket connection is secured with encryption (WSS) if sensitive data is being transmitted. Additionally, consider implementing authentication and authorization mechanisms to control access to the GR-1 robot.

## WebSocket Libraries

To communicate with GR-1 robot product via WebSocket, you'll need to use WebSocket libraries in your programming language of choice. These libraries facilitate the creation and management of WebSocket connections. Depending on your preferred programming language, choose a WebSocket library that is compatible with your application.

### Sample WebSocket Connection (Python)

Below is a simplified Python code snippet that demonstrates how to establish a WebSocket connection to your GR-1 robot product using the `websockets` library:

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

In this example, replace `"wss://your_gr1_ip_or_hostname:443/your_websocket_endpoint"` with the appropriate WebSocket URL of your GR-1 robot product. This URL should include the IP address or hostname, the port (443 for secure WebSocket), and the WebSocket endpoint you wish to communicate with.

## Error Handling

Robust applications need to handle errors when communicating with the GR-1 robot product over WebSocket. WebSocket libraries often provide mechanisms for error handling, allowing you to gracefully manage issues like connection failures or timeouts. Be sure to implement error-handling logic in your application to ensure reliability.

## Robot Discovery

To talk to GR-1, a client application needs to specify an IP address where a GR-1 is running. There are a number of possible options for doing this sort of robot discovery.

* **Fixed IP address**. This approach can be used reliably when connecting directly to Spot as a WiFi access point, or over ethernet. No name lookup infrastructure is required.
* **DNS name**. A DNS server (or HOSTS file) can be configured to statically point to a fixed IP address that GR-1 listens on, and the application specifies a DNS name to reach.
* **Custom Discovery mechanism**. Applications can develop custom approaches to map a specific GR-1 to an IP address, such as using a cloud-based discovery endpoint.
