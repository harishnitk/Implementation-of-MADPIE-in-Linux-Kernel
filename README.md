# Implementation of MADPIE algorithm in Linux kernel

## Course Code: CS822

## Assignment: #FP4

### Overview 

Maximum and Average queuing Delay with Proportional Integral controller Enhanced (MADPIE) [1] is an extension of PIE [2], that adds deterministic packet drops at controlled intervals. This repository provides an implementation of MADPIE in the Linux kernel.

### Compiling and Installing the kernel

1. Configure the kernel

   `make menuconfig`

2. Compile the kernel

   `make`

3. Build and install the modules

   `make modules`

   `make modules_install`

4. Install the kernel

   `make install`

### Testing the kernel using FLENT

1. Setup a physical topology 

   `Client <---> Router <---> Server`

2. Create a separate passwordless ssh connection between client and router so that flent can collect queue statistics from router

3. Install Netserver in server machine

4. Install FLENT in client machine

5. Install the kernel in router machine

6. Run FLENT for plotting differnt graphs 

#### Command

   `./run-flent rrul -p [PLOT_NAME] -l 160 -H [SERVER_IP] --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=          [ROUTER_SSH_IP] --test-parameter qdisc_stats_interfaces=[ROUTER_AQM_INTERFACE] --test-parameter upload_streams=num_cpus --test-     parameter download_streams=num_cpus -t MADPIE -o ~/Desktop/MADPIE/test.png`

PLOT_NAME - The type of graph needed

SERVER_IP - IP Address of the server

ROUTER_SSH_IP - IP Address using which ssh connection is setup with router 

#### Example

   `./run-flent rrul -p all_scaled -l 160 -H 172.16.10.2 --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=           192.168.20.2 --test-parameter qdisc_stats_interfaces=eth1 --test-parameter upload_streams=num_cpus --test-parameter                 download_streams=num_cpus -t MADPIE -o ~/Desktop/MADPIE/test.png`

### References

[1] Kuhn, N., & Ros, D. (2016). Improving PIE's performance over high-delay paths. arXiv preprint arXiv:1602.00569.

[2] Pan, R., Natarajan, P., Piglione, C., Prabhu, M. S., Subramanian, V., Baker, F., & VerSteeg, B. (2013, July). PIE: A lightweight control scheme to address the bufferbloat problem. In High Performance Switching and Routing (HPSR), 2013 IEEE 14th International Conference on (pp. 148-155). IEEE.
