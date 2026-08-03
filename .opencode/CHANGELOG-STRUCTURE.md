# CheatScale Structure Migration Changelog

## Version 2.0.0 - Feature > Task > Subtask

### Breaking Changes

#### Old Structure (Deprecated)
```
Phase > Day > Task
- Phase N — [Name]
  - Day M
    - [ ] Task checkbox
```

#### New Structure
```
Feature > Task > Subtask
- Feature: [name]
  - Task: [name]
    - [ ] Subtask checkbox
```

### Command Syntax Changes

| Command | Old Syntax | New Syntax | Status |
|---------|-----------|-----------|--------|
| `/routine` | `scope P1D1` | `scope login-flow` | Deprecated* |
| `/commit` | `[scope:P1D1]` | `[scope#login-flow]` | Deprecated* |
| `/push` | `scope P1D1` | `scope login-flow` | Deprecated* |
| `/sitrep` | P1D2 status | login-flow status | Updated |

*Backward compatible - old format still works with deprecation warning

### Files Modified

1. **[NEW]** `.opencode/templates/feature.md` - Feature template (renamed from roadmap.md)
2. **[NEW]** `.opencode/templates/task.md` - Task template with Obsidian frontmatter
3. **[NEW]** `.opencode/scripts/common.sh` - Dual format parser functions
4. **[UPDATE]** `.opencode/commands/bootstrap.md` - New roadmap structure
5. **[UPDATE]** `.opencode/commands/routine.md` - New task format
6. **[UPDATE]** `.opencode/commands/commit.md` - New tag format
7. **[UPDATE]** `.opencode/commands/push.md` - New search pattern
8. **[UPDATE]** `.opencode/commands/sitrep.md` - New status format
9. **[UPDATE]** `.opencode/commands/inject.md` - Updated surgical rules
10. **[UPDATE]** `.opencode/scripts/jira-sync/jira-sync.sh` - 1:1 JIRA mapping
11. **[UPDATE]** `.opencode/scripts/jira-sync/jira-pull.sh` - Feature > Task > Subtask output
12. **[UPDATE]** `.opencode/scripts/jira-sync/jira-push.sh` - Reads feature.md + tasks/*.md
13. **[UPDATE]** `.opencode/scripts/jira-sync/README.md` - Updated documentation
14. **[UPDATE]** `.opencode/instructions/INSTRUCTIONS.md` - plans/ and feature.md refs
15. **[UPDATE]** `.opencode/README.md` - New syntax examples
16. **[NEW]** `.opencode/MIGRATION-PLAN.md` - Migration guide

### Directory Structure Changes

**OLD:**
```
plans/scope/
├── roadmap.md        # Phase > Day > Task
├── days/
│   ├── day-1.md
│   └── day-2.md
└── ...
```

**NEW:**
```
plans/scope/
├── feature.md       # Feature > Task > Subtask
└── tasks/
    ├── login-flow.md
    └── password-reset.md

.opencode/templates/
├── feature.md       # Feature template
└── task.md          # Task template with Obsidian frontmatter
```

### JIRA Integration

| CheatScale | JIRA Space |
|----------|-----------|
| Feature | Epic |
| Task | Task |
| Subtask | Subtask |

**1:1 Mapping** - No complex translation required.

### Migration Status

- [x] Templates created
- [x] Parser functions created (dual format)
- [x] Bootstrap command updated
- [x] Routine command updated
- [x] Commit command updated
- [x] Push command updated
- [x] SitRep command updated
- [x] Inject command updated
- [x] Execute command updated
- [x] Validate-roadmap command updated
- [x] Plan command updated
- [x] Debate command updated
- [x] JIRA sync updated
- [x] All command references scanned

### Backward Compatibility

Both formats are supported:
- `/routine auth P1D1` - Works (deprecated, shows warning)
- `/routine auth login-flow` - New recommended format

The dual parser in `scripts/common.sh` automatically detects format.