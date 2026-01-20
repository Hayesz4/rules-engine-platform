# DecisionFlow

DecisionFlow is a rules-driven evaluation service designed to demonstrate AI-orchestrated backend engineering. The project emphasizes system architecture, specification-driven development, and rigorous validation of AI-generated code to production standards.

Rather than focusing on manual implementation alone, this project showcases how AI agents can be directed to design, implement, test, and document a real backend service under human technical leadership.

## Purpose
DecisionFlow allows organizations to define structured evaluation rules and process structured submissions into auditable decisions. It models real-world systems such as risk engines, compliance pipelines, and internal decision services.

## Core Goals
- Architecture-first system design
- Clear AI-consumable specifications
- Deterministic evaluation engine
- Strong validation and error handling
- Integration and E2E testing
- Production-style service structure and deployment

## Tech Stack (Planned)
- TypeScript + Node (NestJS)
- PostgreSQL
- Prisma or TypeORM
- Jest or Vitest, Supertest, Playwright
- Docker, AWS ECS, Terraform

## Development Approach
This project is built using an AI-orchestration workflow:

1. System architecture and API contracts are written first.
2. Formal specifications are created for AI agents (backend, testing, documentation).
3. AI tools (e.g., Cursor, Claude, ChatGPT) generate implementations.
4. All outputs are reviewed, tested, and iterated against explicit quality criteria.
5. Failures, edge cases, and refinements are documented.

The focus is on instruction quality, architectural clarity, and validation rigor.

## Repository Structure
/docs — architecture, system design, and decision records  
/specs — formal AI agent specifications and requirements  
/prompts — agent prompts and iteration history  
/src — application source code  
/tests — automated tests and validation suites  
/docker — containerization and environments  
/terraform — infrastructure and deployment  

## Roadmap
- Phase 1: Architecture and system design
- Phase 2: AI agent specifications
- Phase 3: Orchestrated implementation
- Phase 4: Validation, testing, and hardening
- Phase 5: Cloud deployment and production review
