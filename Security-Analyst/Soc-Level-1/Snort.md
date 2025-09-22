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

## Task 4

We can verify snort is installed and verify the version by running the following:

```snort -V```

We can also make sure that our snort configuration file is correct by running the following:

```sudo snort -c /etc/snort/snort.conf -T```

### Question 1

Run the Snort instance and check the build number.

#### Answer

149

![Snort Build](images/snort-build.png)

### Question 2

Test the current instance with "/etc/snort/snort.conf" file and check how many rules are loaded with the current build.

#### Answer

4151

![Snort Rules Read](images/snort-rules-read.png)

### Question 3

Test the current instance with "/etc/snort/snortv2.conf" file and check how many rules are loaded with the current build.

#### Trials

For this, we can use the following command:

```sudo snort -c /etc/snort/snortv2.conf -T```

#### Answer

1

![Snort Conf v2 Rules](images/snort-rules-v2.png)

## Task 5

In Snort, you can sniff with -i parameter to specify an interface you would like to "sniff". For example, if I wanted to sniff traffic on the eth0 interface I would run the following:

```sudo snort -v -i eth0```

If we want to run snort in verbose mode(-v) (this will show the packets inside of the terminal) we can do the following:

```sudo snort -v```

We can also run snort in the dumping packet data mode(-d), which will be similar to verbose mode but with more data:

```sudo snort -d```

Similarly, we can run snort in dumping packet data mode (-d) along with link-layer heading grabbing (-e):

```sudo snort -d -e```

Finally, we can run with full packet data dump mode (-X):

```sudo snort -X```

### Snort Parameters

**`-v`** - Verbose. Display the TCP/IP output in the console.

**`-d`** - Display the packet data (payload).

**`-e`** - Display the link-layer (TCP/IP/UDP/ICMP) headers.

**`-X`** - Display the full packet details in HEX.

**`-i`** - This parameter helps to define a specific network interface to listen/sniff.

### Question 1

You can practice the parameter combinations by using the traffic-generator script.

#### Answer

No answer needed

## Task 6

### Snort in Logger Mode Parameters

**`-l`** - Logger mode, target log and alert output directory. Default output folder is /var/log/snort The default action is to dump as tcpdump format in /var/log/snort

**`-K ASCII`** - Log packets in ASCII format.

**`-r`** - Reading option, read the dumped logs in Snort.

**`-n`** - Specify the number of packets that will process/read. Snort will stop after reading the specified number of packets.

We can start snort in packet logger mode with the following command:

```sudo snort -dev -l .```

This will create a file in binary/tcpdump format.

To create a log in readable format, we can run the following:

```sudo snort -dev -K ASCII -l .```

You can also pass the `-r` parameter to read a snort log:

```sudo snort -r snort.log.1758560978```

**Note the log name will be different**

### Question 1

Investigate the traffic with the default configuration file with ASCII mode.

```sudo snort -dev -K ASCII -l .```
Execute the traffic generator script and choose "TASK-6 Exercise". Wait until the traffic ends, then stop the Snort instance. Now analyse the output summary and answer the question.

```sudo ./traffic-generator.sh```
Now, you should have the logs in the current directory. Navigate to folder "145.254.160.237". What is the source port used to connect port 53?

#### Answer

3009

![Task 6 Question 1](images/task6-question1.png)

### Question 2

Use snort.log.1640048004 

Read the snort.log file with Snort; what is the IP ID of the 10th packet?

```snort -r snort.log.1640048004 -n 10```

#### Answer

49313

Navigate to the Task 6 directory from the home directroy:

```cd Desktop/Task-Excercies/TASK-6```

From there, run the command in the question:

```snort -r snort.log.1640048004 -n 10```

![Task 6 Question 2](images/task6-question2.png)

### Question 3

Read the "snort.log.1640048004" file with Snort; what is the referer of the 4th packet?

#### Answer

http://www.ethereal.com/development.html

To find this answer, you can use the `-X` to display the results in ASCII format. Run the following command:

```snort -Xr snort.log.1640048004 -n 4```

The refferer will be right down at the bottom of the packet.

![Task 6 Question 3](images/task6-question3.png)

### Question 4

Read the "snort.log.1640048004" file with Snort; what is the Ack number of the 8th packet?

#### Answer

0x38AFFFF3

Similar to the last question. Use the following command:

```snort -Xr snort.log.1640048004 -n 8```

On the 8th packet you will see an ACK field. There is your answer.

![Task 6 Question 4](images/task6-question4.png)

### Question 5

Read the "snort.log.1640048004" file with Snort; what is the number of the "TCP port 80" packets?

#### Answer

41

This question is just looking for the numbert of packets that fit this description. Here is the command I used:

```snort -r snort.log.1640048004 'tcp and port 80'

![Task 6 Question 5](images/task6-question5.png)



















