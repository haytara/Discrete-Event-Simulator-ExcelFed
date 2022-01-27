# Discrete-Event-Simulator-ExcelFed
This is a school project from Data Structures and Algorithms course. It is an application of discrete event simulation where and is an quite complex problem.  The aim of the project is to serve as much as player that come to the tennis court at discrete times for different services. The project graded as full point by the course instructors.
  
  **REFERENCE: Following Parts are project descriptions that are written by assistants of the course CmpE250 (Data Structures and Algorithms) in Bogazici University**
  
##  1 Introduction
Heraclitus once said “The only constant in life is change”. Heraclitus was a wise man, indeed,
but he missed an exception: if you take CMPE 250, you solve a Discrete Event Simulation
(DES) project!  
Well, but what is DES?  
Enter, Wikipedia: “A discrete-event simulation (DES) models the operation of a system as
a (discrete) sequence of events in time. Each event occurs at a particular instant in time and
marks a change of state in the system. Between consecutive events, no change in the system
is assumed to occur; thus the simulation time can directly jump to the occurrence time of
the next event”. In other words, DES is the representation of a certain process by simulating
certain events which occur at certain times. Hence, time is not continuous in DES and progress
according to the events. As a demonstrative example, a process of taking a coffee can be
simulated as follows:  
• TIME: 09:00 Go into the checkout queue.  
• TIME: 09:05 Order your coffee and make your payment.  
• TIME: 09:10 Go into the serving queue.  
• TIME: 09:15 Wait for the preparation of your coffee and enjoy your free time.  
• TIME: 09:20 Grab your coffee and enjoy!  
Note that in DES the only things that count are events and everything else is ignored. In
the case of the customer, until 09:20 only 5 things happened. Additionally, the time progressed
in a discrete fashion (i.e. jumped from one event to the next one). 1
In this project, you are expected to simulate training procedure of ExcelFed,
which is a tennis club founded by his excellency.

