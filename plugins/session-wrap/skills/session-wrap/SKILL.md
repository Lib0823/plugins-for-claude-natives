---
name: Session Wrap Best Practices
description: This skill should be used when the user asks about "session wrap-up", "wrap best practices", "multi-agent orchestration", "2-phase pipeline", "session end workflow", or wants guidance on structuring end-of-session analysis workflows.
version: 1.0.0
---

# Session Wrap Best Practices

Guidance for effective session wrap-up workflows and multi-agent orchestration patterns.

## Overview

Session wrap-up is the process of analyzing completed work, documenting learnings, identifying automation opportunities, and planning follow-up tasks. This skill covers both manual best practices and the multi-agent orchestration approach.

## Why Session Wrap Matters

1. **Knowledge Preservation**: Capture learnings before context is lost
2. **Documentation Debt Prevention**: Update docs while context is fresh
3. **Automation Discovery**: Identify repetitive patterns worth automating
4. **Continuity**: Create clear handoff points for future sessions
5. **Quality Improvement**: Reflect on what worked and what didn't

## Manual Session Wrap Checklist

Before ending a session, consider:

### Documentation
- [ ] Update CLAUDE.md with new commands, skills, or workflows
- [ ] Update context.md with project-specific learnings
- [ ] Add comments for non-obvious code
- [ ] Document any decisions made

### Code Quality
- [ ] Remove debug code and console.logs
- [ ] Check for TODO/FIXME comments
- [ ] Ensure error handling is in place
- [ ] Verify tests pass

### Follow-up Planning
- [ ] Note incomplete work
- [ ] Identify blockers
- [ ] List next logical steps
- [ ] Estimate remaining effort

### Commit Hygiene
- [ ] Stage relevant changes
- [ ] Write descriptive commit message
- [ ] Don't commit sensitive files

## 2-Phase Pipeline Architecture

For comprehensive analysis, use the multi-agent approach with 2 phases.

### Design Principles

Based on [Anthropic Multi-Agent Research](https://www.anthropic.com/engineering/multi-agent-research-system):

- **Phase 1**: Independent analysis → Parallel execution (latency optimization)
- **Phase 2**: Dependent validation → Sequential execution (coherence guarantee)

### Phase 1: Analysis Agents (Parallel)

Four agents run simultaneously, each with independent focus:

| Agent | Focus | Output |
|-------|-------|--------|
| **doc-updater** | Documentation gaps | Specific content to add |
| **automation-scout** | Repetitive patterns | skill/command/agent proposals |
| **learning-extractor** | New knowledge, mistakes | TIL-format learnings |
| **followup-suggester** | Incomplete work, next steps | Prioritized task list |

**Why parallel?** These agents don't share state or depend on each other's output.

### Phase 2: Validation Agent (Sequential)

One agent validates Phase 1 results:

| Agent | Focus | Output |
|-------|-------|--------|
| **duplicate-checker** | Phase 1 proposal validation | Approved/Merge/Skip for each |

**Why sequential?** Needs Phase 1 results as input. Validates before action.

### Pipeline Diagram

```
Phase 1 (Parallel)
┌──────────────┬──────────────┬──────────────┬──────────────┐
│ doc-updater  │ automation-  │ learning-    │ followup-    │
│              │ scout        │ extractor    │ suggester    │
└──────┬───────┴──────┬───────┴──────┬───────┴──────┬───────┘
       │              │              │              │
       └──────────────┴──────────────┴──────────────┘
                            │
                            ▼
Phase 2 (Sequential)
┌─────────────────────────────────────────────────────────────┐
│                    duplicate-checker                         │
│              (validates doc-updater & automation-scout)      │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
                    User Selection
                            │
                            ▼
                   Execute Actions
```

## When to Use /wrap

**Use the command:**
- End of significant work session
- Before switching to different project
- After completing a feature or fixing a bug
- When unsure what to document

**Skip the command when:**
- Very short session with trivial changes
- Only reading/exploring code
- Quick one-off question answered

## Output Integration

After running /wrap, integrate results:

### For Documentation Updates
1. Review doc-updater proposals
2. Check duplicate-checker validation
3. Apply approved updates
4. Merge partial duplicates as suggested

### For Automation
1. Review automation-scout proposals
2. Use `/plugin-dev:create-plugin` for complex automations
3. Create simple commands/agents directly

### For Learnings
1. Extract key insights from learning-extractor
2. Consider adding to team knowledge base
3. Share notable discoveries with team

### For Follow-ups
1. Review followup-suggester priorities
2. Create issues/tickets for P0/P1 items
3. Note Quick Wins for next session start

## Additional Resources

### Reference Files

For detailed patterns and techniques, consult:

- **`references/multi-agent-patterns.md`** - Comprehensive multi-agent orchestration patterns

### Related Commands

- `/wrap` - Run the full session wrap-up workflow
- `/wrap [message]` - Quick commit with provided message

### Related Agents

- `doc-updater` - Documentation analysis
- `automation-scout` - Automation detection
- `learning-extractor` - Learning capture
- `followup-suggester` - Task prioritization
- `duplicate-checker` - Validation
