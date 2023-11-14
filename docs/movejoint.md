# Move Joints

The Motion Library provides the capability to control specific joints on the robot using the `move_joint` method. This method accepts a variable-length parameter, allowing simultaneous control of multiple joints. By leveraging the `Motor` object, which defines joint mapping relationships and parameter numbers through `human.motor_limits`, you can precisely manipulate the robot's joints.

To initiate joint movements, invoke the `move_joint` function and pass the relevant `Motor` objects as parameters. This flexibility enables intricate control over the robot's articulation, facilitating the execution of complex and coordinated motions. Note that the estimated delay for joint movements is around 2ms, ensuring responsiveness and accuracy in your robotic applications. Experiment with different joint configurations to achieve diverse and dynamic robot behaviors.

It's crucial to call the `stand` method when finished with remote control to ensure a safe exit from the control mode.

```Python
import time
from rocs_client import Human, Motor

# Connect to your robot using its IP address
human = Human(host='192.168.9.17')  # Replace '192.168.9.17' with your robot's actual IP

# Activate remote control for the robot
human.start()

# Wait for 10 seconds to ensure the robot's control system stabilizes after initiating the remote control command start().
time.sleep(10)

# Define Motor objects for joints
joint_motor_1 = Motor(no='1', angle=10, orientation='left')
joint_motor_2 = Motor(no='2', angle=20, orientation='right')
# Add more Motor objects as needed

# Move joints
human.move_joint(joint_motor_1, joint_motor_2)  # Add more joint_motor objects if controlling multiple joints

```
