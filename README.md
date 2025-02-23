[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: CHEN, Hao 
### Student Id: 21093529 
### Email: howie.c@outlook.com | hchenem@connect.ust.hk 

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Phoronix Test Suite  
    > All configurations are maintained at the default settings.  
    > For CPU performance evaluation, the **Compression Rating** is used as the measurement metric. The unit is **MIPS** , which indicates how many millions of instructions are executed per second. There is a positive correlation between this value and CPU performance - generally, the higher the MIPS value, the stronger the CPU performance.  
    > For memory performance evaluation, **RAMspeed** (memory speed) is measured using **integer copy** operations. The unit is **MB/s** (Megabytes Per Second), which reflects the data transfer rate during the copying process. A higher MB/s value indicates stronger memory performance.  

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro`  |  3560 MIPS      |   10635.20 MB/s    |
    | `t2.medium` |  10084 MIPS     |   19706.86 MB/s    |
    | `c5d.large` |  8107 MIPS      |   15254.17 MB/s    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |   3,960        |  0.208   |
    | `m5.large` - `m5.large`   |   4,960        |  0.152   |
    | `c5n.large` - `c5n.large` |   4,940        |  0.148   |
    | `t3.medium` - `c5n.large` |   2,400        |  0.595   |
    | `m5.large` - `c5n.large`  |   2,440        |  0.616   |
    | `m5.large` - `t3.medium`  |   4,470        |  0.230   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |    32.8        |  61.621  |
    | N. Virginia - N. Virginia |    3,450       |  0.303   |
    | Oregon - Oregon           |    4,470       |  0.191   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
