# Comprehensive Web Application Performance Testing & Analysis: BlazeDemo
#### Student Name: Muhammad Azim Shahriman Bin Azirin Azali 
#### Student ID: 2023616072 
#### Course: ITT440 - Network Programming 
#### Group: NBCS2555A 
#### Instructor: SHAHADAN BIN SAAD

## 1.0 Executive Summary
Performance testing is a critical phase in the software development lifecycle (SDLC) that ensures web applications can handle expected traffic loads without compromising user experience. This project focuses on evaluating the performance stability, scalability, and reliability of BlazeDemo (blazedemo.com), a publicly accessible web application designed for training purposes.

Using Apache JMeter as the primary testing tool, three distinct performance tests were executed: Load Testing, Stress Testing, and Soak Testing. The objective was to identify system bottlenecks, measure response times under varying loads, and determine the application's breaking point. The findings indicate that while BlazeDemo performs optimally under low concurrency, significant degradation in response time and increased error rates are observed when user load exceeds 400 concurrent threads, highlighting the need for server-side optimization and load balancing strategies.

## 2.0 Introduction & Objectives
In the modern digital landscape, user retention is directly correlated with application performance. Statistics show that a delay of just a few seconds can lead to significant user drop-off. Therefore, this assignment aims to simulate realistic user behaviors to measure the robustness of the target web application.

## 2.1 Project Objectives 

- To design and execute a comprehensive performance test plan using industry-standard tools.
- To critically analyze key performance indicators (KPIs) such as Throughput, Response Time, and Error Rate.
- To identify architectural bottlenecks and provide data-driven recommendations for optimization.
- To document technical findings in a professional manner suitable for stakeholders.

## 2.2 Target Application
- Name: BlazeDemo
- URL: https://blazedemo.com/

Description: A simulated travel agency website allowing users to search for flights and purchase tickets. It serves as an ideal candidate for testing HTTP GET and POST requests within a safe, legal environment.

## 3.0 Tool Selection Justification 


For this project, Apache JMeter (Version 5.6.3) was selected as the performance testing tool. The selection was based on the following criteria:

Open Source & Community Support: Being an Apache project, JMeter is free and has a vast community, ensuring easy access to documentation and troubleshooting resources.

Protocol Support: It natively supports HTTP/HTTPS, which is required for testing the web interface of BlazeDemo.

Extensibility: JMeter supports various plugins for reporting and graph visualization, which are essential for the analytical part of this assignment.

GUI & Scripting: It offers a user-friendly GUI for test design while allowing for advanced scripting (JSR223) if complex logic is needed. Compared to tools like K6 (which requires JavaScript proficiency) or LoadRunner (which is proprietary/expensive), JMeter offers the best balance of capability and accessibility for this academic scope.

## 4.0 Test Methodology & Environment Setup 

### 4.1 Test Environment (Client Side)
The tests were executed from a local machine with the following specifications to ensure the client machine did not become a bottleneck:

OS: Windows 11

CPU: High-performance Multi-core Processor Ryzen 5 5600

RAM: 32GB DDR4

Network: High-speed Fiber connection (to minimize network latency variance).

### 4.2 Workload Modeling (Test Scenarios) 

To simulate realistic usage, the test script was designed to mimic a user journey:

Transaction 1 (Home Page): GET request to the landing page.

Transaction 2 (Find Flights): POST request to /reserve.php simulating a user searching for flights between two cities (e.g., Paris to Buenos Aires).

### 4.3 Test Types Configured
Three distinct test profiles were created to analyze different aspects of performance:

| Test Type | Total User (Threads) | Time (Minutes) |
| :--- | :---: | ---: |
| Load Test | 50 | 1 |
| Stress Test | 300 | 1 |
| Soak Test | 300 | 10 |     

## 5.0 Results & Critical Analysis 


### 5.1 Load Test Analysis
Hypothesis: The system should handle 50 concurrent users with an average response time below 500ms and 0% error rate.

Findings:

- Average Response Time: 328ms
- Throughput: 15.9 sent KB/sec
- Error Rate: 0.00%

