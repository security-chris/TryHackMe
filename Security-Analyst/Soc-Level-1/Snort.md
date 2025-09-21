# Snort Walkthrough and Documentation

## Task 1

Task 1 of the Snort room is an introduction. It recommends the [Network Fundamentals](https://tryhackme.com/module/network-fundamentals) room as a prerequisite to this room. It also recommends to have a knowledge of the Linux Command line and to potentially use the Linux Fundamentals rooms as well for this:[1](https://tryhackme.com/room/linuxfundamentalspart1) [2](https://tryhackme.com/room/linuxfundamentalspart2)  [3](https://tryhackme.com/room/linuxfundamentalspart3). Here, you can find some beginner information about [Snort](https://www.snort.org/).

### Question 1

Read the task above.

#### Answer

No answer needed.

## Task 2

Task 2 of the Snort room will require you to Start a virtual machine to access interactive material. The Virtual Machine will look like this and will contain a "Task Exercises" folder:

![Desktop VM](images/desktop-vm.png)

In the "Task-Exercises" folder, there is a script "traffic-generator.sh" that is used to generate traffic for Snort since the machine has no internet connection.

![Task Exercises](images/task-exercises-folder.png)

### Question 1

Navigate to the Task-Exercises folder and run the command "./.easy.sh" and write the output

#### Answer 

Too Easy!

![Easy Script Output](images/easy-script-output.png)

## Task 3

Task 3 in the Snort room is all about the differences between detection and prevention (IPS vs IDS). The biggest difference is that IDS detect and IPS detects and prevents (takes action on). IDS has:

- Network-Based Intrusion Detection System (NIDS)
- Host-Based Intrusion Detection System (HIDS) 

IPS has 4 different types which are:

- Network Intruction Prevention System (NIPS)
- Behavior-based Intrusion Prevention System (Network Behavior Analysis - NBA)
- Wireless Intrusion Prevention System (WIPS)
- Host-based Intrusion Prevention System (HIPS)

### Question 1

Which IDS or IPS type can help you stop the threats on a local machine?.

#### Answer

HIPS

### Question 2

Which IDS or IPS type can help you detect threats on a local network?

#### Answer

NIDS

### Question 3

Which IDS or IPS type can help you detect the threats on a local machine?

#### Answer

HIDS

### Question 4

Which IDS or IPS type can help you stop the threats on a local network?

#### Answer

NIPS

### Question 5

Which described solution works by detecting anomalies in the network?

#### Answer

NBA

### Question 6

According to the official description of the snort, what kind of NIPS is it?

#### Answer

full-blown

### Question 7

NBA training period is also known as ...

#### Answer

baselining










