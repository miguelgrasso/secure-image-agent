# secure-image-agent

Agente construido con Strands Agents que empaqueta imágenes de contenedor desde repositorios con enfoque DevSecOps: análisis del repo, escaneo pre-build (secretos, SAST, SCA, lint), build aislado, SBOM, escaneo de CVEs, política como código (OPA), firma y publicación, con loop de remediación vía PR.

> Estado: estructura inicial (scaffolding). Los archivos contienen solo un `TODO`.

## Estructura

| Carpeta | Propósito |
|---|---|
| `src/secure_image_agent/agents/` | Nodos con LLM: analyzer, triage, remediator |
| `src/secure_image_agent/tools/` | Wrappers deterministas de CLIs de seguridad |
| `src/secure_image_agent/models/` | Contratos Pydantic (structured output) |
| `src/secure_image_agent/graph/` | Orquestación del grafo |
| `src/secure_image_agent/hooks/` | Auditoría, guardrails, human-in-the-loop |
| `src/secure_image_agent/skills/` | Buenas prácticas por stack |
| `policies/` | Política como código (Rego) + excepciones |
| `templates/` | Dockerfiles endurecidos por stack |
| `sandbox/` | Entorno aislado de build |
| `examples/vulnerable-app/` | Repo de prueba con fallas plantadas |
| `tests/`, `evals/` | Tests y evaluación del agente |
| `docs/` | Arquitectura, threat model, ADRs |

## Principio de diseño

El agente orquesta los controles, no los reemplaza: el pass/fail lo decide OPA, la firma la hace una tool con identidad propia y el LLM nunca ve llaves.
