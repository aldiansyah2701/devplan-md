# Smart AI Sprint Planner - Development Plan

# Project Overview

Smart AI Sprint Planner adalah platform AI yang membantu software engineering team mengubah requirement document menjadi sprint planning yang dapat dieksekusi.

Platform dapat:

* Menganalisa FSD, BRD, SRS, User Story
* Menghasilkan backend task
* Menghasilkan frontend task
* Menghasilkan QA task
* Menghasilkan story point estimation
* Menghasilkan dependency mapping
* Menyediakan chatbot berbasis RAG terhadap dokumen

---

# Product Vision

Mengurangi waktu sprint planning.

Mengurangi effort manual dalam membaca requirement.

Menyediakan AI-powered project planning assistant.

Menyediakan knowledge base berbasis AI.

---

# Target Users

## Engineering Manager

* Sprint planning
* Capacity planning
* Dependency management

## Product Manager

* Requirement validation
* Scope clarification

## Backend Engineer

* Backend task generation

## Frontend Engineer

* UI task generation

## QA Engineer

* Test case generation

---

# Core Features

## Authentication

* Register
* Login
* Refresh Token
* Logout
* JWT Authentication
* RBAC

---

## Document Upload

Supported Files:

* PDF
* DOCX
* TXT

Original file tidak disimpan.

File diproses sementara dalam memory.

Setelah diproses, hanya metadata, chunks dan embeddings yang disimpan.

---

## Smart Sprint Planning

Input:

Requirement Document

Output:

* Backend Tasks
* Frontend Tasks
* QA Tasks
* Story Point Estimation
* Complexity Analysis
* Dependency Mapping
* Suggested Sprint Plan

---

## AI Chatbot

User dapat bertanya terhadap dokumen:

Contoh:

* Apa requirement login?
* Endpoint apa yang dibutuhkan?
* Apa acceptance criteria?
* Apa dependency task ini?

Jawaban berasal dari RAG context.

---

# High Level Architecture

Frontend (React)

↓

Fastify API

↓

PostgreSQL

↓

Redis

↓

BullMQ

↓

Worker

↓

OpenAI

↓

pgvector

---

# Tech Stack

## Frontend

React

TypeScript

Vite

TailwindCSS

TanStack Query

React Router

Zustand

Shadcn UI

---

## Backend

Node.js

TypeScript

Fastify

Prisma

PostgreSQL

Redis

BullMQ

LangChain JS

OpenAI API

Swagger

JWT

Zod

Docker

---

## Infrastructure

Docker Compose

GitHub Actions

Nginx

Redis

PostgreSQL

Worker Service

Backend Service

Frontend Service

---

# AI Agent Architecture

## Agent 1

Sprint Breakdown Agent

Responsibilities:

* Analyze requirements
* Detect features
* Generate engineering tasks
* Generate acceptance criteria
* Generate dependencies
* Generate story points

Output:

Backend Tasks

Frontend Tasks

QA Tasks

Story Points

Dependencies

---

## Agent 2

RAG Retrieval Agent

Responsibilities:

* Retrieve document context
* Answer questions
* Minimize hallucination

Workflow:

Question

↓

Embedding

↓

Similarity Search

↓

Retrieve Chunks

↓

Context Building

↓

OpenAI Completion

↓

Answer

---

## Agent 3

Estimation Agent

Responsibilities:

* Complexity analysis
* Sprint estimation
* Risk assessment

Output:

Story Point

Risk Level

Recommended Sprint

---

## Agent 4

Dependency Agent

Responsibilities:

* Detect task relationships
* Build dependency graph

Output:

Task A depends on Task B

Task B depends on Task C

---

# Database Design

## users

id

email

password

role

created_at

updated_at

---

## refresh_tokens

id

user_id

token

expired_at

created_at

---

## documents

id

filename

file_type

status

uploaded_by

created_at

updated_at

---

## document_chunks

id

document_id

chunk_index

content

embedding

created_at

---

## processing_jobs

id

document_id

status

started_at

