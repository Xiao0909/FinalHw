# FinalHw
This project is an implementation of a small simulation program. It is a simulation of a process
scheduler of a computer system. This simulated scheduler is a very small, simplified version,
which reflects some of the basic operations of a typical process scheduler.
To successfully finish the program, students are expected to:
• Study and learn how to use PriorityQueues
• Study and learn how to write a small simulation program.
Name the file with the main method ProcessScheduling.java. You may define other classes as
needed in separate files.
The following describes the scheduling system that is simulated:
Processes arrive at a computer system and the computer system choose which process to
execute at each time point based on the process’s priority. Each process has a process id,
priority, arrival time, and duration. The duration of a process is the amount of time it takes
to completely execute the process. The system keeps a priority queue to keep arriving
processes and prioritize the execution of processes. When a process arrives, it is inserted into
the priority queue. Then, at each timestep the system removes a process with the smallest
priority from the priority queue and executes it for a single timestep.
Suppose that a process p with a very large priority arrives at the system while the system is
executing another process. While p is waiting in the queue, another process q with a
relatively small priority arrives. After the execution of the current process is finished, the
system will remove and execute q (because q has a smaller priority), and p must wait until q
finishes. If another process with a smaller priority arrives while q is being executed, p will
have to wait again after q is completed. If this is repeated, p will have to wait for a very long
time. One way of preventing this is as follows: If a process has waited longer than a
predetermined maximum wait time, we update the priority of the process by decreasing the
priority by one. For example, if the current priority of the process is 5, then it is updated to 4.
For the purpose of this simulation, we assume the following:
• We use a modified version of the HeapAdaptablePriorityQueue given by the textbook
o Please use the version of net.datastructures given in the project code package and
not the net.datastructures package that you used in other assignments.
• Each entry in the priority queue keeps a process object, which represents a process.
• Each process must have, at the minimum, the following attributes:
id: integer // process id 
arrivalTime: integer // the time when the process arrives at the system
duration: integer // execution of the process takes this amount of time
The simulation program uses a logical time to keep track of the simulation process and the same
logical time is used to represent the arrivalTime and duration. The simulation goes through a
series of iterations and each iteration represents the passage of one logical time unit (in what
follows we will use time to refer to logical time unit). At the beginning, the current time is set to
time 0. Each iteration implements what occurs during one time unit and, at the end of each
iteration, the current time is incremented.
The following describes the general behavior of the simulation program:
• All processes are stored in a certain data structure D, which is supposed to be external
to the computer system.
• In each iteration (one time unit), the following occurs (not necessarily in the given
order):
• We compare the current time with the arrival time of a process with the earliest
arrival time in D. If the arrival time of that process is equal to or smaller than the
current time, we remove the process from D and insert it into the adaptable priority
queue Q (this represents the arrival of a process at the system).
• If there is at least one process in Q, then the process with the smallest priority in Q is
executed. If multiple processes have the same priority, then Java will arbitrarily
decide which process to execute.
• The wait time of a process p is the amount of time p has waited in Q. It is calculated
by subtracting the arrival time of p from the time when p is removed from Q. For
example, if the arrival time of p is 12 and p is removed from Q at time 20, then the
wait time is 20 – 12 = 8.
• Update the priorities of some processes. The update is performed as follows. If there
is any process in Q that has been waiting longer than the predetermined maximum
wait time, then the priority of that process is decreased by one. You may need an
additional data structure to help make updates (since changing the priority of a
Process will affect the order of Processes in the PriorityQueue).
• The current time is increased by one time unit.<br>
• The above is repeated until D and Q are empty. At this time, all processes have<br>
arrived at the system. Some of them may have been completed and removed from Q
and some may still wait in Q.
<br>A pseudocode of the simulation is given below. Note that this pseudocode is a high-level
description, and you must determine implementation details and convert the pseudocode to a
Java program. In the pseudocode, Q is a priority queue. 
Read all processes from an input file and store them in an appropriate data structure, D
Initialize currentTime
create an empty priority queue Q
<br>// Each iteration of the while loop represents what occurs during one time unit
<br>// Must increment currentTime in each iteration
<br>While Q and D are not empty // while loop runs once for every time unit until Q is empty
<br>If D is not empty
<br> Get (don’t remove) a process p from D that has the earliest arrival time
<br> If the arrival time of p <= currentTime
<br> Remove p from D and insert it into Q
If Q is not empty
Execute the top process in Q for one time step
 Update the wait times of all processes in Q
