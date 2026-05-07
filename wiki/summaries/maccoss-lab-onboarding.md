---
title: "Onboarding Claude Code Like a New Developer: MacCoss Lab Lessons"
type: summary
tags: [case-study, claude-code, legacy-codebase, onboarding, context-management, open-source]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Onboarding Claude Code like a new developer Lessons from 17 years of development.md"]
confidence: high
---

## Key Points

### Project Context
- **Software**: Skyline, open-source protein analysis tool for biomarker discovery and drug development
- **Scale**: 700,000+ lines of C#, 17 years of active development since 2008
- **Team**: Small team at University of Washington MacCoss Lab, maintained by principal developer Brendan MacLean
- **Testing**: 200,000+ automated nightly tests
- **Challenge**: Decades of knowledge, frequent developer turnover (undergrads, grad students, postdocs)

### The Insight
Applied same methodology for onboarding human developers to onboarding Claude Code: "Explain enough to achieve a successful limited project and produce improved context for the next iteration"

### Architecture: Separate Repository for AI Context
- **pwiz-ai repository**: All AI context kept separate from codebase, applies across all branches and time points
- **CLAUDE.md at root**: Environment setup, points to documentation ("lay of the land")
- **Skills**: Expertise lives in skills (open format for agent capabilities), not CLAUDE.md
- **Example**: `debugging` skill pulls Claude out of "guess and test" mode toward root cause analysis
- **Skill triggers**: Can be manual or automatic with explicit conditions

### Key Principle: Context is an Artifact
"Context is just another artifact to maintain and grow" - treat it like code, version it, update it deliberately

### Practical Results
1. **Finished abandoned work**: Completed year-long Files View panel project in 2 weeks (previous efforts typically discarded)
2. **Revived stalled features**: Added features to 3-year-dormant nightly test management module in under a day
3. **New infrastructure**: Automated screenshot reproduction (2,000+ tutorial images), diff-only views, pixel change amplification
4. **MCP servers**: Custom C# and Python MCP servers for test infrastructure integration
5. **Daily automation**: Morning summary emails of test failures, exceptions, open support threads
6. **Team adoption**: Developers now barely write code themselves, primarily instruct Claude Code
7. **New features**: Skeptical developer shipped mobilogram pane (ion mobility visualization) and credited Claude Code

### Three-Part Advice for Legacy Codebases

**1. Context is Your Best Friend**
- Plans don't persist, context does
- Invest in building and maintaining context layer
- Version it, grow it, maintain it like any artifact
- Keep in separate repo (applies to all branches/time points)
- Memory that names specific functions/files can go stale - verify before recommending

**2. Invest in Building Skill Library**
- Use skills to encode domain knowledge
- "Reference do not embed" principle - skills point to central documentation
- Key skills: `skyline-development` (project orientation), `version-control` (conventions), `debugging` (root cause analysis)
- Skills persist across project lifetime, available to every contributor

**3. Use MCP Integrations for Data Access**
- Build MCP integrations where Claude needs real data (test results, exception reports, support threads)
- For open source: context layer is itself an artifact that persists beyond any one contributor
- Example: Daily summaries from nightly test infrastructure, GitHub, LabKey Server

### Technical Details
- **Context location**: github.com/ProteoWizard/pwiz-ai (separate from codebase)
- **Connection**: Dario Amodei (Anthropic co-founder) was previously MacCoss Lab member
- **Open source benefit**: Context persists as project artifact beyond human institutional memory

## Relevant Concepts

- [[concepts/context-as-artifact]] - Treating context like versioned code
- [[concepts/onboarding-methodology]] - Systematic approach to teaching codebase
- [[concepts/skill-libraries]] - Encoding domain expertise
- [[concepts/legacy-codebase-management]] - Working with 17-year-old code
- [[concepts/separate-context-repository]] - Versioning AI context separately
- [[concepts/reference-not-embed]] - Pointing to documentation vs copying
- [[concepts/mcp-servers]] - Custom integrations for data access
- [[concepts/institutional-memory]] - Preserving knowledge beyond individuals

## Relevant Entities

- [[entities/brendan-maclean]] - Principal developer, Claude Developer Ambassador
- [[entities/maccoss-lab]] - University of Washington research lab
- [[entities/skyline]] - Protein analysis software
- [[entities/pwiz-ai]] - AI context repository
- [[entities/labkey-server]] - Scientific data web portal
- [[entities/dario-amodei]] - Anthropic co-founder, former MacCoss Lab member

## Source Metadata

- **Type**: Case study / best practices guide
- **Publisher**: Anthropic (Claude.com blog)
- **Published**: 2001-04-28 (likely 2026-04-28)
- **URL**: https://claude.com/blog/onboarding-claude-code-like-a-new-developer-lessons-from-17-years-of-development
- **Program**: Claude for Open Source program
- **Role**: Brendan MacLean is Claude Developer Ambassador
