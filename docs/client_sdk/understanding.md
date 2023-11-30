# Understanding RoCS Programming

This guide will help you understand the programming principles that drive the robot and its Client SDKs.

## Fundamentals

### Understanding the "IP"

The IP address of the GR-1 robot is used to uniquely identify and locate the robot on a network. The IP address allows other devices or applications to send data, commands, or requests to the GR-1 robot and receive responses in return. It is a fundamental component for establishing network connectivity and enabling communication with the GR-1 robot.

For how to configure the IP and set up connection to the robot, refer to chapter [Network Communication](https://fftai.github.io/#/networking?id=network-communication).

## How to Setup and Command GR-1 to Move

To gain a fundamental understanding of how to command GR-1 robot, follow these steps:

1. **Open a Python Interpreter:** Start by launching a Python interpreter in your preferred environment. Ensure that you have Python installed on your system.
   ```python
   $ python
   ```
2. **Import the RoCS SDK:** Import the RoCS SDK package to access its functionalities. This assumes you've successfully completed the RoCS SDK setup.
   ```python
   import rocs_client
   ```
3. **Initialize the RoCS Client:** Create an instance of the RoCS client, providing the necessary connection details. This step establishes a connection with the RoCS robot.
   ```python
   from rocs_client import Human
   ```
4. **Command the Robot:** Utilize the RoCS SDK to issue commands to the robot. For example, you can command the robot to stand using the `stand` method.
   ```python
   from rocs_client import Human

   from rocs_client.robot.human import ArmAction, HandAction, Motor

   # Connect to your robot using its IP address
   human = Human(host='192.168.9.17') # Replace '192.168.9.17' with your robot's actual IP

   # Activate remote control for the robot
   human.start() 

   # Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
   time.sleep(10) 

   # Instruct the robot to stand up
   human.stand() 

   ```

By following these steps, you'll have a solid foundation for interacting with the RoCS robot using the RoCS SDK. Explore additional commands and functionalities offered by the SDK to unleash the full potential of the RoCS robot in your applications.

### Asynchronous SDK Functions

The RoCS SDK primarily offers asynchronous functions that leverage Promises, allowing non-blocking execution and enhancing the overall responsiveness and performance of the application. Asynchronous functions, such as those using the `async` keyword and returning `Promise<any>`, enable the code to proceed with other tasks while waiting for robot operations to complete.

```
/**
 * Start the robot asynchronously.
 *
 * Initiates the robot startup asynchronously, allowing non-blocking execution.
 *
 * @return {Promise<any>} A Promise that resolves when the operation completes.
 */
public async startAsync(): Promise<any> {
    return super.http_request({
        method: "POST",
        url: "/robot/start",
    });
}

```

### Inspecting Robot State

The RoCS SDK provides functionalities to inspect various aspects of the robot's state, allowing developers to retrieve crucial information for monitoring and control. Below are key functions for inspecting the robot state:

#### 1. Get Joint Limits

```typescript
/**
 * Retrieve information about the joint limits of the robot.
 *
 * @return {Promise<any>} A Promise that resolves with the joint limit data.
 */
public async getJointLimits(): Promise<any> {
    return super.http_request({
        method: "GET",
        url: "/robot/join_limit",
    });
}

```

Use this function to obtain details about the robot's joint limits, which are essential for ensuring safe and controlled movements.

#### 2. Get Joint States

```typescript
/**
 * Retrieve the current joint states of the robot.
 *
 * @return {Promise<any>} A Promise that resolves with the current joint states.
 */
public async getJointStates(): Promise<any> {
    return super.http_request({
        method: "GET",
        url: "/robot/joint_states",
    });
}

```

This function allows you to fetch real-time information about the robot's current joint states, providing insights into its posture.

#### 3. Enable Debug State

```typescript
/**
 * Enable the debug state mode to receive periodic state updates from the robot.
 *
 * @param {number} frequency - The frequency of state updates (integer).
 * @return {Promise<any>} A Promise that resolves when the debug state mode is enabled.
 */
public async enableDebugState(frequency: number = 1): Promise<any> {
    return super.http_request({
        method: "GET",
        url: "/robot/enable_states_listen",
        params: {
            frequency: frequency,
        },
    });
}

```

Use this function to enable the debug state mode, allowing the robot to actively send periodic state updates. This is beneficial for real-time monitoring.

#### 4. Disable Debug State

```typescript
/**
 * Disable the debug state mode.
 *
 * @return {Promise<any>} A Promise that resolves when the debug state mode is disabled.
 */
public async disableDebugState(): Promise<any> {
    return super.http_request({
        method: "GET",
        url: "/robot/disable_states_listen",
    });
}

```

This function disables the debug state mode, stopping the periodic state updates from the robot. Integrate these functions into your application to inspect and monitor the robot's state effectively.

#### Robot State is a Message

The RoCS state message is a comprehensive JSON-formatted data package that encapsulates real-time information about the robot's status. This payload includes details about the robot's joint states, offering precise information about the positioning and configuration of its mechanical components. Additionally, the state message encompasses data related to the robot's base state, providing insights into its spatial orientation and location. Contact force information is also embedded, shedding light on the external forces acting on the robot. The RoCS state message serves as a rich source of information, empowering users to monitor and interact with the robot in real-time with a granular level of detail. For details, refer to [Server API](serverapi.md).

### Powering on the robot

To power on the RoCS robot, you can utilize the start method provided by the RobotBase class. This method sends an HTTP POST request to the "/robot/start" endpoint, triggering actions that include resetting, zeroing, and calibrating the device to its initial state. Before calling this method, ensure that the robot is in a safe position, with a charged battery and not connected to shore power. The start method returns a Promise, allowing you to handle the response or any potential errors accordingly. Below is an example of how to use the start method:

```typescript
// Assuming you have instantiated the RoCS robot
const rocsRobot = new RobotBase();

// Power on the robot
rocsRobot.start()
    .then(response => {
        console.log("Robot started successfully:", response);
        // Add any additional logic as needed
    })
    .catch(error => {
        console.error("Error starting the robot:", error);
        // Handle the error appropriately
    });

```

### Commanding the robot

Effectively control the robot by utilizing the diverse methods provided by the `Human` class, allowing you to dictate the robot's behavior and movements. The `stand` method, for instance, directs the robot to assume a standing posture in its current location, adjusting its stance accordingly. This command proves valuable when you want the robot to maintain an upright position without any lateral movement. Explore various other commands and functionalities available in the RoCS API, including adjusting joint positions, capturing video streams, and accessing system-level controls. Execute commands using either HTTP requests or WebSocket messages, ensuring seamless real-time communication with the robot. When issuing commands, prioritize safety measures and adhere to the recommended guidelines for optimal operation. Below is an example of how to command the RoCS robot to stand:

```typescript
await human.stand();

```

### Powering off the robot

To power off the robot, you can utilize the `stop` method provided by the `RobotBase` class. This method sends an HTTP POST request to the "/robot/stop" endpoint, initiating a controlled power-down sequence. It is important to prioritize the use of the `stop` command in emergency situations, as it causes the robot to lose power immediately. Before invoking this method, ensure the robot is in a safe position. The `stop` method returns a Promise, allowing you to handle the response or any potential errors accordingly. Below is an example of how to use the `stop` method:

```typescript
/ Assuming you have instantiated the RoCS robot
const rocsRobot = new RobotBase();

// Power off the robot
rocsRobot.stop()
    .then(response => {
        console.log("Robot stopped successfully:", response);
        // Add any additional logic as needed
    })
    .catch(error => {
        console.error("Error stopping the robot:", error);
        // Handle the error appropriately
    });
```
