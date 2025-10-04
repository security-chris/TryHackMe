# Snort Challenge - Live Attacks

## Introduction

### Question 1

Read the task above.

#### Answer

No answer needed

## Scenario 1 | Brute Force

### Question 1

First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

    Create the rule and test it with "-A console" mode. 
    Use "-A full" mode and the default log path to stop the attack.
    Write the correct rule and run the Snort in IPS "-A full" mode.
    Block the traffic at least for a minute and then the flag file will appear on your desktop.

Stop the attack and get the flag (which will appear on your Desktop)

#### Answer

To take a look at the traffic, I ran the following command:

```sudo snort -vde -l /var/log/snort -K ascii``` 

I then investigated the files in the /var/log/snort directory and noticed that traffic was coming from 3 main IPs:

```
10.10.245.36
10.201.10.0
10.201.152.193
```

If you look in each of these directories you will see different patterns but what is interesting is for 10.10.245.36 there is a pattern of ports, they keep increasing by 2:

```
TCP:46452-22  TCP:46472-22  TCP:46672-22  TCP:46822-22  TCP:46846-22
TCP:46454-22  TCP:46474-22  TCP:46674-22  TCP:46824-22  TCP:46850-22
TCP:46456-22  TCP:46476-22  TCP:46678-22  TCP:46826-22  TCP:46852-22
TCP:46458-22  TCP:46478-22  TCP:46680-22  TCP:46830-22  TCP:46854-22
TCP:46460-22  TCP:46480-22  TCP:46682-22  TCP:46832-22  TCP:46856-22
TCP:46462-22  TCP:46482-22  TCP:46684-22  TCP:46834-22  TCP:46858-22
TCP:46464-22  TCP:46484-22  TCP:46686-22  TCP:46836-22  TCP:46860-22
TCP:46466-22  TCP:46666-22  TCP:46688-22  TCP:46838-22  TCP:46862-22
TCP:46468-22  TCP:46668-22  TCP:46690-22  TCP:46842-22  TCP:46864-22
TCP:46470-22  TCP:46670-22  TCP:46692-22  TCP:46844-22
```
To stop this attack, add the following rule to /etc/snort/rules/local.rules:

```drop tcp 10.10.245.36 any -> any 22 (msg: "SSH Brute Force Attack Detected"; sid:1000001; rev:1;)```

Then test the UPS mode with:

```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console```

You should see a number of packets being dropped. If so, you can run this in full mode with:

```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full -l /var/log/snort```

After about a minute you will be alerted that you stopped the attack and will get a flag.txt file on your desktop.

Answer:**THM{81b7fef657f8aaa6e4e200d616738254}**

### Question 2

What is the name of the service under attack?

#### Answer

Answer:**ssh**

### Question 3

What is the used protocol/port in the attack?

#### Answer

Answer:**tcp/22**

## Scenario 2 | Reverse-Shell

### Question 1

First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

    Create the rule and test it with "-A console" mode. 
    Use "-A full" mode and the default log path to stop the attack.
    Write the correct rule and run the Snort in IPS "-A full" mode.
    Block the traffic at least for a minute and then the flag file will appear on your desktop.

Stop the attack and get the flag (which will appear on your Desktop)

#### Answer

Check the attack using:

```sudo snort -vde -l /var/log/snort -K ascii```

Then become root so you can view the logs:

```sudo -i```

Inside of the /var/log/snort you will see the following directories now:

10.10.144.156  10.10.196.55  10.10.63.58  10.100.67.236  PACKET_NONIP  alert

If we cd into 10.10.144.156 we will see the following:

```
TCP:43332-4444  TCP:43338-4444  TCP:43344-4444  TCP:43350-4444
TCP:43334-4444  TCP:43340-4444  TCP:43346-4444  TCP:43352-4444
TCP:43336-4444  TCP:43342-4444  TCP:43348-4444  TCP:43354-4444
```

This is most likely the attack because it is similar to the last one with incrementing source ports. Lets right a rule to defend this:

```drop tcp 10.10.144.156 any -> any 4444 (msg: "Brute-Force blocked"; sid:10000001; rev:1;)```

Test this rule in console mode with the following:

```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console```

We should see a number of packets getting blocked so now we can run it with -A full:

```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full -l /var/log/snort```

After about a minute we will get a notification that we stopped the attack and will receive the flag.txt on our desktop.

Answer:**THM{0ead8c494861079b1b74ec2380d2cd24}**

### Question 2

What is the used protocol/port in the attack?

#### Answer

Answer:**tcp/4444**

### Question 3

Which tool is highly associated with this specific port number?

#### Answer

Answer:**Metasploit**

