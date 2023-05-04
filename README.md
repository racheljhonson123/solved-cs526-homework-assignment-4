Download Link: https://assignmentchef.com/product/solved-cs526-homework-assignment-4
<br>
The goal of this assignment is to give students an opportunity to implement an application that uses a priority queue. The application to be implemented is a simulation of a process scheduler of a computer system. This simulated scheduler is a small, simplified version, which reflects some of the basic operations of a typical scheduler.




Name the file with the main method as <em>ProcessScheduling.java</em>.




The following describes the scheduling system that is simulated.




Processes arrive at a computer system and the computer system executes the processes one at a time based on a priority criterion. Each process has a <em>process id</em>, <em>priority</em>, <em>arrival time</em>, and <em>duration</em>. The <em>duration</em> of a process is the amount of time it takes to completely execute the process. The system keeps a priority queue to keep arriving processes and prioritize the execution of processes. When a process arrives, it is inserted into the priority queue. Then, each time the system is ready to execute a process, the system removes a process with the <strong><em>smallest priority</em></strong> from the priority queue and executes it for the <em>duration </em>of the process.




For the purpose of this simulation, we assume the followings:




<ul>

 <li>We use the priority queue implemented in the <em>java</em>. This class implements a priority queue that uses a heap data structure.</li>

 <li>Each entry in the priority queue keeps (<em>K</em>, <em>V</em>) pair, which represents a process.

  <ul>

   <li><em>K</em> is the <em>priority</em> of the process and it is of Integer type. The value of <em>priority</em> is between 1 and 10, inclusively. A process with a smaller <em>priority</em> is executed before a process with a larger <em>priority</em>.</li>

   <li><em>V</em> is the reference to the process.</li>

  </ul></li>

 <li>Each process must have, at the minimum, the following attributes:</li>

</ul>




<em>pr</em>: Integer                   // priority of the process

<em>id</em>: integer                    // process id

<em>arrivalTime</em>: integer    // the time when the process arrives at the system <em>duration</em>: integer        // execution of the process takes this amount of time




The simulation program uses a logical time to keep track of the simulation process and the same logical time is used to represent the <em>arrivalTime</em> and <em>duration</em>. The simulation goes through a series of iterations and each iteration represents the passage of one logical time unit (in what follows we will use <em>time unit</em> to refer to <em>logical time unit</em>). At the beginning, the current time is set to time 0. Each iteration implements what occurs during one time unit and, at the end of each iteration, the current time is incremented.




The following describes the simulation program:

<ul>

 <li>All processes are stored in a certain data structure<em> D</em>, which is supposed to be external to the computer system.</li>

 <li>In each iteration, the following occurs:</li>

 <li>We compare the current time with the arrival time of a process with the earliest arrival time in <em>D</em>. If the arrival time of that process is equal to or smaller than the current time, we remove the process from <em>D</em> and insert it into the priority queue <em>Q</em> (this represents the arrival of a process at the system).</li>

 <li>If no process is being executed at this time and there is at least one process in <em>Q</em>, then a process with the <em>smallest priority</em> is removed from <em>Q</em> and executed.</li>

 <li><strong>Note:</strong> When there is more than one process with the same <em>smallest</em> <em>priority</em>, it would be reasonable that the one with the earliest <em>arrivalTime</em> is removed from <em>Q</em> and executed. However, for this assignment, you don’t need to implement this and you just need to remove an entry with the smallest <em>priority </em>as determined by the code within <em>java</em>.</li>

 <li>The current time is increased by one time unit.</li>

 <li>The above is repeated until <em>D</em> is empty. At this time, all processes have arrived at the system. Some of them may have been completed and removed from <em>Q</em> and some may still wait in <em>Q</em>.</li>

 <li>If there are any remaining processes in <em>Q</em>, these processes are removed and executed one at a time. Again, a process with the smallest priority is removed and executed first.</li>

</ul>




A pseudocode of the simulation is given below. You must consider this pseudocode as a highlevel description and you need to figure out details and convert the pseudocode to a Java program. In the pseudocode, <em>Q</em> is a priority queue, which stores &lt;<em>priority</em>, <em>process</em>&gt; pairs. There is a Boolean variable <em>running </em>in the pseudocode. It is used to indicate whether the system is currently executing a process or not. It is <strong><em>true</em></strong> if the system is currently executing a process and <strong><em>false</em></strong> otherwise.







Read all processes from the input file and store them in an appropriate data structure, <em>D</em> currentTime = 0  running = false

create an empty priority queue <em>Q </em>




While <em>D</em> is not empty // while loop runs once for every time unit until <em>D</em> is empty

Get (don’t remove) a process <em>p</em> from <em>D</em> that has the earliest arrival time

If the arrival time of <em>p</em> &lt;= currentTime Remove <em>p</em> from <em>D</em> and insert it into <em>Q</em>

