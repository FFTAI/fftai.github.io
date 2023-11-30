# RoCS App Logic Flow

### Overall Control Logic

The RoCS app is built upon a robust control logic that orchestrates various functionalities seamlessly. At its core, the control logic is structured around Vue.js components and Vuex for state management.

**Vue.js Components:**
The app's user interface is constructed using Vue.js components. These components encapsulate specific features, such as navigation, user prompts, and control interfaces. The interaction between components is managed through Vue Router, facilitating a smooth transition between different views.

**State Management with Vuex:**
Vuex plays a pivotal role in maintaining the state of the application. The central store, organized into modules, holds critical information like the robot's connection status, control type, and other relevant data. Mutations and actions in Vuex ensure controlled and predictable state changes, providing a foundation for the app's dynamic behavior.

### How to Connect to the Robot

The initiation of a connection occurs at key moments, such as app startup or when a user triggers a relevant action. The app checks the server status on the robotic system using `robot.control_svr_status()`, which is a method of the robot obejct. Based on the result, the app proceeds with navigation or connects to the robotic system. Prior to this, the `robot` object should be initialized in the `mounted` lifecycle hook of the Vue component.

```
this.robot = new RocsClient(); // Assuming RocsClient is the class for robot communication
this.robot.on_connected(() => {
  this.robot.enable_debug_state(2);
});

```

After the connection is built, the robot can be started by sending a http request to the url: `/robot/sdk_ctrl/start`.

```javascript
   //Start robot
        getStartup() {
            this.$http.request({
                timeout: 60000,
                baseURL: process.env.VUE_APP_URL,
                method: "GET",
                url: "/robot/sdk_ctrl/start"
            }).then(response => {
                console.log('start-response', response)
            }).catch(error => {
                console.log('start-error', error)
            })
            setTimeout(() => {
                this.stateOn()
            }, 30000);
        },
```

### How to Manage Connection Status

In the RoCS app, connection management is crucial for maintaining a reliable and responsive interaction with the robotic system. It involves a combination of heartbeat checks, updating the Vuex store with connection status, and triggering actions based on the current state of the connection. This ensures that the application remains aware of the connection status and can adapt its behavior accordingly.

**Heartbeat Functionality:**
The app employs a heartbeat mechanism to continuously monitor the connection status between the app and the robotic system. This is achieved by periodically sending requests to the robotic system using the RoCS client library. Successful responses affirm an active connection, while failures trigger appropriate actions to handle a potential disconnection.

```javascript
// Import the `get_robot_type` function from the "rocs-client" library
import { get_robot_type } from "rocs-client";

export default {
  data() {
    return {
      intervalId: null, // Store the interval ID for later use
    };
  },
  created() {
    // When the component is created, start the heartbeat check
    this.startHeartbeat();
  },
  destroyed() {
    // When the component is destroyed, stop the heartbeat check
    this.stopHeartbeat();
  },
  methods: {
    startHeartbeat() {
      this.heartbeatCheck(); // Initial heartbeat check

      // Set up a periodic timer for heartbeat checks
      this.intervalId = setInterval(() => {
        // Execute the heartbeat check logic
        this.heartbeatCheck();
      }, 2000); // Heartbeat check every 2000 milliseconds (2 seconds)
    },
    stopHeartbeat() {
      // Stop the periodic heartbeat check
      clearInterval(this.intervalId);
    },
    heartbeatCheck() {
      // Extract the IP and port from the environment variable
      let ip = process.env.VUE_APP_URL.split("//")[1].split(":");
  
      // Call the `get_robot_type` function with the extracted IP and port
      get_robot_type({ host: ip[0], port: ip[1] })
        .then((res) => {
          console.log("gettype成功", res);
          // Check if the response indicates a successful and connected status
          if (res.status == 200 && res.data.msg == "ok")
            this.$store.commit("setConnected", true); // Set connection status to true
        })
        .catch((err) => {
          // If there is an error, set the connection status to false
          this.$store.commit("setConnected", false);
          console.log("gettype失败", err);
        });
    },
  },
};

```

In this code snippet, the `Heartbeat.js` mixin defines methods for starting and stopping the heartbeat checks. The `heartbeatCheck` function sends a request to the robotic system using the RoCS client library (`get_robot_type`). A successful response updates the connection status in the Vuex store using `this.$store.commit("setConnected", ...)`.

By integrating this mixin into relevant components, the RoCS app ensures continuous monitoring of the connection status.

**Dynamic Updates with Vuex:**
As mentioned earlier, the Vuex store, acting as the centralized state management system, holds information about the connection status. Mutations and actions in Vuex are employed to dynamically update the state based on the results of the heartbeat checks. This dynamic updating mechanism triggers UI changes, such as displaying connection icons or warnings, offering users immediate visual feedback.

**User-Friendly Feedback:**
In addition to dynamic updates, the RoCS app ensures that users receive clear and user-friendly feedback regarding the connection status. This may involve displaying visual indicators, such as connection icons, and triggering dialog boxes to communicate important messages, ensuring a seamless and transparent user experience.

## How to Command the Robot

Controlling the robot involves interacting with the `robot` object, which is an instance of the underlying robotic system. The process of commanding the robot is relatively straightforward. This object provides methods to command various actions such as walking, moving the head, controlling the body, and more. Below is an overview of how to use these methods to command the robot.

1. **Instantiate the Robot Object:**

   ```
   let robot = new Robot();

   ```
2. **Call Robot Methods to Command:**
   Once you have the `robot` object, you can call its methods to command different actions. For example:

   ```
   robot.walk(direction, velocity);
   robot.head(pitch, yaw);
   robot.body(squat, rotate_waist);
   robot.stand();
   robot.upper_body(arm_action, hand_action);
   robot.lower_body(lower_body_mode);
   // ... and other methods

   ```

These methods are used to control various aspects of the robot, such as walking, moving the head and body, changing posture, and performing upper and lower body actions.

### Walking

To make the robot move, the `walk` method is utilized. This method takes two parameters: `direction` and `velocity`. The `direction` parameter represents the angle of movement, and `velocity` determines the speed of the robot.

```
// Example: Move the robot forward
robot.walk(0, 1);

```

### Head Movement

Controlling the robot's head involves the `head` method. It allows adjustments to the pitch and yaw angles, providing flexibility in positioning the robot's head.

```
// Example: Tilt the head up
robot.head(45, 0);

```

### Body Control

The `body` method enables control over the robot's body. It takes parameters for squatting and rotating the waist.

```
// Example: Squat down
robot.body(0.5, 0);

```

### Upper Body Actions

To perform specific actions with the upper body, such as waving or grabbing, the `upper_body` method can be employed.

```
// Example: Wave left arm
robot.upper_body("LEFT_ARM_WAVE", "");

```

### Sending Commands

Commands are sent to the robot using the appropriate methods. It's crucial to consider the robot's current state and capabilities when issuing commands.

```
// Example: Send a custom command
robot.send_command("CUSTOM_COMMAND");

```

This is a basic guide to get you started with commanding the robot. Always refer to the robot's documentation for a comprehensive list of available commands and their parameters.

Remember to handle errors and ensure a stable connection to the robot before issuing commands.