## 2 Details of the ExcelFed
Do you know his excellency? This is not even a question, everyone knows him. Yes, I am talking
about Roger Federer2 who is the best tennis player ever! He has decided to retire since he is
not young enough to continue his career. However, he wants to transfer his great experience to
the new generation. That’s why, he has founded ExcelFed.
Roger is very experienced so he knows almost everything that plays a huge role in the development
of the tennis player. He has already hired great nutritionists and chefs. Additionally,
he has a consulting team consists of Rafael Nadal and Novak Djokovic. Furthermore, he has
rent nice tennis courts. His aim is to train children in very good conditions so that there are
better tennis players.  
There is one “little” problem though. He needs great training coaches, masseurs, and
physiotherapists but he does not know how many he needs. He may hire many staffs but this
would be a waste of money and there are not many outstanding staffs. Therefore, he decided
to simulate the training procedure of ExcelFed with fictional players and staffs to
find how many of them would be enough. However, his relationship with simulation tools
and coding is terrible so he needs your help! Let Roger provide more detail.  
• There might be multiple training coaches, masseurs and physiotherapists depending on
the simulation configuration. In this case, every physiotherapist has his/her own service
time and training, and massage duration depending on the player’s need.  
• There are exactly three queues in the system: one for training, one for massage and one
for physiotherapy. So, each coach shares a common queue and similar for the others.  
• The training queue works in first-come-first-served fashion. Thus, the first player to
enter the queue is served before the others. If two players arrive at the same time, the
one with the lower ID is served first. When the training of the player is finished, he/she
enters the physiotherapy queue, immediately.  
• Since more training time requires more urgent rehabilitation, physiotherapy queue works
in a prioritized manner. Therefore, in this queue, the more the training time, the
higher the priority. If there are more than one player that have the same training
time, then the one that arrived earlier is served before. If they arrived at the same time
as well, then the one with the lower ID is served first. Note that, one player may come
to the training more than one time, for the prioritization, you should consider only the
current training time not the cumulative.  
• Because massage is an advanced service, players should deserve them by their skills.
Hence, in the massage queue, the higher the skill level, the earlier the service. If
there are more than one player that are in the same skill level, then the one that arrived
earlier is served before. If they arrived at the same time as well, then the one with the
lower ID is served first  
• For all of the services, players visit the first available staff for the service (the available
staff with the smallest ID) when they leave the queue.  
• Each player is allowed to take at most 3 massage service. Hence, whenever a player
attempts to enter the massage queue 4th time, this is called an “invalid attempt”.  
• Since it is hard for the players to estimate how much time they spend in the queues,
there could be some cases such that players may try to come to the training or massage
when they are already in the training, physiotherapy or massage process. These attempts
should be “canceled” so they are called “canceled attempts”.  
• One can enter the physiotherapy queue only after the training, no direct entrance is
possible.  
Below, is a schematic description of the training procedure of his excellency.  
![image](https://user-images.githubusercontent.com/81170575/151330391-1a78f03e-eddc-4465-a754-ea373e6a34a4.png)
**Figure 1: A schema of the queues**  

Therefore, for our purposes, there are two types of events triggered by the players: coming
to the training and massage request. Keep also in mind that internal events, such as leaving
the training, should also be triggered by the simulation. Roger Federer expects you to simulate
the training procedure of ExcelFed using these external and internal discrete events and collect
some statistics.
## 3 Input & Output
### 3.1 Input
Roger provides all simulation configuration files in the following format:  
• The first line contains an integer N that denotes the total number of players in ExcelFed.
• Each of the next N line contains two integer: the ID of the player and his/her skill level.
These players will be given in sorted order by ID.  
• The next line is the line of an integer A that denotes the total number of arrival to the
training and massage.  
• Each of the next A lines contains a character At denoting the type of arrival (either
“m”(massage) or “t”(training)), an integer denoting the ID of the player, the second T
that denotes the arrival time, and d duration of the process. These events will not be
given in sorted order.  
• The next line comprises an integer Sp that denotes the number of physiotherapists and
a list of floats of size Sp. The ith element of the list denotes the service time of the ith
physiotherapist.  
• The last line contains two integers: Sc that denotes the number of training coaches and
Sm that denotes the number of masseurs.  
Following demonstrates an example input provided by Rafael Nadal, the best consultant in
the consultancy team.  
**Sample Input File Explanations**
**3 There are 3 players.**  
0 2            _The player with ID 0 has a skill level 2._  
1 3            _The player with ID 1 has a skill level 3._  
2 1            _The player with ID 2 has a skill level 1. _ 
**9 There 9 arrivals in total.**  
t 0 1 1.2      _The player with ID 0 arrives for the training at second 1 and the training will take 1.2 seconds._    
t 1 1.2 2  
m 0 6 3        _The player with ID 0 arrives for the massage at second 6 and the massage will take 3 seconds._  
m 1 6.3 1.8  
m 0 10 1.2  
t 2 10.1 4  
m 0 15 1.2  
m 2 16 1.5  
m 0 20 3  
1 2            _There is 1 physiotherapist and her service time is 2 seconds._    
1 1            _There are 1 training coach and 1 masseur._  
### 3.2 Output
Roger needs you to collect the following statistics to evaluate the configuration and output
them in separate lines, in the order they are given. Please round the statistics to exactly 3
decimal points. In case you cannot report any of the following 15 statistics, print -2 for each
of them in order to adhere the output format.  
1. Maximum length of the training queue.  
2. Maximum length of the physiotherapy queue.  
3. Maximum length of the massage queue.  
4. Average waiting time in the training queue.  
5. Average waiting time in the physiotherapy queue.  
6. Average waiting time in the massage queue.  
7. Average training time.  
8. Average physiotherapy time.  
9. Average massage time.  
10. Average turnaround time (Turnaround time: Total time passed from the training queue
entrance until leaving the physiotherapy service.) To compute, sum all turnaround times
and divide it by the number of turnarounds, which is also equal to the number of total
training arrivals.  
11. ID of the player who spent the most time in the physiotherapy queue and the waiting
time of that player in seconds. If more than one player spent the same amount of time,
choose the one with the smallest ID.  
12. ID of the player who spent the least time in the massage queue and the waiting time of
that player in seconds, among the ones who took three massage services. If more than
one player spent the same amount of time, choose the one with the smallest ID. If there
is no player that took three massage services, print -1 for both.  
13. Total number of invalid attempts to get a message service.  
14. Total number of canceled attempts including both training and massage attempts.  
15. Total seconds passed during the whole simulation.  
Nadal also showed the courtesy to share the expected output for the input in Table 2 with
explanations. He also showed the progress of queues and services in Table 3 where the numbers
in the parenthesis in the“service” columns represent the number of remaining seconds to finish
the process. 
![Table](https://user-images.githubusercontent.com/81170575/151333505-ed8a5e6b-3b3a-466b-b711-b8672e5517c5.png)  
**Table:** Step by step progress of the queues and services. Numbers in the parentheses denote
the exact second to leave the service.  