If <em>Q</em> is not empty and the flag <em>running</em> is false

Remove a process with the smallest priority from <em>Q</em>

Set a flag<em> running</em> to true currentTime = currentTime + 1 If currently running process has finished

Set a flag<em> running</em> to false

End of While loop




// At this time all processes in <em>D</em> have been moved to <em>Q</em>.

While there is a process waiting in <em>Q</em>

Remove a process with the smallest priority from <em>Q</em> and execute it

<em> </em>

As mentioned in the first line of the pseudocode, an input file stores information about all processes. The name of the input file is <em>process_scheduling_in.txt</em>. A sample input file is shown below (this sample input is posted on Blackboard):




<ul>

 <li>10 25 10</li>

 <li>3 15 17</li>

 <li>1 17 26</li>

 <li>9 17 30</li>

 <li>10 9 40</li>

 <li>6 14 47</li>

 <li>7 18 52</li>

 <li>5 18 70</li>

 <li>2 16 93</li>

 <li>8 20 125</li>

</ul>




Each line in the input file represents a process and it has four integers separated by a space(s). The four integers are the <em>process id</em>, <em>priority</em>, <em>duration</em>, and <em>arrival time</em>, respectively, of a process. Your program must read all processes from the input file and store them in an appropriate data structure. You can use any data structure that you think is appropriate.




However, for the priority queue, you must use the priority queue implemented in <em>HeapPriorityQueue.java</em>. The <em>HeapPriorityQueue </em>class inherits from or implements a few superclasses and interfaces. You may want to study some or all of these superclasses and interfaces to better understand the <em>HeapPriorityQueue </em>class. On Blackboard, I will post only the <em>HeapPriorityQueue.java</em> file. You can obtain other files from the textbook’s source code collection.




While your program is performing the simulation, whenever a process is removed from the priority queue (to be executed), your program must display information about the removed process. Your program also needs to print other information as shown in the sample output below. After your program finishes the simulation of the execution of all processes in the input file, it must display the average waiting time of all processes. A sample output is shown below, which is the expected output for the above sample input. <em> </em>




Id = 1, priority = 10, duration = 25, arrival time = 10

Id = 2, priority = 3, duration = 15, arrival time = 17

Id = 3, priority = 1, duration = 17, arrival time = 26

Id = 4, priority = 9, duration = 17, arrival time = 30 Id = 5, priority = 10, duration = 9, arrival time = 40 Id = 6, priority = 6, duration = 14, arrival time = 47

Id = 7, priority = 7, duration = 18, arrival time = 52

Id = 8, priority = 5, duration = 18, arrival time = 70

Id = 9, priority = 2, duration = 16, arrival time = 93

Id = 10, priority = 8, duration = 20, arrival time = 125




Process removed from queue is: id = 1, at time 10, wait time = 0 Total wait time = 0.0

Process id = 1

Priority = 10

Arrival = 10

Duration  = 25

Process 1 finished at time 35




Process removed from queue is: id = 3, at time 35, wait time = 9 Total wait time = 9.0

Process id = 3

Priority = 1

Arrival = 26

Duration  = 17

Process 3 finished at time 52




Process removed from queue is: id = 2, at time 52, wait time = 35 Total wait time = 44.0 Process id = 2

Priority = 3

Arrival = 17

Duration  = 15

Process 2 finished at time 67




Process removed from queue is: id = 6, at time 67, wait time = 20 Total wait time = 64.0 Process id = 6

Priority = 6

Arrival = 47

Duration  = 14

Process 6 finished at time 81




Process removed from queue is: id = 8, at time 81, wait time = 11 Total wait time = 75.0 Process id = 8

Priority = 5

Arrival = 70

Duration  = 18

Process 8 finished at time 99




Process removed from queue is: id = 9, at time 99, wait time = 6 Total wait time = 81.0

Process id = 9

Priority = 2

Arrival = 93

Duration  = 16

Process 9 finished at time 115




Process removed from queue is: id = 7, at time 115, wait time = 63 Total wait time = 144.0 Process id = 7

Priority = 7

Arrival = 52

Duration  = 18




D becomes empty at time 125




Process 7 finished at time 133




Process removed from queue is: id = 10, at time 133, wait time = 8 Total wait time = 152.0 Process id = 10

Priority = 8

Arrival = 125

Duration  = 20

Process 10 finished at time 153




Process removed from queue is: id = 4, at time 153, wait time = 123 Total wait time = 275.0 Process id = 4

Priority = 9

Arrival = 30

Duration  = 17

Process 4 finished at time 170




Process removed from queue is: id = 5, at time 170, wait time = 130 Total wait time = 405.0 Process id = 5

Priority = 10

Arrival = 40

Duration  = 9

Process 5 finished at time 179




Total wait time = 405.0

Average wait time = 40.5




Your program must write the output to an output file named <em>process_scheduling_out.txt</em>.


