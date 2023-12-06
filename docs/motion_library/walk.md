# Walk

The `walk` method in the Motion Library is used to command the robot to perform walking motions. Below is a sample code
snippet demonstrating the usage of the `walk` method to command the robot to walk forward at a speed of 0.1.

```Python
import time
from rocs_client import Human

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Walk motion
human.walk(0, 0.1)
```

The `walk` method is called to command the robot to perform walking motions. The `angle` parameter represents the angle
or direction of the walk, and the `speed` parameter controls the walking speed.

After calling `start` and waiting for stabilization, you can issue the `walk` command to initiate the walking motion.
Following the `walk` call, you can proceed with additional control commands or motion instructions.

It's crucial to call the `stand` method when finished with remote control to ensure a safe exit from the control mode.

<video controls>
  <source src="../_media/walk.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
