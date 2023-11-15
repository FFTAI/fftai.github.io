
# Understanding RoCS Programming

This guide will help you understand the programming principles that drive RoCS and the RoCS Python SDK.

<!--ts-->

* [Fundamental Robot Services](#fundamental-robot-services)
  * [Understanding the &#34;id&#34; command](#understanding-the-id-command)
  * [Listing Services](#listing-services)
* [Understanding How to Setup and Command RoCS to Move](#how-to-setup-and-command-RoCS-to-move)
  * [Create the SDK object](#create-the-sdk-object)
  * [Create a Robot object](#create-a-robot-object)
  * [Retrieve the Robot ID](#retrieve-the-robot-id)
  * [Blocking vs. Asynchronous RoCS Python SDK functions](#blocking-vs-asynchronous-RoCS-python-sdk-functions)
  * [Inspecting robot state](#inspecting-robot-state)
    * [Services and Authentication](#services-and-authentication)
    * [Retrieving Robot State](#retrieving-robot-state)
    * [Robot State was a Message, Messages are defined by Protobufs](#robot-state-was-a-message-messages-are-defined-by-protobufs)
  * [Capture and View Camera images](#capture-and-view-camera-images)
  * [Configuring &#34;Motor Power Authority&#34; (software E-Stop)](#configuring-motor-power-authority-software-e-stop)
    * [Create and register an E-Stop Endpoint](#create-and-register-an-e-stop-endpoint)
    * [Clear the E-Stop](#clear-the-e-stop)
  * [Powering on the robot](#powering-on-the-robot)
  * [Establishing timesync](#establishing-timesync)
  * [Commanding the robot](#commanding-the-robot)
  * [Powering off the robot](#powering-off-the-robot)

<!--te-->

## Fundamental Robot Services

### Understanding the "id" command

The "id" command is one of the simplest RoCS commands, so it's useful to understand how it works, since every command to RoCS performs many of the same basic functions.

Specify the verbose flag with `--verbose` , and you'll get a lot of information! We'll explain the pieces...

```
$ python -m RoCS.client --verbose 192.168.80.3 id
2020-03-26 17:30:27,571 - DEBUG - Creating standard Sdk, cert glob: "None"
2020-03-26 17:30:27,610 - DEBUG - Created client for robot-id
2020-03-26 17:30:27,615 - DEBUG - Created channel to 192.168.80.3 at port 443 with authority id.RoCS.robot
...
```

The first output line creates a RoCS SDK object.  All RoCS API programs start this way.

Note that the output text itself demonstrates RoCS' use of Python's [logging facility](https://docs.python.org/3/library/logging.html), we recommend you perform your logging with the same.

The third line creates a `client` of RoCS's `robot-id` service. The RoCS API exposes on-robot capabilities via a set of network-accessible services - similar to a [microservice](https://en.wikipedia.org/wiki/Microservices) architecture.

The final line of output above shows the command initiating a gRPC channel to RoCS.  All communication to the robot is over a secure HTTPS connection.  RoCS API uses [gRPC](https://grpc.io) as its underlying RPC (Remote Procedure Call) transport. gRPC is a high-performance  networking connection for services which supports a wide variety of programming environments. gRPC uses [Protocol Buffers](https://developers.google.com/protocol-buffers/) as the messaging format, which has a compact over-the-wire representation and supports backwards and forwards compatibility.

```
2020-03-26 17:30:27,616 - DEBUG - blocking request: b'/RoCS.api.RobotIdService/GetRobotId'
header {
  request_timestamp {
    seconds: 1585258227
    nanos: 616570624
  }
  client_name: "RoCSClientbblank02:__main__.py-28906"
}
```

In the above output, a blocking `GetRobotId` RPC can be seen being made to the `RoCS.api.RobotIdService`.

Finally, the RobotIdService responds to the GetRobotId RPC with a response including information about the robot.

```
2020-03-26 17:30:27,650 - DEBUG - response: b'/RoCS.api.RobotIdService/GetRobotId'
header {
  request_header {
    request_timestamp {
      seconds: 1585258227
      nanos: 616570624
    }
    client_name: "RoCSClientbblank02:__main__.py-28906"
  }
  request_received_timestamp {
    seconds: 1585258226
    nanos: 224952738
  }
  response_timestamp {
    seconds: 1585258226
    nanos: 224990830
  }
  error {
    code: CODE_OK
  }
  request {
    type_url: "type.googleapis.com/RoCS.api.RobotIdRequest"
    value: "\n6\n\014\010\363\275\364\363\005\020\200\276\200\246\002\022&RoCSClientbblank02:__main__.py-28906"
  }
}
robot_id {
  serial_number: "beta-BD-90490007"
  species: "RoCS"
  version: "V3"
  software_release {
    version {
      major_version: 2
    }
    changeset_date {
      seconds: 1583941992
    }
    changeset: "b11205d698e"
    install_date {
      seconds: 1583953617
    }
  }
  nickname: "beta29"
  computer_serial_number: "02-19904-9903"
}
```

### Listing services

The following command lists all of the services available on the robot.  Note the `robot-id` service is listed, which we just used in the previous section.  Services are what you communicate with on RoCS, use them to issue commands, retrieve information, etc.

```
$ python -m RoCS.client --user user --password password 192.168.80.3 dir list
name                             type                                              authority                                   tokens
------------------------------------------------------------------------------------------------------------------------------------
auth                             RoCS.api.AuthService                            auth.RoCS.robot
directory                        RoCS.api.DirectoryService                       api.RoCS.robot                              user
directory-registration           RoCS.api.DirectoryRegistrationService           api.RoCS.robot                              user
estop                            RoCS.api.EstopService                           estop.RoCS.robot                            user
graph-nav-service                RoCS.api.graph_nav.GraphNavService              graph-nav.RoCS.robot                        user
image                            RoCS.api.ImageService                           api.RoCS.robot                              user
lease                            RoCS.api.LeaseService                           api.RoCS.robot                              user
...
```

See the Concept documents for more details about [RoCS&#39;s API Architecture](../concepts/README.md).

## How to Setup and Command GR-1 to Move

It is useful to run GR-1 from the command line to understand the basics for commanding GR-1.

Start up a python interpreter and import the client package - this should work assuming you've successfully completed our [RoCS Python SDK Quickstart](./quickstart.md).

```sh
$ python
Python 3.6.8 (default, Jan 14 2019, 11:02:34)
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import RoCS.client
```

### Create the SDK object

All RoCS API programs start by creating an SDK object with a client name argument. The client name is used to help with debugging, and does not have any semantic information - so use whatever string is helpful for you.

```python
>>> sdk = RoCS.client.create_standard_sdk('understanding-RoCS')
```

### Create a robot object

To retrieve the robot id like we did in [RoCS Python SDK Quickstart](./quickstart.md) we'll first need to create a `robot` object, using its network address as an argument. In this example, we only create one `robot` object, but it is possible to create and control multiple robots in the same program with the RoCS API.

```python
>>> robot = sdk.create_robot('192.168.80.3')
```

### Retrieve the Robot ID

As discussed earlier, RoCS exposes its capability via a number of services. The RoCS Python API has a corresponding set of clients for each service, which are created off of the robot object.

Let's create a `RobotIdClient` of the `robot-id` service, and then retrieve id information:

```python
>>> id_client = robot.ensure_client('robot-id')
>>> id_client.get_id()
serial_number: "beta-BD-90490007"
species: "RoCS"
...
```

### Blocking vs. Asynchronous RoCS Python SDK functions

The `get_id()` call above is blocking - it will not complete until after the RPC completes. It is possible to tweak parameters for the call, such as a timeout for how long to wait. The following example sets a too short timeout and fails...

```
>>> id_client.get_id(timeout=0.0001)
Traceback (most recent call last):
  File "/mnt/c/RoCS_v2_0/bblank_RoCS_v2_0_env/lib/python3.6/site-packages/RoCS/client/common.py", line 290, in call
    response = rpc_method(request, **kwargs)
  File "/mnt/c/RoCS_v2_0/bblank_RoCS_v2_0_env/lib/python3.6/site-packages/grpc/_channel.py", line 826, in __call__
    return _end_unary_response_blocking(state, call, False, None)
  File "/mnt/c/RoCS_v2_0/bblank_RoCS_v2_0_env/lib/python3.6/site-packages/grpc/_channel.py", line 729, in _end_unary_response_blocking
    raise _InactiveRpcError(state)
grpc._channel._InactiveRpcError: <_InactiveRpcError of RPC that terminated with:
        status = StatusCode.DEADLINE_EXCEEDED
        details = "Deadline Exceeded"
        debug_error_string = "{"created":"@1585323526.280242100","description":"Error received from peer ipv4:192.168.80.3:443","file":"src/core/lib/surface/call.cc","file_line":1056,"grpc_message":"Deadline Exceeded","grpc_status":4}"
>
```

In addition to blocking calls, clients support non-blocking asynchronous calls. This can be useful in high performance applications where a thread of execution can not stall waiting for an RPC to complete. Python's [futures](https://docs.python.org/3/library/concurrent.futures.html#future-objects) architecture is used as the underpinning of asynchronous communication.  See the [get_robot_state_async programming example](../../python/examples/get_robot_state_async/README.md) for how to use these functions.

Let's make an asynchronous call for the robot id and wait for the result from the returned future object:

```python
>>> fut = id_client.get_id_async()
>>> fut.result()
serial_number: "beta-BD-90490007"
species: "RoCS"
...
```

### Inspecting robot state

The `robot-state` service contains dynamic information about the robot such as location, battery status, etc.

#### Services and Authentication

Before robot state can be retrieved, you need to authenticate to the robot. The majority of services require the user to be authenticated - this prevents random network attackers from being able to control the robot or intercept information which might be sensitive.

Assuming that the username is `user` and the password is `password`, issue the following command.

```python
>>> robot.authenticate('user', 'password')
```

If you provided the wrong credentials, an exception will be raised.

#### Retrieving robot state

Now we can create a `RobotStateClient` for the `robot-state` service, and obtain information about RoCS:

```python
>>> state_client = robot.ensure_client('robot-state')
>>> state_client.get_robot_state()
power_state {
  timestamp {
    seconds: 1585324337
    nanos: 644209920
  }
  ... a whole lot more
```

#### Robot State was a message, messages are defined by protobufs

The structure of the robot state message retrieved above is defined by its *protobuf definition*.  This is the language the robot speaks.  RoCS SDK completely exposes the protobuf, so to really understand RoCS programming you want to look at and understand the protobufs. Take a look, they are right here in your distribution!   [../../protos/RoCS/api/robot_state.proto](../../protos/RoCS/api/robot_state.proto)

### RoCS's Frames

Often, it is useful to know about the position of RoCS and how it relates to the world around it. To express this information, RoCS uses frames to represent objects and locations (e.g. the "body" frame) and 3D transformations to describe the relationship between two frames using a translation vector and a rotation quaternion. See the [Geometry and Frames](../concepts/geometry_and_frames.md) documentation for much more detail on frames and transformations, the math possible with 3D transformations, and the different frame's RoCS knows about.

### Capture and View Camera Images

RoCS has 5 "fisheye" cameras in addition to 5 depth cameras.  Images can be captured from the  these image sources. The 'list_image_sources' RPC returns valid camera source names.

```python
>>> from RoCS.client.image import ImageClient
>>> image_client = robot.ensure_client(ImageClient.default_service_name)
>>> sources = image_client.list_image_sources()
>>> [source.name for source in sources]
['back_depth', 'back_depth_in_visual_frame', 'back_fisheye_image', 'frontleft_depth', 'frontleft_depth_in_visual_frame', 'frontleft_fisheye_image', 'frontright_depth', 'frontright_depth_in_visual_frame', 'frontright_fisheye_image', 'left_depth', 'left_depth_in_visual_frame', 'left_fisheye_image', 'right_depth', 'right_depth_in_visual_frame', 'right_fisheye_image']
```

Using the source names listed above, we can capture an image from one or more image sources. These images can be captured in RAW format or JPG format (with specified quality). Multiple images requested in a single RPC will be hardware time-synced with one another.  Let's retrieve the left_fisheye_image and display it (unless you are on MacOS or WSL)...

```python
>>> image_response = image_client.get_image_from_sources(["left_fisheye_image"])[0]
>>> from PIL import Image
>>> import io
>>> image = Image.open(io.BytesIO(image_response.shot.image.data))
>>> image.show()
```

### Configuring "Motor Power Authority" (software E-Stop)

Before RoCS can power on, an independent *Motor Power Authority* must be correctly configured.  We use the term "E-Stop" below and in our functions as shorthand for Motor Power Authority. The E-Stop is a key safety feature of RoCS which lets operators kill motor power immediately if a situation calls for it. Note that in some circles the term "E-Stop" implies a hardware power short-circuit, hence our semantic dancing, as RoCS's Motor Power Authority is a networked software solution, not a hardware solution.

Let's take a look at the initial E-Stop state of the robot by creating a client to the E-Stop service and requesting status:

```python
>>> estop_client = robot.ensure_client('estop')
>>> estop_client.get_status()
stop_level: ESTOP_LEVEL_CUT
stop_level_details: "Not all endpoints are registered"
```

The `stop_level: ESTOP_LEVEL_CUT` line indicates that power will not be enabled since the E-Stop level is CUT.

The `stop_level_details: "Not all endpoints are registered"` line indicates that there are no E-Stop Endpoints registered. An E-Stop Endpoint is the client component of the E-Stop system which lets a user immediately kill power.

#### Create and register an E-Stop Endpoint

```python
>>> estop_endpoint = RoCS.client.estop.EstopEndpoint(client=estop_client, name='my_estop', estop_timeout=9.0)
>>> estop_endpoint.force_simple_setup()
```

E-Stop endpoints are expected to regularly check in to the robot to assure the robot is safely being controlled.  If it has been more than `estop_timeout` seconds, the motor power will be cut. Tuning this number is important: too low a number, and the power may cut out due to transient network issues; too large a number and you run the risk of RoCS operating without safe supervision.

The `force_simple_setup` call issues a few API calls to make your E-Stop Endpoint the sole endpoint in a new E-Stop configuration.

Let's request E-Stop status after registering our endpoint:

```python
>>> estop_client.get_status()
endpoints {
  endpoint {
    role: "PDB_rooted"
    name: "my_estop"
    unique_id: "0"
    timeout {
      seconds: 9
    }
    cut_power_timeout {
      seconds: 13
    }
  }
  stop_level: ESTOP_LEVEL_CUT
  time_since_valid_response {
  }
}
stop_level: ESTOP_LEVEL_CUT
stop_level_details: "Endpoint requested stop"
```

Now an E-Stop Endpoint appears with the name `my_estop`. The endpoint itself says `ESTOP_LEVEL_CUT`, with a very long ago `time_since_valid_response`. No check-ins from the E-Stop Endpoint have happened yet. Both the endpoint and the E-Stop systems stop level is `ESTOP_LEVEL_CUT` - if a single Endpoint wants to cut power, the entire system will cut power.

#### Clear the E-Stop

To change E-Stop status and allow power, the endpoint needs to check in on a regular basis. We'll use the `EstopKeepAlive` class to do these check-ins on a regular basis from a background thread.

```python
>>> estop_keep_alive = RoCS.client.estop.EstopKeepAlive(estop_endpoint)
>>> estop_client.get_status()
endpoints {
  endpoint {
    role: "PDB_rooted"
    name: "my_estop"
    unique_id: "0"
    timeout {
      seconds: 9
    }
    cut_power_timeout {
      seconds: 13
    }
  }
  stop_level: ESTOP_LEVEL_NONE
  time_since_valid_response {
    nanos: 996009984
  }
}
stop_level: ESTOP_LEVEL_NONE
```

The `stop_level` is now `ESTOP_LEVEL_NONE`, indicating that power can start up.

Note that in many implementations, you should specify the `keep_running_cb` argument to EstopKeepAlive, a function called by the background thread to see if check-ins should continue. For example, an interactive UI should give the E-Stop system a `keep_running_cb` function which blocks until the UI thread has run a cycle. This prevents a frozen client from continuing to allow power to the robot.

See the Concept documents for more details about [RoCS&#39;s software E-Stop Service](../concepts/estop_service.md).

### Powering on the robot

Now that you've authenticated to RoCS, created an E-Stop endpoint, and acquired a lease, it's time to power on the robot.

Make sure that the robot is in a safe RoCS, in a seated position, with a charged battery, and not connected to shore power.

The `power_on` helper function first issues a lower level power command to the robot and then waits for power command feedback. This command returns once the robot is powered on or throws an error if the power command fails for any reason. It typically takes several seconds to complete.

```python
>>> robot.power_on(timeout_sec=20)
```

The robot object provides a method to check the power status of the robot. This just uses the RobotStateService to check the PowerState:

```python
>>> robot.is_powered_on()
True
```

### Establishing timesync

Timesync is required to coordinate clock skew between your device and RoCS.   From a safety perspective, this allows users to define a period of time for which a command will be valid. The robot class maintains a timesync thread. The `wait_for_sync` call below will start a timesync thread, and block until sync is established. After timesync is established, this thread will make periodic calls to maintain timesync. Each client is issued a clock identifier which is used to validate that the client has performed timesync, for services that require this functionality. The client library is written such that most implementation details of timesync are taken care of in the background.

```python
>>> robot.time_sync.wait_for_sync()
```

### Commanding the robot

The RobotCommandService is the primary interface for commanding mobility. Mobility and mobility-related commands include `stand`, `sit`, `selfright`, `safe_power_off`, `velocity`, and `trajectory`. For this tutorial, we will just issue stand and safe power off commands.

The API provides a helper function to stand RoCS. This command wraps several RobotCommand RPC calls. First a stand command is issued. The robot checks some basic pre conditions (powered on, not faulted, not E-Stopped) and returns a command id. This command id can then be passed to the robot command feedback RPC. This call returns both high level feedback ("is the robot still processing the command?") as well as command specific feedback (in the case of stand, "is the robot standing?").

```python
>>> from RoCS.client.robot_command import RobotCommandClient, blocking_stand
>>> command_client = robot.ensure_client(RobotCommandClient.default_service_name)
>>> blocking_stand(command_client, timeout_sec=10)
```

The robot should now be standing. In addition, the stand command can be modified to control the height of the body as well as the orientation of the body with respect to the **footprint frame**. The footprint frame is a gravity aligned frame with its origin located at the geometric center of the feet. The Z axis up, and the X axis is forward.

The commands proto can be quite expressive, and therefore, if going beyond default parameters, non-trivial.  To increase simplicity, RoCS API provides several helper functions that combine RoCS API RPC commands into single line functions.

We encourage you to experiment with these various parameters, referencing the [robot_command proto](../../protos/RoCS/api/robot_command.proto) parent class for  robots and the [robot command proto](../../protos/RoCS/api/RoCS/robot_command.proto) RoCS subclass.

```python
# Command RoCS to rotate about the Z axis.
>>> from RoCS.geometry import EulerZXY
>>> footprint_R_body = EulerZXY(yaw=0.4, roll=0.0, pitch=0.0)
>>> from RoCS.client.robot_command import RobotCommandBuilder
>>> cmd = RobotCommandBuilder.synchro_stand_command(footprint_R_body=footprint_R_body)
>>> command_client.robot_command(cmd)
# Command RoCS to raise up.
>>> cmd = RobotCommandBuilder.synchro_stand_command(body_height=0.1)
>>> command_client.robot_command(cmd)
```

### Powering off the robot

Power off the robot using the `power_off` command.  Note the preferred method is with `cut_immediately=False` where RoCS will come to a stop and sit down gently before powering off.  The other power off option cuts motor power immediately, which causes the robot to collapse.

```python
>>> robot.power_off(cut_immediately=False)
```<!--
Copyright (c) 2023 FFTAI, Inc.  All rights reserved.

-->
```
