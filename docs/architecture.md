# DecisionFlow Architecture

## Purpose
 Define structured evaluation rules.
 Accept structured submissions.
 Produce auditable decisions.
 Store results and reasoning.
 Reprocess data as rules evolve.

-> It will model systems such as:
 Risk engines, compliance checks, application screening, data quality pipelines



## Goals
 Deterministic evaluation service
 Clear API contracts
 Full audit trail
 Strong validation and error handling
 Integration & E2E testing
 Production-stlye deployment

-> Non-Goals
 UI (optional later)
 Machine Learning
 Real-time streaming



## System Flow
 1. Admin defines set of rules
 2. Client submits data in a structured format
 3. System validates received data
 4. Engine evaluates validated data
 5. Result logged as value and context
 6. Client receives decision
 7. Admin updates rules
 8. Past submissions may be reprocessed




## Core Entities
-> RuleSet
 -id
 -name
 -version
 -description
 -active
 -created_at

-> Rule
 -id
 -ruleset_id
 -field
 -operator(>, <, =, includes)
 -value
 -weight
 -failure_message

-> Submission
 -id
 -raw_payload(JSONB)
 -ruleset_version
 -status(Pending, Processed, Failed)
 -created_at

-> EvaluationResult
 -id
 -submission_id
 -decision(approved, review, rejected)
 -score
 -breakdown(JSONB)
 -processed_at

-> AuditLog
 -id
 -entity_type
 -entity_id
 -action
 -before
 -after
 -processed_at


## API Design 

-> Admin
 - POST /rulesets
 - POST /rules
 - GET /rulesets
 - POST /rulesets/:id/activate

-> Submissions
 - POST /submissions
 - GET /submissions/:id
 - POST /submissions/:id/reprocess

-> System
 - GET /health



## Evaluation Engine
 -Validates required fields
 -Applies rules in deterministic order
 -Calculates weighted score
 -Produces:
   -pass/fail per rule
   -final decision
   -explanation object

->Must handle:
 -missing data
 -malformed types
 -contradicting rules
 -division-by-zero type of errors
 -version mismatches



## Error Strategy
-> 3 Classes:
 1.ValidationError(400)
 2.BusinessRuleError(422)
 3.SystemError(500)
-> All Errors Return:
 -code
 -message
 -correlationID
 -details




## Testing Strategy
-> Unit:
 -rule evaluation
 -validators

-> Integration:
 -API
 -DB
 -reprocessing flows
 -failure scenarios

-> E2E
 -admin defines rules
 -user submits data
 -system returns evaluation result




## Observability
 -structured logging
 -health endpoints
 -request IDs
 -Rule execution traces
 -Audit logs




## Security
 -API key
 -Role separation (admin, user)
 -Payload size limits
 -Input sanitization
 -Migration safety




## Deployment
 -Dockerized API
 -Postgres container
 -AWS ECS
 -Terraform baseline
 -Environment configs