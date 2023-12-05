# Move Arms and Hands

The `upper_body` method in the Motion Library is used to command the robot's upper limbs, including the arms and hands. Below is a sample code snippet demonstrating the usage of the `upper_body` method:

```Python
port time
from rocs_client import Human, ArmAction, HandAction

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Execute preset commands for the upper body
human.upper_body(arm=ArmAction.LEFT_ARM_WAVE)  # Example: Wave the left arm
time.sleep(2)  # Wait for 2 seconds between actions

human.upper_body(arm=ArmAction.TWO_ARMS_WAVE)  # Example: Wave both arms
```


The `upper_body` method is called to execute preset commands for the upper limbs. The `ArmAction` and `HandAction` enumerations provide specific arm and hand preset commands, respectively. You can choose from various arm and hand actions, such as waving and trembling, by specifying the appropriate action in the `upper_body` method.

After calling `start` and waiting for stabilization, you can issue the `upper_body` commands to control the robot's upper limbs. Following the `upper_body` calls, you can proceed with additional control commands or motion instructions. 

It's crucial to call the `stand` method when finished with remote control to ensure a safe exit from the control mode.
