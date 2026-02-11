# 5G QoS Viva Questions and Answers

## 1. What is Quality of Service (QoS) in 5G?

**Answer:**
Quality of Service (QoS) in 5G is a framework that ensures different applications receive guaranteed performance levels such as latency, throughput, and reliability based on their requirements.

**Example:**
- Voice calls -> low latency
- Video streaming -> high throughput
- IoT -> high reliability

**One-line answer:**
QoS ensures critical traffic gets priority service in 5G networks.

## 2. Why is resource management important in modern 5G networks?

**Answer:**
5G networks serve thousands of users simultaneously with limited spectrum. Resource management ensures fairness, efficiency, and QoS satisfaction without wasting bandwidth.

**One-line answer:**
Resource management balances performance and fairness under limited bandwidth.

## 3. What is 5QI and why is it important?

**Answer:**
5QI (5G QoS Identifier) is a standardized label that defines how a data flow should be treated in the network, including its priority, delay budget, and reliability.

**Example:**
- URLLC -> very low latency
- Best-effort -> normal priority

## 4. What are the key QoS parameters in 5G?

**Answer:**
The key QoS parameters are:
- Latency - delay in data transmission
- Throughput - data rate (Mbps/Gbps)
- Packet loss - percentage of lost packets
- 5QI - defines traffic behavior

## 5. Why does QoS depend on application-specific requirements?

**Answer:**
Different applications have different needs:
- Voice -> low latency
- Video -> high bandwidth
- IoT -> ultra-low latency and reliability

QoS ensures each application gets the right combination of resources.

## 6. What is priority-based traffic handling in 5G?

**Answer:**
5G classifies traffic into priority tiers, ensuring emergency and critical services receive resources first during congestion, while background traffic uses remaining capacity.

## 7. What is a QoS bearer in 5G?

**Answer:**
A QoS bearer is a dedicated data path that guarantees specific performance characteristics for a data flow across the 5G network.

**Analogy:**
Like separate lanes on a highway for ambulances and normal vehicles.

## 8. What are the steps in QoS bearer configuration?

**Answer:**
1. Define service requirements.
2. Configure dedicated bearers with 5QI.
3. Enable network differentiation.

This ensures critical traffic always meets QoS targets.

## 9. What is KPI collection and why is it needed?

**Answer:**
KPI collection is used to monitor and validate QoS effectiveness by measuring real-time network performance.

**Purpose:**
To check whether QoS policies are actually working.

## 10. Which KPIs are monitored for QoS effectiveness?

**Answer:**
- Throughput
- Latency
- Packet loss
- Resource utilization
- Fairness across users

## 11. What is fairness and efficiency in scheduling?

**Answer:**
- Fairness ensures no user is starved.
- Efficiency ensures maximum resource utilization.

Schedulers balance both to prevent bottlenecks.

## 12. What is the role of the gNB in scheduling?

**Answer:**
The gNodeB (gNB) acts as an intelligent traffic controller, allocating Physical Resource Blocks (PRBs) every millisecond based on QoS and channel conditions.

## 13. How does downlink scheduling differ from uplink scheduling?

**Answer:**
- Downlink: fully controlled by gNB.
- Uplink: UEs request resources, gNB grants them.

Uplink scheduling is more complex due to multiple transmitters.

## 14. What are the main scheduling objectives in 5G?

**Answer:**
- Fairness
- Spectral efficiency
- QoS satisfaction

Schedulers dynamically balance these goals.

## 15. Which scheduling algorithms are discussed in your PPT?

**Answer:**
- Proportional Fair - balances fairness and throughput
- Maximum Throughput - maximizes data rate
- QoS-Aware - prioritizes critical applications

## 16. Why is Proportional Fair scheduling important?

**Answer:**
It prevents starvation while still maintaining good throughput, making it suitable for mixed traffic environments.

## 17. What is multi-user optimization in 5G?

**Answer:**
Multi-user optimization allows simultaneous transmission to multiple users using techniques like MU-MIMO and beamforming, improving capacity without extra spectrum.

## 18. Why is multi-user optimization needed in dense networks?

**Answer:**
In dense areas like stadiums or cities, traditional single-user transmission is inefficient. Multi-user optimization improves capacity and user experience.

## 19. How do QoS, scheduling, and optimization work together?

**Answer:**
- QoS defines requirements.
- Scheduling allocates resources.
- Optimization maximizes capacity.

Together, they form a complete resource management framework.

## 20. What real-world example demonstrates this framework?

**Answer:**
- VoNR -> ultra-low latency
- Video streaming -> high throughput
- File downloads -> best-effort

Schedulers dynamically allocate resources to satisfy all flows efficiently.

## 21. What are the main performance bottlenecks in 5G scheduling?

**Answer:**
- Limited spectrum
- High user density
- Scheduler complexity
- Channel variability

## 22. How can scheduling logic be optimized further?

**Answer:**
- Dynamic parameter tuning
- AI/ML-based scheduling
- Better KPI feedback loops
- Improved interference management

## 23. What role did you play in this project? (Safe Answer)

**Answer:**
I contributed to understanding QoS concepts, scheduling logic, and KPI analysis, and helped in explaining the design and performance aspects during implementation and presentation.

## Final Viva-Saving Line (Very Important)

Our project demonstrates how QoS-driven scheduling combined with multi-user optimization enables efficient, fair, and high-performance 5G networks.
