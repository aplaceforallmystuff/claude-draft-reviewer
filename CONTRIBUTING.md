# Contributing to Claude Draft Reviewer

Thanks for your interest in improving the draft-reviewer agent!

## Ways to Contribute

### Improve the Workflow

The 3-phase workflow can be refined:

- Better sequencing of checks
- More effective fix prioritization
- Improved handling of edge cases

### Expand Fix Categories

Help categorize more fix types:

- New patterns to detect
- Better automatic fixes
- Clearer decision criteria

### Enhance Skill Integration

Improve how skills work together:

- Better handoff between skills
- Shared context preservation
- Combined output formatting

### Add Output Examples

Real-world examples are valuable:

- Before/after comparisons
- Different content types
- Various voice profiles

## Submitting Changes

1. Fork the repository
2. Create a feature branch (`git checkout -b improve-workflow`)
3. Make your changes to `agents/draft-reviewer.md`
4. Test with various content types
5. Submit a pull request

## Guidelines

### Keep It Actionable

The agent emphasizes fixing over reporting:

- Every issue should have a concrete fix
- Fixes should be applied, not suggested
- Vague advice like "consider improving" is not acceptable

### Maintain the FIXER Philosophy

The agent is an editor, not a critic:

- Find issues → Fix them → Report what changed
- Don't produce reports for someone else to implement
- Show before/after for every change

### Respect Skill Boundaries

Each skill has its role:

- `slop-detector` - AI pattern detection
- `craft-rules` - Writing mechanics
- `voice-editor` - Voice consistency

Don't duplicate functionality across skills.

## Questions?

Open an issue for discussion before major changes.
