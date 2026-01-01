# ai-assisted-Support-ticketing-system
🎫 AI-Assisted Ticket Processing System

A scalable, async, human-in-the-loop ticket processing system built with FastAPI, PostgreSQL, Redis, Celery, and AI services.

This project demonstrates clean system design, clear async boundaries, and enterprise-ready architecture suitable for banking and support workflows.

📌 Problem Statement

Customer support tickets often involve:

High latency operations (AI summarization, suggestions)

Unreliable external services

Strict audit and consistency requirements

The goal is to:

Keep user-facing APIs fast

Isolate heavy AI processing

Ensure human control over decisions

Maintain strong auditability

🏗️ High-Level Architecture
Core Design Principles

Synchronous for users, asynchronous for heavy work

PostgreSQL as the single source of truth

AI as advisory, never authoritative

Clear component boundaries

Architecture Style

Layered architecture

Event-driven async processing

Human-in-the-loop AI system

🧱 Components & Responsibilities
1️⃣ FastAPI (API Layer)

Responsibilities

Request validation

Transaction management

Trigger async jobs

Does NOT

Call AI directly

Run long-running logic

2️⃣ PostgreSQL (Database)

Responsibilities

Store tickets

Store AI results

Maintain audit history

Why PostgreSQL?

ACID guarantees

Strong consistency

Enterprise-grade reliability

Nothing is considered valid unless it is persisted in Postgres.

3️⃣ Redis (Message Broker)

Responsibilities

Queue async jobs

Decouple API from workers

Why Redis?

Fast

Lightweight

Simple to operate locally and in interviews

4️⃣ Celery Worker (Async Processing)

Responsibilities

Process background jobs

Handle retries

Call AI services

Update ticket state

Why workers?

Failure isolation

Horizontal scalability

No impact on API latency

5️⃣ AI Service

Responsibilities

Generate ticket summaries

Provide resolution suggestions

Explicit limitations

❌ No state changes

❌ No decisions

AI output is treated as data, not truth.

6️⃣ React UI (Human Review)

Responsibilities

Display tickets

Show AI suggestions

Allow human approval or modification