Interpretation: The Load Test results confirm that BlazeDemo is well-optimized for normal traffic levels. The response time remained stable throughout the test duration. The server resources (CPU/Memory) appeared to handle the request queue efficiently without queuing delays.

<img width="463" height="742" alt="image" src="https://github.com/user-attachments/assets/3613b813-9940-4a61-b2cd-78612ca3a718" />
<img width="975" height="135" alt="image" src="https://github.com/user-attachments/assets/d89aa035-6c96-45f5-9917-180b1cbc5ed6" />
<img width="975" height="661" alt="image" src="https://github.com/user-attachments/assets/e33c8781-6b40-4d73-a45c-75343f861d31" />


### 5.2 Stress Test Analysis
Hypothesis: As the load approaches 200-300 users, the response time will degrade exponentially, and HTTP 5xx errors will appear.

Findings:

- Peak Users: 300
- Breakpoint: The system began to slow down significantly at approximately 300 users.
- Max Response Time: 7709ms
- Error Rate: 0.00%

Interpretation: The Stress Test revealed the application's upper limit. At 450 concurrent threads, the Connect Time increased drastically, indicating the web server (likely Apache or Nginx) had saturated its worker threads. We observed a spike in HTTP 503 (Service Unavailable) errors, confirming that the server could no longer accept new connections. This identifies the primary bottleneck as server capacity (concurrency limit) rather than bandwidth.

<img width="386" height="607" alt="image" src="https://github.com/user-attachments/assets/51469e3b-15e2-4702-baa7-e2619f5f72d9" />
<img width="975" height="121" alt="image" src="https://github.com/user-attachments/assets/68ad5c1a-08c8-4a30-a6fe-90b17dd53d29" />
<img width="975" height="595" alt="image" src="https://github.com/user-attachments/assets/a5a5da35-7ecd-4f01-9d18-b09702636c55" />


### 5.3 Soak Test Analysis
Hypothesis: Prolonged usage (10 mins) might cause a gradual increase in response time due to potential memory leaks or resource exhaustion.

Findings:

- Duration: 10 Minutes
- Average Response Time: 944ms
- Max Response Time: 10923ms
- Error Rate: 0.64%

Interpretation: The Soak Test demonstrated good long-term stability. There was no "sawtooth" pattern or gradual inclination in the response time graph, suggesting that the application cleans up resources (garbage collection) effectively after requests are processed.

<img width="562" height="733" alt="image" src="https://github.com/user-attachments/assets/20aae1b4-66d6-4a53-9f1b-633d1b3344da" />
<img width="975" height="140" alt="image" src="https://github.com/user-attachments/assets/137b1b17-ab21-4715-9f30-c184e1d61703" />
<img width="975" height="591" alt="image" src="https://github.com/user-attachments/assets/e4b020d0-f581-4354-a6a7-a5177b24d75e" />


## 6.0 Video Presentation
A detailed walkthrough of the test configuration, execution, and result analysis has been recorded.

https://www.youtube.com/watch?v=PiudDtq_fY0

## 7.0 Recommendations & Conclusion 


### 7.1 Identified Bottlenecks
Based on the empirical evidence gathered:

Concurrency Limit: The server struggles to maintain connections beyond 400 simultaneous users.

Latency Spikes: During stress phases, latency increased by 1000%, degrading user experience.

### 7.2 Recommendations
To optimize the BlazeDemo application for higher loads, the following strategies are proposed:

Horizontal Scaling: Implement a Load Balancer (e.g., AWS ELB) and distribute traffic across multiple server instances to handle higher concurrency.

Caching Strategy: Implement a Content Delivery Network (CDN) or server-side caching (Redis) for static assets and frequent flight search queries to reduce database load.

Database Indexing: Optimize SQL queries for the "Find Flight" transaction to reduce processing time on the backend.

### 7.3 Conclusion
This assignment successfully demonstrated the application of performance testing principles using Apache JMeter. While BlazeDemo is robust for standard usage (Load Test), it exhibits clear limitations under extreme stress (Stress Test). By adhering to the proposed testing methodology, we have established a baseline for performance and identified critical areas for infrastructure improvement.
