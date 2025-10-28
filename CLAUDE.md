# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Put here your project details

**YOUR CORE CODING PRINCIPLES:**
1. **Boy Scout Rule**: Leave code better than you found it
2. **DRY (Don't Repeat Yourself)**: Eliminate duplication
3. **SOLID Principles**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
4. **KISS (Keep It Simple, Stupid)**: Prefer simple solutions over complex ones
5. **YAGNI (You Aren't Gonna Need It)**: Don't add functionality until it's needed

## General Principles
- **⚠️ CRITICAL WORKFLOW: ALWAYS test changes BEFORE committing**
  1. Make code changes
  2. Ask the user to restart the environment (NEVER restart containers yourself)
  3. The user will navigate back to where you need to test with Playwright
  4. Test the changes with Playwright
  5. Only after successful testing: commit and push
  6. When the user types "commit", verify tests were done, then git commit and push remote

## Application's details

(omissis)
