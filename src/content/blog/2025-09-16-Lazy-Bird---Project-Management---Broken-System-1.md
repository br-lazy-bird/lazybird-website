---
title: "Project Management - Broken System 1 - Employee Directory"
date:  2025-09-16 17:35:16
categories: ["Lazy Bird Project"]
tags: []
---

## 🎯 Project Planning Session Overview

We successfully planned the development of the **Lazy Bird Broken System 1: Employee Directory** - the first broken system in the educational project repository designed to teach database indexing optimization through hands-on experience.

## 📋 Key Decisions Made

### System Architecture
- **Backend**: FastAPI (Python) with SQLAlchemy ORM
- **Frontend**: React with TypeScript 
- **Database**: PostgreSQL
- **Deployment**: Docker Compose setup for easy one-command startup
- **Learning Focus**: Single performance issue - missing database indexes on search columns

### Learning Approach Strategy
- **Single Branch Strategy**: Only maintain the broken system (Documentation-Only Solution)
- **No Solution Code**: Candidates must diagnose and fix the problem themselves using standard database tools
- **Realistic Learning**: Forces genuine understanding rather than copying pre-written solutions

### Frontend Design Philosophy
- **Minimal UI**: Focused solely on showcasing backend performance issues
- **No Complex Dashboards**: Candidates use standard database tools (psql, pgAdmin) for query analysis
- **Core Components**: Search interface + performance timing display only

## 📝 DETONADO Standard Established

Created the standardized format for optimization guides across all future broken systems:

1. **🎯 Learning Objective** - What specific concept this system teaches
2. **🔍 Problem Identification** - How to recognize the issue
3. **🛠️ Diagnosis Tools** - Commands/techniques to analyze the problem
4. **🧠 Root Cause Analysis** - Understanding why the problem exists
5. **⚡ Solution Implementation** - Step-by-step fix instructions
6. **✅ Verification** - How to confirm the fix worked
7. **📊 Expected Results** - Specific performance improvements
8. **🚨 Troubleshooting** - Common issues and solutions

## 📋 Complete Development Backlog

Generated **13 GitHub Issues** organized across key development areas:

### Infrastructure & Setup (1 issue)
- Setup Docker Compose Environment

### Backend Development (5 issues)
- Create PostgreSQL Database Schema (intentionally missing indexes)
- Create Employee Data Seeding Script (10,000+ records)
- Implement FastAPI Backend Setup
- Create Employee Search Endpoint (the slow, problematic query)
- Add Query Performance Timing (to showcase the problem)

### Frontend Development (3 issues)
- Create React Frontend Setup
- Build Employee Search Interface
- Add Performance Timing Display

### Testing & Validation (2 issues)
- Create Solution Validation Tests
- Performance Baseline Tests

### Documentation (2 issues)
- Create Project README
- Create DETONADO Guide (following standardized template)