finished_at

error_message

created_at

---

## sprint_tasks

id

document_id

title

description

task_type

story_point

priority

status

created_at

updated_at

---

## task_dependencies

id

task_id

depends_on_task_id

---

## chat_sessions

id

user_id

title

created_at

---

## chat_messages

id

session_id

role

content

created_at

---

# Backend Modules

## Auth Module

Responsibilities:

* Register
* Login
* Refresh Token
* Logout
* RBAC

---

## User Module

Responsibilities:

* User Profile
* User Management

---

## Document Module

Responsibilities:

* Upload
* Validation
* Metadata Management

---

## Processing Module

Responsibilities:

* Queue orchestration
* Background processing

---

## Embedding Module

Responsibilities:

* Chunking
* Embedding generation
* Vector storage

---

## Sprint Module

Responsibilities:

* Task generation
* Story point estimation
* Dependency generation

---

## Chat Module

Responsibilities:

* Chat sessions
* Chat history
* Retrieval

---

# API Contract

## Authentication

POST /auth/register

POST /auth/login

POST /auth/refresh

POST /auth/logout

GET /auth/me

---

## Documents

POST /documents/upload

GET /documents

GET /documents/{id}

GET /documents/{id}/status

---

## Sprint Planning

POST /sprint/generate

GET /sprint/{documentId}

GET /sprint/{documentId}/tasks

---

## Chat

POST /chat/message

GET /chat/sessions

GET /chat/{sessionId}

---

# Upload Processing Flow

User Upload

↓

Fastify API

↓

Create Job

↓

BullMQ

↓

Worker

↓

Extract Text

↓

Chunking

↓

Embedding Generation

↓

Store Vector

↓

Update Status

↓

Completed

---

# Chat Flow

User Question

↓

Generate Query Embedding

↓

Vector Search

↓

Retrieve Chunks

↓

Build Context

↓

OpenAI

↓

Response

---

# Sprint Planning Flow

Requirement Document

↓

AI Analysis

↓

Feature Detection

↓

Task Generation

↓

Dependency Analysis

↓

Story Point Estimation

↓

Persist Tasks

↓

Frontend Display

---

# Folder Structure

backend/

src/

plugins/

modules/

auth/

users/

documents/

processing/

embeddings/

sprint/

chat/

workers/

middlewares/

types/

utils/

prisma/

tests/

---

frontend/

src/

pages/

components/

hooks/

stores/

services/

types/

---

docs/

devplan.md

---

# Security Requirements

JWT Authentication

Refresh Token Rotation

RBAC

Password Hashing (bcrypt)

Rate Limiting

Input Validation (Zod)

Secure Headers

Audit Logging

---

# Development Roadmap

## Phase 1

Foundation

* Fastify
* Prisma
* PostgreSQL
* Redis
* Docker
* Swagger
* JWT
* RBAC

Status: In Progress

---

## Phase 2

Document Upload

* Upload API
* Validation
* Queue
* Worker

---

## Phase 3

Embedding Pipeline

* Chunking
* Embedding
* pgvector
* Similarity Search

---

## Phase 4

Sprint Planning Agent

* Requirement Analysis
* Task Generation
* Estimation

---

## Phase 5

Chatbot

* RAG
* Session Management
* Context Retrieval

---

## Phase 6

Production Readiness

* Testing
* Monitoring
* Logging
* CI/CD
* Deployment

---

# Definition Of Done

* Dockerized
* Swagger documented
* Authentication complete
* Queue processing working
* Embedding generation working
* Vector search working
* Sprint generation working
* Chatbot working
* CI/CD pipeline working
* Production deployable

---

# Coding Standards

Use TypeScript strict mode.

Use Prisma ORM for standard CRUD.

Use Raw SQL only for advanced vector search.

Use Service Layer pattern.

Never place business logic in controllers.

Use dependency injection where appropriate.

Write unit tests.

Write integration tests.

Document all APIs using Swagger.

Use OpenAPI-first mindset.

Keep modules isolated and maintainable.
