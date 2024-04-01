# Start

To activate the GR robot and establish a connection, you can use the `start()` function from the `rocs_client` library.

The `start` method in the Motion Library initiates the remote control mode for the robot, allowing external systems or programs to send control commands to the robot. After calling `start`, it's advisable to wait for a brief period (e.g., 10 seconds) to allow the robot's control system to stabilize. Following the `start` call, you can issue various motion commands or control instructions to the robot.

```Python
import time
from rocs_client import Human

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)
```
