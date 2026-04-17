# SDN Learning Switch Controller using Ryu & Mininet

## 📌 Problem Statement
Implement a Software Defined Networking (SDN) controller that mimics a learning switch by dynamically learning MAC addresses and installing forwarding rules using OpenFlow.

---

## 🎯 Objective
- Understand controller-switch interaction
- Implement MAC learning logic
- Install dynamic flow rules
- Validate packet forwarding
- Analyze basic network performance

---

## 🛠️ Tools & Technologies
- Ryu Controller (Python 3.8)
- Mininet
- Open vSwitch (OVS)
- OpenFlow 1.3
- Ubuntu Linux

---

## ⚙️ Setup & Execution Steps

### 1. Activate virtual environment

source ryu-env/bin/activate

### 2. Run RYU Controller

ryu-manager learning_switch.py

### 3. Start mininet (in new terminal)

sudo mn --topo single,3 --controller remote --switch ovsk,protocols=OpenFlow13



## Testing and Validation

### 1. Connectivity test

ping all

### 2. MAC Learning and Flow Installation

sh ovs-ofctl -O OpenFlow13 dump-flows s1

### 3. Failure Scenario (Link Down)

link s1 h1 down
h1 ping -c 3 h2

### 4. Throughput Test (iperf)

h2 iperf -s &
h1 iperf -c 10.0.0.2


# Working Explanation

When a packet arrives, the controller learns the source MAC address and maps it to the incoming port.
If the destination MAC is known, a flow rule is installed in the switch.
Future packets are forwarded directly without contacting the controller.
If the destination is unknown, packets are flooded to all ports.

# Observations
Initial packets are flooded before learning
After learning, flow rules reduce controller load
Link failure results in loss of connectivity
High bandwidth observed due to virtual environment
