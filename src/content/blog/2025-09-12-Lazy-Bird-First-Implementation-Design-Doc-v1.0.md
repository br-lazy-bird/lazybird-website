---
title: "First Broken System"
date:  2025-09-12 18:04:15
categories: ["Lazy Bird Project"]
tags: []
---

# User Directory - Design Document v1.0

## Domain Description

Employee directory system demonstrating database indexing optimization through a relatable, intuitive interface that users expect to be fast. This serves as the foundational broken system in the Lazy Bird Project repository.

## The Specific Problem

- **Issue**: Employee name search query performs table scans instead of using indexes
- **Solution**: Add indexes on first_name and last_name columns
- **Expected Outcome**: Search queries change from table scans to index seeks, dramatically improving performance

## Problem Focus

**Single Issue: Missing Database Indexes**

This system demonstrates one specific performance problem: missing indexes on searchable database columns. The broken system contains:
- **One Primary Query**: Employee search by name that performs poorly
- **Single Root Cause**: Missing indexes on name fields (first_name, last_name)
- **Single Solution**: Add appropriate indexes to optimize the search query

**Why This Approach**:
- **Focused Learning**: Developers learn one concept thoroughly rather than multiple concepts superficially
- **Clear Cause-Effect**: Direct relationship between missing indexes and poor performance
- **Simple Verification**: Easy to test and validate the single optimization
- **Reduced Complexity**: No confusion about which optimization to implement first

## Problem Demonstration Strategy

1. **Broken State Delivery**: System delivered with poor search performance
2. **User Empathy**: Realistic employee directory scenario everyone understands
3. **Obvious Performance Issues**: Painfully slow search experience that clearly needs optimization
4. **Visual Impact**: Loading states, progress indicators, and timing displays emphasize the problem

## System Features

### Core Functionality
- **Single Search Feature**: Search employees by name (first_name, last_name)
- **Large Dataset**: Substantial employee records to make the missing index problem obvious
- **Simple Interface**: Minimal UI focused on demonstrating the search performance issue
- **Realistic Data**: Employee records with names, departments, and basic information

### Performance Visibility Features
- **Query Timer**: Display exact execution time for the search operation
- **Loading States**: Visual feedback during slow search operations
- **Query Analysis Tools**: Built-in tools to examine the problematic query execution plan

## Success Metrics

- **Relative Performance Improvement**: Meaningful improvement in search query execution time
- **Query Plan Verification**: Automated detection that search queries now use index seeks instead of table scans
- **Index Existence Check**: Verification that proper indexes exist on first_name and last_name columns
- **Single Query Focus**: All testing centers around the one optimized search operation

## Learning Objectives

**Technical Skills**:
- Understanding database index impact on query performance
- Reading and interpreting database query execution plans
- Implementing basic database indexes

**Problem-Solving Process**:
- Identifying performance bottlenecks in a single, specific query
- Applying targeted optimization to resolve the identified issue
- Verifying that the optimization actually solved the problem

## Domain-Specific Considerations

**Realistic Scenarios**: Employee directory represents a common business application that candidates can immediately understand and relate to.

**Scalability Demonstration**: Large datasets show how performance problems compound with scale, making optimization necessity clear.

**User Experience Impact**: Direct connection between database performance and user frustration, making abstract concepts concrete.

**Business Context**: Optimization has clear business value (employee productivity, system usability), connecting technical improvements to real-world impact.

## Technology Stack

**Backend**: Python with FastAPI
- Async support for clear performance differentiation
- SQLAlchemy for database operations and query plan analysis
- Built-in instrumentation for performance measurement

**Frontend**: React with TypeScript
- Type safety to prevent interface breaking during optimization
- Real-time performance metrics display
- Visual feedback components (loading states, timing displays)

**Database**: PostgreSQL
- Rich query execution plan analysis (EXPLAIN ANALYZE)
- Comprehensive metadata for programmatic index verification
- Industry-standard enterprise database

**Stack Rationale**: This combination provides clear performance visibility across all layers while using familiar, industry-standard technologies that translate directly to real-world optimization scenarios.

This implementation serves as the template and proof-of-concept for the Lazy Bird Project approach, establishing patterns and techniques that will be applied to future broken systems focusing on different single issues.