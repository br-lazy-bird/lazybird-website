---
title: "Project Management - Broken System 2 - Product Catalog"
date:  2025-10-08 17:10:05
categories: ["Lazy Bird Project"]
tags: []
---

## Domain Description

E-commerce product page system demonstrating API call optimization through sequential vs parallel request patterns. This serves as the second broken system in the Lazy Bird Project repository.

## The Specific Problem

- **Issue**: Backend makes three microservice calls sequentially instead of in parallel
- **Solution**: Use `asyncio.gather()` to parallelize independent API calls
- **Expected Outcome**: Product page load time reduces from ~3 seconds to ~1 second

## Problem Focus

**Single Issue: Sequential API Calls**

This system demonstrates one specific performance problem: sequential execution of independent API calls. The broken system contains:
- **Three Microservices**: Product, Inventory, and Reviews services with artificial delays
- **One Primary Endpoint**: GET /product/{product_id} that aggregates data from all three services
- **Single Root Cause**: Sequential await calls instead of parallel execution
- **Single Solution**: Implement `asyncio.gather()` for concurrent requests

**Why This Approach**:
- **Focused Learning**: Developers learn one async pattern thoroughly
- **Clear Cause-Effect**: Direct relationship between sequential calls and cumulative delay
- **Simple Verification**: Easy to observe timing differences
- **No Database Complexity**: Pure API optimization focus

## Problem Demonstration Strategy

1. **Broken State Delivery**: System delivered with sequential API calls
2. **Visual Feedback**: Three loading icons showing sequential execution
3. **Obvious Performance Issues**: 3-second wait time that clearly needs optimization
4. **Simple Interface**: Minimal UI focused on demonstrating the call pattern

## System Features

### Core Functionality
- **Single Endpoint**: GET /product/{product_id} aggregates three service responses
- **Three Microservices**: Each returns simple JSON data with ~1 second artificial delay
- **Simple Interface**: Button trigger with three service status components
- **No Database**: Pure API call demonstration

### Performance Visibility Features
- **Service Status Components**: Three components showing Product, Inventory, and Reviews service states
- **Stopwatch Timers**: Each service displays elapsed time while fetching (e.g., "Fetching... 1.2s")
- **Sequential Execution**: Timers run one after another in broken state, others show "Waiting..."
- **Parallel Execution**: All three timers run simultaneously after optimization

## Success Metrics

- **Load Time Reduction**: Product page loads in ~1 second instead of ~3 seconds
- **Parallel Execution**: All three services called concurrently
- **Correct Data**: All service responses properly aggregated

## Learning Objectives

**Technical Skills**:
- Understanding async/await patterns in Python
- Implementing `asyncio.gather()` for parallel execution
- Identifying sequential bottlenecks in API calls

**Problem-Solving Process**:
- Recognizing when API calls can be parallelized
- Understanding the performance impact of sequential vs parallel calls
- Verifying optimization through timing observation

## Domain-Specific Considerations

**Realistic Scenarios**: E-commerce product page represents common microservice architecture that candidates encounter in production.

**External Dependencies**: Simulates real-world scenario where backend depends on multiple external services with network latency.

**Independent Services**: Three services have no dependencies on each other, making them ideal candidates for parallelization.

## Technology Stack

**Backend**: Python with FastAPI
- Async support for demonstrating sequential vs parallel patterns
- Simple microservice implementation
- Built-in timing for performance measurement

**Frontend**: React with TypeScript
- Type safety for API responses
- Component-based architecture for service status display
- Loading state management

**Microservices**: Three separate FastAPI services
- Product Service: Returns basic product information
- Inventory Service: Returns stock availability
- Reviews Service: Returns customer reviews
- Each service has ~1 second artificial delay

**No Database**: Focus purely on API call optimization

**Deployment**: Docker Compose
- Separate containers for each microservice
- Separate container for main backend API
- Separate container for frontend
- Easy one-command startup

**Stack Rationale**: Same as 01-employee-directory system for consistency across Lazy Bird Project exercises, with microservices architecture added to demonstrate API call patterns.

## Project Structure

Following 01-employee-directory pattern:

```
lazy-bird-product-catalog/
├── backend/
│   ├── app/
│   ├── tests/
│   └── requirements.txt
├── microservices/
│   ├── product-service/
│   ├── inventory-service/
│   └── reviews-service/
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
├── docker/
│   ├── docker-compose.yml
│   ├── backend.dockerfile
│   ├── frontend.dockerfile
│   └── microservices.dockerfile
├── Makefile
├── README.md
└── DETONADO.md
```

## Frontend Design

**Lazy Bird Header**: Title and short system description

**Single Button**: "Load Product Page" to trigger API call

**Three Service Components**: 
- Product Service component with stopwatch timer
- Inventory Service component with stopwatch timer
- Reviews Service component with stopwatch timer

**Timer Behavior**:
- Before optimization: Timers run sequentially (one at a time), others show "Waiting..."
- After optimization: All three timers run simultaneously (in parallel)

**Data Display**: Simple text display of JSON responses from each service

**Styling**: Follow 01-employee-directory CSS patterns

## Testing Strategy

**Single Integration Test**: End-to-end test verifying:
- All microservices are running
- Main API endpoint successfully calls all three services
- Correct data is returned

**Containerized Testing**: Tests run inside Docker container, no local venv required

**Makefile Commands**: All common operations accessible via make commands:
- Starting services
- Running tests
- Stopping/cleaning up containers

**No Unit Tests**: Following 01-employee-directory approach

## Microservices Implementation

**Product Service** (Port 8001):
- Endpoint: GET /products/{product_id}
- Returns: {"id": "...", "name": "...", "price": ...}
- Artificial delay: ~1 second

**Inventory Service** (Port 8002):
- Endpoint: GET /inventory/{product_id}
- Returns: {"product_id": "...", "stock": ..., "warehouse": "..."}
- Artificial delay: ~1 second

**Reviews Service** (Port 8003):
- Endpoint: GET /reviews/{product_id}
- Returns: {"product_id": "...", "average_rating": ..., "review_count": ...}
- Artificial delay: ~1 second

Each service is a simple FastAPI application with a single endpoint and sleep() call.

## Candidate Modification Scope

**DO Modify**:
- `backend/` - Main API implementation with sequential calls to optimize

**DO NOT Modify**:
- `microservices/` - Mock services simulating external APIs
- Documented clearly in README

This implementation establishes the second broken system pattern in the Lazy Bird Project, focusing on API call optimization while maintaining consistency with the first system's structure and approach.