

# Stand

The `stand` method in the Motion Library is used to command the robot to stand up from a sitting or resting position. After calling `start` and waiting for stabilization, you can issue the `stand` command to initiate the standing motion. Following the `stand` call, you can proceed with additional control commands or motion instructions.

```Python
import time
from rocs_client import Human

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Stand motion
human.stand()

```
