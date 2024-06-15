# 1. What else to know to build reliable, scalable, and fast systems

Imagine you're organizing a big event with friends in different places. Sometimes, things can go wrong because everyone is in different locations and not everyone has the same information at the same time. Distributed systems have similar issues. Here are some common problems:

1. **Transient Network Issues:** Think of it like a hiccup in your internet connection that fixes itself quickly.
2. **Long-lasting Network Issues:** This is like when your internet goes out for a long time.
3. **Consumer Application Failures:** Imagine if your friends' phones run out of battery and they can't communicate.
4. **Performance Degradation:** This is like when everything starts running slower because too many people are using the same Wi-Fi.
5. **Timeouts:** Imagine waiting too long for a friend to reply and giving up.
6. **Sudden Burst of Incoming Messages:** Like getting too many text messages at once and not being able to read them all.
7. **Gradual Increase in the Number of Messages:** Similar to more and more people joining your event over time, needing more resources.

### Deep Dive and Important Points:

1. **Network Problems:**

   - **Transient Network Issues:** These are temporary and usually resolve themselves.
   - **Long-lasting Network Issues:** These require intervention to fix.

2. **Application Failures:** Systems can fail due to bugs, overload, or resource exhaustion.

3. **Performance Issues:** Systems can slow down under heavy load or due to inefficient code.

## System Design Concepts that Help Solve These Problems

To fix these problems, there are several concepts in system design that can help:

1. **Retries and Idempotency:**

   - **Retries:** Trying the same action again if it fails.
   - **Idempotency:** Ensuring that repeating an action doesn't cause additional effects.

2. **Backoff with Jitter:** Waiting longer periods before retrying, with some randomness to avoid repeated clashes.

3. **Failover and Fallback:**

   - **Failover:** Switching to a backup system if the primary one fails.
   - **Fallback:** Using an alternative method if the main one doesn't work.

4. **Message Delivery Guarantees:** Ensuring that messages are delivered correctly even if there are issues.

5. **Batching and Compression:** Grouping multiple messages together and compressing them to save space and time.

6. **Horizontal and Vertical Scaling:**

   - **Horizontal Scaling:** Adding more machines to share the load.
   - **Vertical Scaling:** Adding more power to existing machines.

7. **Autoscaling:** Automatically adding or removing resources based on the current load.

8. **Partitioning:** Splitting data into smaller parts to manage it more easily.

9. **Load Shedding and Rate Limiting:**

   - **Load Shedding:** Dropping some work to save the system from overload.
   - **Rate Limiting:** Controlling the number of requests to a system to prevent overload.

10. **Circuit Breaker and Bulkhead:**
    - **Circuit Breaker:** Stopping calls to a failing service to prevent further issues.
    - **Bulkhead:** Isolating different parts of a system to prevent failure from spreading.

## Three-Tier Architecture

Imagine your system is a big cake with three layers. Each layer has a specific role:

1. **Presentation Tier:** This is the top layer, like the icing. It's what users see and interact with.

   - Responsible for displaying data to users.
   - Examples: Web pages, mobile apps.

2. **Application Tier:** This is the middle layer, like the filling. It handles the logic and processing of the system.

   - Contains the business logic.
   - Processes requests from the presentation tier.
   - Examples: Web servers, application servers.

3. **Data Tier:** This is the bottom layer, like the cake base. It stores all the data.

   - Manages data storage and retrieval.
   - Examples: Databases, file storage systems.

### Mermaid Diagram:

```mermaid
graph LR
    A[Presentation Tier] --> B[Application Tier]
    B --> C[Data Tier]
```

## Summary

Building reliable, scalable, and fast systems involves understanding and addressing common problems in distributed systems. Key system design concepts, such as retries, idempotency, failover, and autoscaling, help solve these issues. The three-tier architecture, consisting of presentation, application, and data tiers, organizes system components to enhance manageability and performance.
