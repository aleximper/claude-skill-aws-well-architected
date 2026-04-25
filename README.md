# Claude Code Skill — AWS Well-Architected Framework

Skill para [Claude Code](https://claude.com/claude-code) que le entrega a Claude una referencia completa y estructurada del **AWS Well-Architected Framework**: los 6 pilares, los design principles, el Shared Responsibility Model, el catálogo de lenses y el proceso de Well-Architected Review (WAR).

Úsalo cuando estés diseñando, revisando u optimizando cualquier workload en AWS.

## Qué contiene

```
aws-well-architected/
├── SKILL.md                                 Entry point ligero (índice + decision matrix)
└── references/
    ├── 01-design-principles.md              General Design Principles cross-pillar
    ├── 02-shared-responsibility.md          Shared Responsibility Model
    ├── 03-operational-excellence.md         Pilar OPS (OPS01–OPS11)
    ├── 04-security.md                       Pilar SEC (SEC01–SEC11)
    ├── 05-reliability.md                    Pilar REL (REL01–REL13) + RTO/RPO + estrategias DR
    ├── 06-performance-efficiency.md         Pilar PERF (PERF01–PERF05)
    ├── 07-cost-optimization.md              Pilar COST (COST01–COST11) + cheatsheet de pricing models
    ├── 08-sustainability.md                 Pilar SUS (SUS01–SUS06)
    ├── 09-lenses-catalog.md                 19 lenses oficiales de AWS (Serverless, SaaS, ML, GenAI, FSI…)
    └── 10-wa-tool-and-review.md             WA Tool + proceso WAR + refresh de Nov 2024
```

Cada archivo de pilar contiene la definición oficial de AWS, los design principles, las best practice areas con sus códigos de pregunta (ej. `OPS01..OPS11`, `SEC01..SEC11`, `REL01..REL13`), las best practices por pregunta, los servicios AWS clave, los anti-patterns más comunes, un review checklist de 12 a 15 ítems y URLs directas a la documentación oficial.

El contenido refleja el **refresh oficial del 6 de noviembre de 2024** (100% de OPS, SEC, PERF, COST, SUS y ~79% de REL actualizados).

> El contenido del skill está en inglés a propósito: coincide con la terminología canónica de AWS, mantiene la fidelidad de los nombres de los principios y BPs, y mejora el matching de keywords cuando Claude decide cargarlo.

## Instalación

### Global (recomendado)

Instálalo una sola vez y queda disponible en todas tus sesiones de Claude Code:

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  ~/.claude/skills/aws-well-architected
```

Para actualizarlo más adelante:

```bash
cd ~/.claude/skills/aws-well-architected && git pull
```

### Por proyecto

Si prefieres tenerlo solo en un repo específico:

```bash
git clone https://github.com/aleximper/claude-skill-aws-well-architected.git \
  .claude/skills/aws-well-architected
```

## Cómo se activa

Claude carga el skill automáticamente cuando la conversación involucra revisión de arquitectura AWS, Well-Architected Reviews, los seis pilares, AWS best practices, HRIs/MRIs o trade-offs de arquitectura en AWS. También puedes invocarlo de forma explícita con `/aws-well-architected` (según la versión de Claude Code).

`SKILL.md` es el entry point ligero que se carga al contexto. Funciona como índice de los archivos más profundos en `references/` — Claude lee solo lo relevante para mantener la ventana de contexto pequeña.

## Ejemplos de prompts que activan el skill

- "Revisa este stack de Terraform contra el AWS Well-Architected Framework."
- "Estoy diseñando un SaaS multi-tenant nuevo en AWS — ¿qué lenses debería aplicar y qué exige el pilar SEC?"
- "Guíame en un Well-Architected Review para un workload Lambda + DynamoDB."
- "¿Cuál es la diferencia entre Pilot Light y Warm Standby como estrategias de DR?"
- "Identifica HRIs en mi arquitectura actual EC2 + RDS desde la perspectiva del pilar Reliability."

## Fuentes y disclaimer

Todo el contenido se destila desde la documentación oficial de AWS. La fuente canónica y siempre actualizada sigue siendo la documentación de AWS:

- Framework: <https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html>
- Lens Catalog: <https://aws.amazon.com/architecture/well-architected/lenses/>
- WA Tool: <https://aws.amazon.com/well-architected-tool/>

Cada archivo en `references/` termina con una sección `## References` apuntando a las páginas oficiales que resume. Cuando tengas dudas, valida contra la documentación viva de AWS — el framework evoluciona continuamente.

Este proyecto **no está afiliado, respaldado ni patrocinado por Amazon Web Services**. AWS, el logo de Powered by AWS y todos los nombres de servicios de AWS son marcas registradas de Amazon.com, Inc. o sus afiliadas.

## Contribuciones

Issues y PRs son bienvenidos. Contribuciones especialmente útiles:

- Actualizaciones cuando AWS publica un refresh del framework
- Nuevos lenses agregados al AWS Lens Catalog
- Correcciones a IDs de BPs o URLs de documentación de AWS que hayan cambiado
- Traducciones a otros idiomas

## Licencia

[MIT](LICENSE) © 2026 Jhon Ortiz
