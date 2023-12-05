# Tremble Fingers

For a gesture like trembling the fingers, use the `upper_body()` function with `HandAction`.

It's crucial to call the `stand` method when finished with remote control to ensure a safe exit from the control mode.

```Python
import time
from rocs_client import Human, ArmAction, HandAction


# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Execute preset commands for trembling the fingers
human.upper_body(hand=HandAction.TREMBLE)  
```
