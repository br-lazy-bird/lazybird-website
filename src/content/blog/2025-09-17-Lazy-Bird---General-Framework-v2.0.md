---
title: "General Framework v2.0"
date:  2025-09-17 17:31:11
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

### Repository Structure Framework (Technical Domain Organization)

**Repository Name**: `lazy-bird`

```
lazy-bird/
├── README.md
├── database/
│   ├── 01-employee-directory/
│   │   ├── README.md
│   │   ├── DETONADO.md
│   │   ├── docker-compose.yml
│   │   ├── backend/
│   │   │   ├── Dockerfile
│   │   │   ├── requirements.txt
│   │   │   └── app/
│   │   ├── frontend/
│   │   │   ├── Dockerfile
│   │   │   ├── package.json
│   │   │   └── src/
│   │   └── database/
│   │       └── init/
│   ├── 02-sales-reports/
│   └── README.md
├── apis/
│   ├── 01-product-catalog/
│   └── README.md
├── caching/
├── events/
├── concurrency/
├── architecture/
├── security/
├── monitoring/
└── docs/
    ├── contributing.md
    └── technical-domains.md
```

### Structure Benefits

- **Technical Domain Organization**: Systems grouped by the specific technical skills they teach (database optimization, API performance, caching strategies, etc.)
- **Spoiler-Free Naming**: Folder names don't reveal the specific problem, preserving the learning experience
- **Scalable Architecture**: Easy to add new domains and systems as the project grows
- **Self-Contained Systems**: Each broken system includes everything needed for setup and learning
- **Clear Learning Paths**: Candidates can focus on mastering specific technical domains

## Problem Documentation & Solution Management

### DETONADO Standard Guide

Each broken system includes a standardized **DETONADO.md** guide following this format:

1. **🎯 Learning Objective** - What specific concept this system teaches
2. **🔍 Problem Identification** - How to recognize the issue
3. **🛠️ Diagnosis Tools** - Commands/techniques to analyze the problem
4. **🧠 Root Cause Analysis** - Understanding why the problem exists
5. **⚡ Solution Implementation** - Step-by-step fix instructions
6. **✅ Verification** - How to confirm the fix worked
7. **📊 Expected Results** - Specific performance improvements
8. **🚨 Troubleshooting** - Common issues and solutions

### Solution Management Strategy: Documentation-Only Approach

**Single Branch Philosophy**:
- **Main Branch Only**: Contains the broken system that candidates receive
- **No Solution Code**: Candidates must implement fixes themselves using DETONADO guide
- **Authentic Learning**: Forces genuine understanding rather than copying pre-written solutions
- **Realistic Workflow**: Mirrors real-world problem-solving where you don't have a "solution branch" to reference

**Why This Approach**:
- **Educational Value**: Candidates get satisfaction of actually solving the problem
- **Prevents Shortcuts**: No way to simply switch to a working version
- **Builds Confidence**: Success comes from genuine understanding and implementation
- **Transferable Skills**: Teaches actual debugging and optimization processes

## Cross-Environment Consistency

### Containerized Testing Strategy

- **Docker Compose Setup**: One-command startup with `docker-compose up`
- **Standardized Environment**: Consistent execution regardless of host machine
- **Relative Performance Metrics**: Focus on improvement ratios rather than absolute timing
- **Query Plan Analysis**: Hardware-independent validation of optimization approaches
- **Reproducible Results**: Same experience for all candidates

### Validation Framework

- **Candidate-Run Tests**: Simple validation tests that candidates execute themselves
- **Performance Benchmarks**: Clear before/after metrics to measure improvements
- **Technical Verification**: Automated checks for proper implementation (e.g., index existence)
- **Self-Service Validation**: Candidates can verify their solutions independently

## Assessment Framework

### Evaluation Criteria

1. **Technical Correctness**: Proper implementation of optimization techniques
2. **Performance Impact**: Meaningful improvement in system performance
3. **Understanding Demonstration**: Evidence that candidate understands the root cause and solution
4. **Process Following**: Adherence to proper diagnostic and validation procedures

### Learning Objectives

**Technical Skills**:
- Domain-specific optimization techniques (database indexing, API parallelization, caching strategies, etc.)
- Performance analysis and diagnostic tools usage
- System architecture understanding

**Problem-Solving Process**:
- Systematic problem identification
- Root cause analysis methodology
- Solution validation and verification
- Performance measurement and interpretation

## Key Changes from Original Framework (v1.0)

### 1. Branch Strategy Simplification
**Original**: Two-branch approach (main + solution branch)
**Updated**: Single branch, documentation-only solution
**Reason**: Eliminates temptation to peek at solutions; forces authentic learning

### 2. Repository Organization Evolution  
**Original**: Individual `broken-system-exercise/` folders
**Updated**: Technical domain-based structure (`database/01-employee-directory/`)
**Reason**: Better skill-based organization; prevents naming spoilers; scalable growth

### 3. Project Structure Streamlining
**Original**: Complex structure with separate docker folder and protected testing infrastructure
**Updated**: Self-contained systems with integrated Docker setup
**Reason**: Simpler setup; easier maintenance; focus on educational value over complex infrastructure

### 4. Solution Management Philosophy
**Original**: Automated testing system switching between branches
**Updated**: Candidate-driven validation with self-service testing
**Reason**: More realistic learning experience; builds debugging skills; reduces infrastructure complexity

### 5. Anti-Cheating Approach
**Original**: Two-container architecture with immutable testing containers
**Updated**: Focus on educational design over technical prevention
**Reason**: Trust-based learning environment; reduced complexity; emphasis on genuine skill development

## Implementation Benefits

This updated framework provides:

- **Focused Learning**: Clear technical domain organization helps candidates build specific skills
- **Authentic Experience**: Documentation-only solutions mirror real-world problem-solving
- **Scalable Growth**: Easy to add new domains and complexity levels
- **Maintainable Codebase**: Simplified structure reduces maintenance overhead
- **Educational Priority**: Design decisions favor learning effectiveness over technical complexity

The framework establishes a sustainable foundation for creating comprehensive systems that make abstract performance concepts tangible and measurable while prioritizing genuine learning over assessment gaming.
