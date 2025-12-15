# Autoscaler + Load Balancer + Workers + Queue Backend Roadmap

## 1. Setup & Boilerplate
- [✅] Initialize project folder
- [✅] Setup Node.js / Python backend with REST APIs
- [✅] Add Dockerfile for worker containers
- [✅] Setup basic logging system (console + optional file)

## 2. Worker Container
- [✅] Make a containerized worker server
- [✅] Expose endpoint `/process-task` that:
  - [✅] Accepts a task
  - [✅] Simulates work (2-min delay or configurable)
- [✅] Expose `/metrics` endpoint:
  - [✅] Tasks processed
  - [✅] Active / current task count

## 3. Queue System
- [✅] Implement a task queue (in-memory or Redis)
- [✅] API endpoint `/enqueue-task` to add tasks
- [✅] API endpoint `/dequeue-task` for workers to fetch tasks
- [✅] Track queue length in real-time
- [✅] When a request is added to the queue, automatically trigger `processTask` if dispatcher/scaler is idle

## 4. Load Balancer
- [✅] Implement REST API endpoint `/dispatch-task`
- [✅] Logic for dispatching tasks:
  - [✅] Round-robin / least-connections worker selection
  - [✅] Forward task from queue to selected worker

## 5. Autoscaler
- [✅] Monitor:
  - [✅] Queue length
  - [✅] Worker utilization (tasks in progress)
- [✅] Scaling rules:
  - [✅] If queue length > threshold → start new worker container
  - [✅] If queue length = 0 & workers idle → stop container
- [✅] Use Docker SDK / CLI to start/stop worker containers programmatically
- [✅] Safe scaling improvements
  - [✅] Add short (1s) delay or lock before next container spawn (prevent race)
  - [✅] Remove port and worker info cleanly on container stop
  - [✅] Log assigned port + container ID for debugging
  - [✅] Expose `/autoscaler-status` endpoint for frontend

## 6. Metrics API
- [✅] metric

## 7. Testing & Simulation
- [✅] Script to simulate incoming requests (traffic generator)
- [✅] Test:
  - [✅] Load balancing
  - [✅] Autoscaling triggers
  - [✅] Queue handling
  - [✅] Dynamic port assignment stability
- [✅] Log everything for verification

---

### In Future:
- [✅] Add async safe queue or Redis
- [✅] Retry of tasks
- [⬜] Predictive or pre-warm scaling

---

## Next Step After Backend
- [✅] Frontend dashboard to visualize:
  - [✅] Active containers & load
  - [✅] Queue length
  - [✅] Requests processed per container
  - [✅] Autoscaling events over time


## My Contribution

- Implemented the custom autoscaling logic for worker containers, including:
  - Defining metrics to track queue length / load.
  - Writing the autoscaler module to decide when to scale up or scale down workers.
  - Integrating the autoscaler with Docker so new worker containers are created and removed automatically.
- Contributed to the frontend dashboard:
  - Built the components that display worker ports, load, and active/inactive status.
  - Connected the UI to the backend APIs so autoscaling metrics are updated in real time.
  - Helped with styling/layout to keep the grid view clear and responsive.
