# Stop

In situations requiring an immediate halt of robot movements, the Motion Library provides the `stop` method. When invoked, this function triggers an emergency stop, bringing the robot to an instantaneous and complete halt with power-off. This command is crucial for ensuring the safety and security of both the robot and its surroundings.

To employ the emergency stop functionality, simply call the `stop` method within your application. This command is particularly useful in scenarios where rapid intervention is necessary to prevent potential hazards or unexpected behaviors. Incorporate the `stop` command strategically within your control logic to establish a robust and responsive safety mechanism for your robotic applications.

```Python
import time
from rocs_client import Human

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Trigger an emergency stop to halt all robot movements
human.stop()

```
