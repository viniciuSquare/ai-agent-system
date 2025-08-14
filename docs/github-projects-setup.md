# GitHub Projects Setup Guide

This document provides step-by-step instructions for creating and configuring the GitHub Projects board for the AI Agent System development roadmap.

## Prerequisites

- GitHub account with appropriate permissions
- GitHub CLI installed (optional, for automation)
- Repository access to `viniciuSquare/ai-agent-system`

## Step 1: Create New GitHub Project

### Using GitHub Web Interface

1. Navigate to [GitHub Projects](https://github.com/users/viniciuSquare/projects)
2. Click "New project"
3. Select "Board" view
4. Configure the project:
   - **Name**: "AI Agent System - Development Roadmap"
   - **Description**: "Comprehensive project board for tracking AI Agent System development across all phases"
   - **Visibility**: Private or Public (as preferred)

### Using GitHub CLI (Alternative)

```bash
# First, ensure proper authentication scopes
gh auth refresh -s project,read:project

# Create the project
gh project create --owner viniciuSquare --title "AI Agent System - Development Roadmap"
```

## Step 2: Configure Project Board Columns

Create the following columns in order:

1. **📋 Backlog**
   - Description: "Issues ready for development planning"
   - Purpose: New issues and future work

2. **🚀 In Progress**
   - Description: "Issues currently being worked on"
   - Purpose: Active development work

3. **👀 Review**
   - Description: "Issues pending review or testing"
   - Purpose: Code review, testing, validation

4. **✅ Done**
   - Description: "Completed and verified issues"
   - Purpose: Finished work

## Step 3: Import All Repository Issues

### Automated Import (Recommended)

Use the following GitHub CLI commands to add all issues to the project:

```bash
# Get the project number from the created project
PROJECT_NUMBER=$(gh project list --owner viniciuSquare --format json | jq -r '.projects[] | select(.title=="AI Agent System - Development Roadmap") | .number')

# Add all issues to the project (issues #1-35)
for i in {1..35}; do
  gh project item-add $PROJECT_NUMBER --owner viniciuSquare --url https://github.com/viniciuSquare/ai-agent-system/issues/$i
  echo "Added issue #$i to project"
done
```

### Manual Import (Alternative)

1. Go to your project board
2. Click "+ Add item" in the Backlog column
3. Search for and select each issue (#1-#35)
4. Repeat for all 35 issues

## Step 4: Configure Custom Fields

Add the following custom fields to track progress:

### 4.1 Phase Field
- **Field Name**: "Phase"
- **Field Type**: Single select
- **Options**:
  - Phase 1: Knowledge Base Foundation
  - Phase 2: Requirements Analyzer Agent
  - Phase 3: Change Analyzer Agent
  - Phase 4: Refiner & Multi-Agent Integration
  - Phase 5: Advanced AI & Optimization
  - Infrastructure

### 4.2 Effort Field
- **Field Name**: "Effort"
- **Field Type**: Single select
- **Options**:
  - S (1-4 points)
  - M (5-8 points)
  - L (9-12 points)
  - XL (13+ points)

### 4.3 Priority Field
- **Field Name**: "Priority"
- **Field Type**: Single select
- **Options**:
  - High
  - Medium
  - Low

## Step 5: Add Dependency Links

GitHub Projects doesn't have native dependency support, but you can use:

1. **Issue References**: Use "Blocks" and "Depends on" in issue descriptions
2. **Linked Issues**: Link related issues using GitHub's linking feature
3. **Project Notes**: Add dependency information to project cards

### Key Dependencies to Track

Based on the dependency graph, these are critical relationships to monitor:

#### Phase 2 Dependencies
- #3 → #4, #5 (Input Schema blocks Validation and Storage)
- #4, #6, #8 → #9 (Multiple issues block Workflow Orchestration)
- #9 → #10 → #11 (Sequential completion required)

#### Phase 3 Dependencies
- #12, #13, #14 → #15 (Utilities block Classification)
- #15 → #16 → #17 (Sequential analysis chain)
- #17 → #18 → #19 (Analysis to Summary to Testing)

#### Phase 4 Dependencies
- #21 → #22, #23 (Message Schema blocks core components)
- #23 → #24 → #25 (Routing to Prompts to Synthesis)
- #25, #27 → #28 (Multiple inputs to final testing)

## Step 6: Set Up Project Views

Create additional views for different perspectives:

### 6.1 Phase View
- **View Type**: Board
- **Group by**: Phase field
- **Sort**: Priority, then Effort

### 6.2 Priority View
- **View Type**: Table
- **Group by**: Priority
- **Columns**: Title, Phase, Effort, Status, Assignee

### 6.3 Timeline View
- **View Type**: Roadmap
- **Group by**: Phase
- **Timeline**: Based on issue milestones

## Step 7: Configure Automation

Set up GitHub Project automation rules:

### 7.1 Auto-move Rules
- **When**: Issue is closed
- **Then**: Move to "Done" column

- **When**: Pull request is opened with "Closes #X"
- **Then**: Move issue #X to "In Progress"

- **When**: Pull request is merged
- **Then**: Move linked issue to "Done"

### 7.2 Status Sync
- **When**: Issue status changes
- **Then**: Update project status field

## Step 8: Populate Issue Details

For each imported issue, set the custom field values:

### Phase 2 Issues (#1, #3-11)
- **Phase**: "Phase 2: Requirements Analyzer Agent"
- **Effort**: Based on issue labels (S-3, M-5, L-8, etc.)
- **Priority**: Based on issue labels

### Phase 3 Issues (#12-20)
- **Phase**: "Phase 3: Change Analyzer Agent"
- **Effort**: Based on issue effort labels
- **Priority**: Based on issue priority labels

### Phase 4 Issues (#21-29)
- **Phase**: "Phase 4: Refiner & Multi-Agent Integration"
- **Effort**: Based on issue effort labels
- **Priority**: Based on issue priority labels

### Phase 5 Issues (#30-35)
- **Phase**: "Phase 5: Advanced AI & Optimization"
- **Effort**: Based on issue effort labels
- **Priority**: Based on issue priority labels

### Infrastructure (#2)
- **Phase**: "Infrastructure"
- **Effort**: Based on complexity
- **Priority**: High

## Project Board URL

Once created, the project will be available at:
`https://github.com/users/viniciuSquare/projects/[PROJECT_NUMBER]`

## Maintenance and Updates

1. **Daily**: Update issue status as work progresses
2. **Weekly**: Review dependency blocking and update priorities
3. **Monthly**: Review phase progress and adjust timeline
4. **Per Release**: Archive completed issues and plan next phase

## Troubleshooting

### Common Issues

1. **Permission Errors**: Ensure you have project creation permissions
2. **CLI Authentication**: Run `gh auth refresh -s project,read:project`
3. **Import Failures**: Check issue numbers and repository access
4. **Missing Fields**: Custom fields need to be created before bulk updates

### Support Commands

```bash
# Check authentication status
gh auth status

# List existing projects
gh project list --owner viniciuSquare

# View project details
gh project view PROJECT_NUMBER --owner viniciuSquare

# List project items
gh project item-list PROJECT_NUMBER --owner viniciuSquare
```

---

*This setup guide ensures comprehensive project tracking aligned with the dependency graph and development roadmap.*