Update priorities of processes that have been waiting longer than max. wait time
End of While loop<br>
<br>
<br>Calculate average wait time
<br>An input file stores information about all processes. The name of the input file is
process_scheduling_input.txt. A sample input file is shown below (this sample input is posted on
Blackboard):
1 4 25 10<br>
2 3 15 17<br>
3 1 17 26<br>
4 4 9 17 30<br>
5 10 9 40<br>
6 6 14 47<br>
7 7 7 18 52<br>
8 5 18 70<br>
9 2 16 93<br>
10 8 20 125<br>


Each line in the input file represents a process and it has four integers separated by a space(s).
The four integers are the process id, priority, duration, and arrival time, respectively, of a
process. Your program must read all processes from the input file and store them in an
appropriate data structure. You can use any data structure that you think is appropriate.
While your program is performing the simulation, whenever a different process is being
executed, your program must display information about the process that stopped execution and
the process that started execution. Your program also needs to print other information as shown
in the sample output below. After your program finishes the simulation of the execution of all 
processes, it must display the average waiting time of all processes. A sample output is shown
below, which is the expected output for the above sample input.
Note that:
<br>• This output was generated using 30 as the maximum wait time. A different maximum
wait time will result in a different output.
<br>• Your output may not be the same as the one shown below. This is because when two
processes have the same smallest priority and wait time, the choice is made by Java
arbitrarily when a process is removed from the queue.



<br>Expected output:
<br>// print all processes first
<br>Id = 1, priority = 4, duration = 25, arrival time = 10<br>
Id = 2, priority = 3, duration = 15, arrival time = 17<br>
Id = 3, priority = 1, duration = 17, arrival time = 26<br>
Id = 4, priority = 9, duration = 17, arrival time = 30<br>
Id = 5, priority = 10, duration = 9, arrival time = 40<br>
Id = 6, priority = 6, duration = 14, arrival time = 47<br>
Id = 7, priority = 7, duration = 18, arrival time = 52<br>
Id = 8, priority = 5, duration = 18, arrival time = 70<br>
Id = 9, priority = 2, duration = 16, arrival time = 93<br>
Id = 10, priority = 8, duration = 20, arrival time = 125<br>
Maximum wait time = 30<br>
Now running Process id = 1<br>
Arrival = 10<br>
Duration = 25<br>
Run time left = 25<br>
at time 10<br>
Executed process ID:1, at time 10 Remaining: 24<br>
Executed process ID:1, at time 11 Remaining: 23<br><br>
Executed process ID:1, at time 12 Remaining: 22<br>
Executed process ID:1, at time 13 Remaining: 21<br>
Executed process ID:1, at time 14 Remaining: 20<br>
Executed process ID:1, at time 15 Remaining: 19<br>
Executed process ID:1, at time 16 Remaining: 18<br>
Now running Process id = 2<br>
Arrival = 17<br>
Duration = 15<br>
Run time left = 15<br>
at time 17
Executed process ID:2, at time 17 Remaining: 14<br>
Executed process ID:2, at time 18 Remaining: 13<br>
Executed process ID:2, at time 19 Remaining: 12<br>
Executed process ID:2, at time 20 Remaining: 11<br>
Executed process ID:2, at time 21 Remaining: 10<br>
Executed process ID:2, at time 22 Remaining: 9<br>
Executed process ID:2, at time 23 Remaining: 8<br>
Executed process ID:2, at time 24 Remaining: 7<br>
Executed process ID:2, at time 25 Remaining: 6<br>
Now running Process id = 3<br>
Arrival = 26<br>
Duration = 17<br>
Run time left = 17<br>
at time 26<br>
Executed process ID:3, at time 26 Remaining: 16<br>
Executed process ID:3, at time 27 Remaining: 15<br>
Executed process ID:3, at time 28 Remaining: 14<br>
Executed process ID:3, at time 29 Remaining: 13<br>
Executed process ID:3, at time 30 Remaining: 12<br>
Executed process ID:3, at time 31 Remaining: 11<br>
Executed process ID:3, at time 32 Remaining: 10<br>
Executed process ID:3, at time 33 Remaining: 9<br>
Executed process ID:3, at time 34 Remaining: 8<br>
Executed process ID:3, at time 35 Remaining: 7<br>
Executed process ID:3, at time 36 Remaining: 6<br>
Executed process ID:3, at time 37 Remaining: 5<br>
Executed process ID:3, at time 38 Remaining: 4<br>
Executed process ID:3, at time 39 Remaining: 3<br>
Executed process ID:3, at time 40 Remaining: 2<br>
Executed process ID:3, at time 41 Remaining: 1<br>
Executed process ID:3, at time 42 Remaining: 0<br>
Finished running Process id = 3<br>
Arrival = 26<br>
Duration = 17<br>
Run time left = 0<br>
at time 42<br>
...(repeat for each id)<br>
Finished running all processes at time 178
Average wait time: 41.3
