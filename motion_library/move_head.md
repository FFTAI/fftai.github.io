# Move Head

To change the orientation of the robot's head, utilize the `head` method in the Motion Library. This method allows precise control over the head's movements, enabling you to adjust its position, tilt, and rotation as needed. By invoking the `head` function with appropriate parameters, you can seamlessly integrate head movements into your application, enhancing the robot's interaction capabilities. Explore the flexibility of the `head` method to create dynamic and expressive gestures, providing a more immersive experience in human-robot interactions.

It's crucial to call the `stand` method when finished with remote control to ensure a safe exit from the control mode.

```
import time
from rocs_client import Human

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Move head motion
human.head(roll=15, yaw=30, pitch=20)  # Adjust the roll, yaw and pitch angles as needed
```
