---
title: "General Framework v1.0 - [OUTDATED]"
date:  2025-09-12 16:56:55
categories: ["Lazy Bird Project"]
tags: []
---

## Project Overview

The Lazy Bird Project is a repository of intentionally broken but complete systems designed for educational purposes and hiring assessments. Rather than studying problems in isolation, this project creates realistic end-to-end applications that demonstrate how performance issues manifest across the full technology stack, from database to user interface.

## Core Philosophy

**Complete System Approach**: Instead of isolated exercises, each broken system includes frontend, backend, and database layers to show how performance problems propagate through real applications.

**Visual Problem Demonstration**: The frontend serves as a showcase for performance issues, making abstract concepts like optimization immediately tangible through user experience.

**Practical Learning Environment**: Provides controlled, reproducible environments where engineers can study and fix common production problems without real-world consequences.

## Primary Use Cases

1. **Hiring Assessments**: Standardized evaluation of candidates' optimization skills
2. **Educational Tool**: Hands-on learning platform for software engineers
3. **Interview Preparation**: Practical exercises for common technical interview scenarios

## Technical Architecture

### Project Structure Framework (Monorepo Approach)

```
broken-system-exercise/
├── backend/
│   ├── app/ (Backend application)
│   ├── database/ (models, migrations, seeds)
│   ├── tests/ (backend-specific tests)
│   └── dependencies file
├── frontend/
│   ├── src/ (Frontend application)
│   ├── public/
│   ├── tests/ (frontend tests)
│   └── dependencies file
├── docker/
│   ├── docker-compose.yml
│   ├── backend.dockerfile
│   ├── frontend.dockerfile
│   └── database.dockerfile
├── testing-infrastructure/ (protected)
│   ├── performance-tests/
│   ├── validation-scripts/
│   └── test.dockerfile
└── data/
    ├── seed-data/
    └── datasets/
```

**Structure Benefits**:
- **Single Repository**: Simplified setup and distribution
- **Clear Separation**: Each technology stack has distinct boundaries
- **Protected Testing**: Evaluation infrastructure separated from modifiable code
- **Flexible Technology Choices**: Structure supports different tech stacks based on problem requirements

### Problem Documentation & Solution Management

**DETONADO.md**: Comprehensive instruction document provided with each broken system.

**Git-Based Solution Management**:
- **Main Branch**: Contains the broken system that candidates receive
- **Solution Branch**: Contains the complete optimized implementation following DETONADO.md instructions
- **Testing Benefits**: Automated testing infrastructure can switch between branches to establish performance baselines and validate exercise effectiveness

**Automated Solution Application**:
- Testing system can checkout solution branch to measure expected performance improvements
- Baseline establishment for setting realistic improvement targets
- Regression testing to ensure broken system demonstrates intended problems
- Solution validation to verify DETONADO.md instructions actually resolve the issues
- Candidate comparison against known optimal solutions

## Cross-Environment Consistency

### Containerized Testing Strategy

1. **Docker with Resource Limits**: Standardized execution environment regardless of host machine
2. **Relative Performance Metrics**: Focus on improvement ratios rather than absolute timing
3. **Query Plan Analysis**: Hardware-independent validation of optimization approaches
4. **Cloud-Based Final Validation**: GitHub Actions or similar for consistent, reproducible results
5. **Protected Test Images**: Immutable testing infrastructure prevents manipulation

### Anti-Cheating Measures

1. **Two-Container Architecture**: Application container (modifiable by candidates) and testing container (protected and immutable).
2. **Automated Execution**: Candidates run simple commands that execute full test suites without exposing internal testing logic.

## Assessment Framework

### Evaluation Criteria
1. **Technical Correctness**: Proper implementation of optimization techniques
2. **Relative Performance Impact**: Meaningful improvement ratios that demonstrate understanding of optimization principles
3. **Query Plan Evidence**: Database execution plans showing efficient operations

This framework establishes the foundation for creating comprehensive systems that make abstract performance concepts tangible and measurable while providing consistent evaluation mechanisms across different environments and use cases.