
# Understanding RoCS Programming

This guide will help you understand the programming principles the `rocs_client` SDK.

## Understand the communication methods between `rocs_client` and `GR-1`

First, we divide apis into two types: `continuous instructions` and `instantaneous instructions`.

1. Continuous instructions include but are not limited to robot walking, robot head movement and other instructions, including speed, Angle and other parameters control!   First of all, we divide api into two types according to continuous instruction and instantaneous instruction.   Continuous instruction includes single but not limited to robot walking, robot head movement and other commands containing speed, Angle and other parameter control instructions!
2. Instantaneous instructions are things like stand and zero and e-stop

### Continuous instructions

In the sdk coding and debugging stage, we packaged this type of instruction, and finally selected websocket for continuous execution of sending and listening.

Similar to the human.walk(angle, speed) directive! When controlling the motion of the 'GR-1' robot, our instructions must be continuous, we need to control its speed and Angle immediately, and get the correct feedback and response immediately, and even accept its active state push, so we must maintain a long link to ensure its reliability. Therefore, your walk command is guaranteed, and our control service ensures that the message is continuous and reliable!

Therefore, in the client sdk, your continuous instructions are transmitted in this way, and the instant state you need is also received in this communication mode!

We provide message monitoring, you can use the on_message function at the time of initialization to listen to the content that 'GR-1' actively pushes to you, including my current position and current state at the moment, as well as my real-time movement trajectory

### Instantaneous instructions

Then the corresponding instant command is to communicate with HTTP at that time! In this type of instruction, we may not need too much real-time feedback, we just need to read the state within the acceptable range. And this type of request is easier if you need to write again!

For example, the function human.start() puts' GR-1 'back to zero. Because it is equivalent to a preset instruction, you must care about the implementation of its internal plan, only need to know whether the execution is successful or not, and the reason for the error when the execution is not successful. So HTTP is a more reasonable way to communicate.

Similarly, the function human.stand() human.stop() is the same

