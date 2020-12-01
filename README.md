# Keep-it-Flat-KiF-Resource-Management-in-Integrated-Cloud-Fog-Networks

#Simulator Classes 

To implement and analyze our proposed variations, we used the Yet Another
Fog Simulator (YAFS). YAFS is a discrete event simulator designed to ana-
lyze the fog applications and the strategies used for their placement, scheduling.
Moreover, this simulator provides tools to analyze the routing strategies as well.
This simulator is built based on the Simpy library, which is a Python library
containing functions that define processes and shared resources.
YAFS is defined by its six main classes which are the core, topology, selection,
placement, population and the application class. The core is the class responsible 
for managing simulation execution to control the life cycle of the processes
running.
The topology class, as its name says, it is used to create the fog nodes, cloud
servers, sensors and actuators. When defining those network modules, the node's
RAM, cost and instruction per simulation time must be provided. Moreover,
each node will be represented by its id. This class is also used to define the links
between the network devices, which will be defined by the source, destination,
bandwidth and propagation delay. This class is accessed by other classes through
the core class, since the topology class is a main element of it.

The application class defines modules that run services and messages. Thus
using this class we can define the messages' behaviour of any type of application.
The message is defined by the size of its data, and the number of instructions.
The selection, placement and population classes are the classes used and modified
by user to define the scheduling, routing, resource allocation, and application's
deployment in the created topology.
In addition to those six classes, one important class is used which is the dis-
tribution class. This class is essential to allow customized distribution among
messages. Some of the distribution methods defined in this class are determin-
istic distribution, uniform distribution, and most importantly the exponential
distribution.
After defining the topology, the application with its messages and deployment,
and the messages distribution the simulation can start. The simulator issues two
excel files as output. The first excel file shows the name of the application, the

ow of messages and the processing time in details; through showing the time
emitted, reception time, time it went into the module for execution, and the time
the execution was over. The second excel file is concerned with the routing, it
shows how the messages moves from the source to destination and which modules
are used as routers for the propagation.
We had to modify the simulator in order to adapt it to the environment needed
to deploy our approach and architecture. Indeed, our fog nodes are characterized
by the CPU, Memory (RAM), instructions per second and privacy measure. For
that, the topology class was changed by adding the new attributes which weren't
present for creating a fog node.

As for IoT tasks, which will be represented by the messages from the application
class, we had to add the other needed variables as security level, scheduling class,
CPU, memory, and maximum allowed delay in addition to to the Bytes and in-
struction count variables which were already declared in the class.
There are fout types of messages in our proposed approach. Each type of these
four messages must be treated diferently, for that, the major changes were done
in the core class especially in the "send message" function present in this class.

The selection class is implemented in a way that helps us customize our task
allocation algorithm and thus implement the two variation of our approach in
chapter 3. For that, diferent methods were added to allow the deployment of
diferent messages. For example, the first type of message must be sent to the
controller of the fog node the IoT device connected to, while the third message
must be sent to the fog node (if found) chosen by the controller.


#Topology:
To evaluate the performance of our approach, four types of topology were cre-
ated, each containing 5, 10, 15, and 20 clusters respectively. 
Each cluster in every type of topology has a small number of fog nodes, since
small scale fogs would result in better performance metrics.
This number of fog nodes ranges between 4 and 8 in our work.
Each fog (cluster) has a range between 3 to 5 IoT devices directly connected
to it. Each of these devices could reach between 0 to 4 other fogs. Although
the number of IoT devices is not large, yet with respect to the topology being
created and the number of fogs in each cluster, this number of devices can issue
enough tasks in order to be able to evaluate the overall performance. This is
due to the fact that the eficiency of the simulation depends on the number of
messages being generated and not only on the number of devices issuing the tasks.
To set the characteristics of the fog nodes, we used values from real servers like
IBM 7030, and Intel 4004. This was helpful to set a reasonable and synchronized values for the
instructions per second, CPU speed and RAM attributes for every fog node.
As for the privacy measure attribute, it was added using a uniform distribu-
tion. Meaning, we assumed that each cluster has a range of privacy measures
and the privacy measure for every fog node belonging to the cluster is within
this range. For example, assume having fog cluster k with privacy measure range
between 0.3 and 0.5; where each value of this range is a trust value generated
based on a tool that assess the security strength of fog nodes
so the fog nodes of this cluster will have a privacy measure value in that range.
We assumed having one cloud server acting as the CLOUD. The instruction
per second parameter of the cloud must be higher than any value being set to
the fog nodes. This is due to the fact that the cloud has higher processing capa-
bilities than any fog node, and for that it's responsible for handling heavy tasks
As for the connections, the bandwidth between an IoT device and a fog node
could be either 54 Mbits/s as in wireless 802.11g networks or 100 Mbits/s as in
fast Ethernet. The bandwidth between the controllers; which act as routers for
IoT devices; and the cloud is set to 10 Gbits/s. While the bandwidth between
fog controllers is set to 100 Mbits/s. 

#Task Batches

Before starting with the simulation we needed to create a large set of tasks. The
tasks' requirements as CPU, memory and instruction count were generated using
the values set to the fog nodes. For example, the minimum value of cycles per
second (CPU) for a fog node in our topology is 740000 as in Intel 4004, while
the maximum value is 8696000 as in IBM System/370 Model 158, so the CPU
required by tasks will be a value within this range. As for the security level, it
was generated uniformly between 0.2 and 0.9. Assuming that lowest trust value
being calculated, for a fog node will be 0.2 while the highest value is 0.9.
The scheduling class of every task was also uniformly generated to be either
0 or 1, yet we gave the preference for 0 over 1. We assumed that IoT tasks should
not always be delay tolerant; rather the tasks should require resources as fast as
possible.
