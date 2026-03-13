# Series Queues with infinite capacity - Open Jackson Network

## Aim :
To find (a) average number of materials in the system (b) average number of materials in the each conveyor of (c) waiting time of each material in the system (d) waiting time of each material in each conveyor, if the arrival  of materials follow Poisson process with the mean interval time 12 seconds, service time of  lathe machine in series follow exponential distribution  with service time  1 second, 1.5 seconds and 1.3 seconds respectively and average service time of robot is 7 seconds.

## Software required :
Visual components and Python

## Theory

![image](https://user-images.githubusercontent.com/103921593/203239736-7b81f599-71a8-4ae7-b63e-5d98acd9ea54.png)


## Procedure :

![image](https://user-images.githubusercontent.com/103921593/203239789-bc870dce-6727-487b-a0e2-4fc3f5114889.png)


## Experiment:


## Program

````
import math

# Getting Inputs
ArrivalTime = float(input("Enter the mean inter-arrival time of objects from Feeder (in secs): "))
ServiceTime1 = float(input("Enter the mean service time of Lathe Machine 1 (in secs): "))
ServiceTime2 = float(input("Enter the mean service time of Lathe Machine 2 (in secs): "))
ServiceTime3 = float(input("Enter the mean service time of Lathe Machine 3 (in secs): "))
RobotTime = float(input("Enter the mean service time of the Robot (in secs): "))

# Calculating Lambda and Mu for each server
Lambda = 1 / ArrivalTime
Mu1 = 1 / ServiceTime1
Mu2 = 1 / ServiceTime2
Mu3 = 1 / ServiceTime3
Mu_robot = 1 / RobotTime

print("\nSeries Queues with Infinite Capacity - Open Jackson Network")
print("Mean arrival rate per second               : %0.4f" % Lambda)
print("Mean service rate per second of Lathe 1    : %0.4f" % Mu1)
print("Mean service rate per second of Lathe 2    : %0.4f" % Mu2)
print("Mean service rate per second of Lathe 3    : %0.4f" % Mu3)
print("Mean service rate per second of Robot      : %0.4f" % Mu_robot)

# Check for stability condition
if (Lambda < Mu1) and (Lambda < Mu2) and (Lambda < Mu3) and (Lambda < Mu_robot):
    
    # Function to calculate M/M/1 metrics
    def mm1_metrics(lam, mu):
        rho = lam / mu
        Ls = rho / (1 - rho)        # Average number in system
        Lq = rho**2 / (1 - rho)     # Average number in queue (conveyor)
        W = 1 / (mu - lam)          # Average waiting time in system
        Wq = Lq / lam               # Average waiting time in queue
        return Ls, Lq, W, Wq
    
    # Metrics for each server
    Ls1, Lq1, W1, Wq1 = mm1_metrics(Lambda, Mu1)
    Ls2, Lq2, W2, Wq2 = mm1_metrics(Lambda, Mu2)
    Ls3, Lq3, W3, Wq3 = mm1_metrics(Lambda, Mu3)
    Ls_robot, Lq_robot, W_robot, Wq_robot = mm1_metrics(Lambda, Mu_robot)
    
    # Total system metrics
    Total_Ls = Ls1 + Ls2 + Ls3 + Ls_robot
    Total_W = W1 + W2 + W3 + W_robot
    
    # Output
    print("\nAverage number of objects in each system (Ls):")
    print("Lathe 1: %0.3f" % Ls1)
    print("Lathe 2: %0.3f" % Ls2)
    print("Lathe 3: %0.3f" % Ls3)
    print("Robot  : %0.3f" % Ls_robot)
    print("Total system: %0.3f" % Total_Ls)
    
    print("\nAverage number of objects in each conveyor/queue (Lq):")
    print("Lathe 1: %0.3f" % Lq1)
    print("Lathe 2: %0.3f" % Lq2)
    print("Lathe 3: %0.3f" % Lq3)
    print("Robot  : %0.3f" % Lq_robot)
    
    print("\nAverage waiting time of an object in system (W) in secs:")
    print("Lathe 1: %0.3f" % W1)
    print("Lathe 2: %0.3f" % W2)
    print("Lathe 3: %0.3f" % W3)
    print("Robot  : %0.3f" % W_robot)
    print("Total system: %0.3f" % Total_W)
    
    print("\nAverage waiting time of an object in queue/conveyor (Wq) in secs:")
    print("Lathe 1: %0.3f" % Wq1)
    print("Lathe 2: %0.3f" % Wq2)
    print("Lathe 3: %0.3f" % Wq3)
    print("Robot  : %0.3f" % Wq_robot)
    
else:
    print("Warning! Objects overflow will happen in the conveyor (system unstable)")
````


## Output

````
Enter the mean inter-arrival time of objects from Feeder (in secs):  12
Enter the mean service time of Lathe Machine 1 (in secs):  1
Enter the mean service time of Lathe Machine 2 (in secs):  1.5
Enter the mean service time of Lathe Machine 3 (in secs):  1.3
Enter the mean service time of the Robot (in secs):  7

Series Queues with Infinite Capacity - Open Jackson Network
Mean arrival rate per second               : 0.0833
Mean service rate per second of Lathe 1    : 1.0000
Mean service rate per second of Lathe 2    : 0.6667
Mean service rate per second of Lathe 3    : 0.7692
Mean service rate per second of Robot      : 0.1429

Average number of objects in each system (Ls):
Lathe 1: 0.091
Lathe 2: 0.143
Lathe 3: 0.121
Robot  : 1.400
Total system: 1.755

Average number of objects in each conveyor/queue (Lq):
Lathe 1: 0.008
Lathe 2: 0.018
Lathe 3: 0.013
Robot  : 0.817

Average waiting time of an object in system (W) in secs:
Lathe 1: 1.091
Lathe 2: 1.714
Lathe 3: 1.458
Robot  : 16.800
Total system: 21.063

Average waiting time of an object in queue/conveyor (Wq) in secs:
Lathe 1: 0.091
Lathe 2: 0.214
Lathe 3: 0.158
Robot  : 9.800
````

## Result

Thus, The Python program is implemented and executed successfully.
