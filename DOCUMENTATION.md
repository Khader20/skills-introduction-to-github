# GitHub Skills: Introduction to GitHub - Complete Documentation

## Table of Contents

1. [Overview](#overview)
2. [Repository Structure](#repository-structure)
3. [Tutorial System Architecture](#tutorial-system-architecture)
4. [Step-by-Step Learning Guide](#step-by-step-learning-guide)
5. [GitHub Actions Workflows](#github-actions-workflows)
6. [Usage Instructions](#usage-instructions)
7. [API Reference](#api-reference)
8. [Troubleshooting](#troubleshooting)
9. [Contributing](#contributing)

---

## Overview

The **Introduction to GitHub** repository is an interactive educational platform designed to teach new users the fundamental concepts and workflows of GitHub. This self-paced tutorial uses automated GitHub Actions to provide real-time feedback and guidance as learners progress through each step.

### Learning Objectives

By completing this tutorial, users will understand:
- What GitHub is and its role in software development
- Repository structure and version control concepts
- How to create and manage branches
- The commit process and best practices
- Pull request workflow and collaboration
- How to merge changes and contribute to projects

### Key Features

- **Interactive Learning**: Automated feedback through GitHub Actions
- **Self-Paced**: Complete at your own speed with pause/resume capability
- **Hands-On Experience**: Real GitHub operations, not simulations
- **Progressive Difficulty**: Builds knowledge step-by-step
- **Visual Guidance**: Screenshots and examples for each step

---

## Repository Structure

```
.
├── README.md                          # Main repository introduction
├── LICENSE                           # MIT License
├── .gitignore                        # Git ignore patterns
├── .github/
│   ├── steps/                        # Tutorial content
│   │   ├── 1-create-a-branch.md     # Step 1: Branch creation
│   │   ├── 2-commit-a-file.md       # Step 2: File commits
│   │   ├── 3-open-a-pull-request.md # Step 3: Pull requests
│   │   ├── 4-merge-your-pull-request.md # Step 4: Merging
│   │   └── x-review.md              # Final review and next steps
│   └── workflows/                    # Automation workflows
│       ├── 0-start-exercise.yml      # Initial setup
│       ├── 1-create-a-branch.yml    # Branch creation validation
│       ├── 2-commit-a-file.yml      # Commit validation
│       ├── 3-open-a-pull-request.yml # PR validation
│       └── 4-merge-your-pull-request.yml # Merge validation
```

---

## Tutorial System Architecture

### Core Components

#### 1. **Tutorial Steps (`/.github/steps/`)**
- **Purpose**: Contains markdown files with learning content
- **Format**: Structured lessons with activities and explanations
- **Features**: 
  - Concept explanations with external links
  - Step-by-step instructions
  - Visual aids (screenshots)
  - Troubleshooting sections

#### 2. **Automation Workflows (`/.github/workflows/`)**
- **Purpose**: Validates user progress and provides feedback
- **Technology**: GitHub Actions
- **Features**:
  - Automatic progress detection
  - Real-time feedback via issue comments
  - Sequential step enablement
  - Error handling and validation

#### 3. **Exercise Toolkit Integration**
- **Repository**: `skills/exercise-toolkit@v0.6.0`
- **Purpose**: Provides common functionality for GitHub Skills
- **Features**:
  - Issue management
  - Comment templates
  - Progress tracking
  - Workflow orchestration

---

## Step-by-Step Learning Guide

### Step 0: Exercise Initialization
**Trigger**: Repository creation/fork  
**Objective**: Set up the learning environment

**What Happens**:
- Creates an exercise tracking issue
- Posts welcome message and first step content
- Enables Step 1 workflow

**Key Concepts**: Repository setup, issue tracking

---

### Step 1: Create a Branch
**File**: `.github/steps/1-create-a-branch.md`  
**Trigger**: Push to `my-first-branch`  
**Objective**: Learn branch creation and management

**Key Concepts**:
- **Repository**: A project containing files and folders with version tracking
- **Branch**: A parallel version of your repository for safe development
- **Main Branch**: The definitive/production branch

**Activity**:
```bash
# User creates branch via GitHub UI:
# 1. Navigate to Code tab
# 2. Click main branch dropdown
# 3. Enter "my-first-branch"
# 4. Click "Create branch: my-first-branch from main"
```

**Learning Outcomes**:
- Understanding of version control concepts
- Practical branch creation experience
- Safety of parallel development

---

### Step 2: Commit a File
**File**: `.github/steps/2-commit-a-file.md`  
**Trigger**: Commit to `my-first-branch` with `PROFILE.md`  
**Objective**: Learn the commit process

**Key Concepts**:
- **Commit**: A set of changes to files and folders in your project
- **Commit Message**: Description of changes for collaboration clarity
- **File Creation**: Adding new content to the repository

**Activity**:
```markdown
# User creates PROFILE.md with content:
Welcome to my GitHub profile!
```

**Required Elements**:
- File must be named exactly `PROFILE.md`
- Must be in repository root directory
- Must be committed to `my-first-branch`
- Commit message should be `Add PROFILE.md`

**Learning Outcomes**:
- Hands-on file creation experience
- Understanding commit workflow
- Importance of descriptive commit messages

---

### Step 3: Open a Pull Request
**File**: `.github/steps/3-open-a-pull-request.md`  
**Trigger**: Pull request opened from `my-first-branch` to `main`  
**Objective**: Learn collaboration through pull requests

**Key Concepts**:
- **Pull Request**: Proposal to merge branch changes into main
- **Code Review**: Process of examining changes before integration
- **Collaboration**: Working together on shared projects

**Activity**:
```
# User creates PR via GitHub UI:
# 1. Navigate to Pull requests tab
# 2. Click "New pull request"  
# 3. Select my-first-branch as source
# 4. Title: "Add my first file"
# 5. Add description
# 6. Click "Create pull request"
```

**Learning Outcomes**:
- Understanding collaboration workflow
- Pull request creation process
- Code review concepts

---

### Step 4: Merge Your Pull Request
**File**: `.github/steps/4-merge-your-pull-request.md`  
**Trigger**: Pull request merged  
**Objective**: Complete the development cycle

**Key Concepts**:
- **Merge**: Integrating branch changes into main branch
- **Development Cycle**: Complete flow from branch to production
- **Integration**: Combining separate work streams

**Activity**:
```
# User merges PR:
# 1. Review the pull request
# 2. Click "Merge pull request"
# 3. Confirm merge
# 4. Delete feature branch (optional)
```

**Learning Outcomes**:
- Completing full GitHub workflow
- Understanding integration process
- Best practices for branch management

---

### Step 5: Review and Next Steps
**File**: `.github/steps/x-review.md`  
**Trigger**: Automatic after Step 4 completion  
**Objective**: Consolidate learning and provide advancement paths

**Content**:
- **Accomplishment Summary**: Review of completed tasks
- **Profile README Guide**: Creating a personal GitHub profile
- **Advanced Resources**: Student Developer Pack, additional skills
- **Community Engagement**: Discussion boards and exploration

---

## GitHub Actions Workflows

### Workflow Architecture

Each workflow follows a consistent pattern:

1. **Trigger Detection**: Specific GitHub events (push, PR creation, etc.)
2. **Progress Validation**: Verify user completed required tasks
3. **Feedback Delivery**: Post results via issue comments
4. **State Management**: Enable next workflow, disable current one

### Common Workflow Components

#### Jobs Structure
```yaml
jobs:
  find_exercise:
    # Locates the tracking issue for this exercise
    uses: skills/exercise-toolkit/.github/workflows/find-exercise-issue.yml@v0.6.0
  
  check_step_work:
    # Validates user's progress against step requirements
    needs: find_exercise
    
  post_next_step_content:
    # Delivers next lesson content and updates state
    needs: [find_exercise, check_step_work]
```

#### Key Features
- **Error Handling**: Graceful failure with helpful feedback
- **Validation Logic**: Specific checks for each step's requirements
- **State Management**: Automatic progression control
- **Template System**: Consistent messaging via exercise-toolkit

---

### Workflow Reference

#### `0-start-exercise.yml`
**Purpose**: Initialize the tutorial experience  
**Trigger**: `push` to `main` branch  
**Actions**:
- Creates exercise tracking issue
- Posts welcome content
- Enables Step 1 workflow

**Environment Variables**:
- `STEP_1_FILE`: Path to first tutorial step

**Permissions Required**:
```yaml
permissions:
  contents: write    # Update README
  actions: write     # Manage workflows
  issues: write      # Create and comment on issues
```

---

#### `1-create-a-branch.yml`
**Purpose**: Validate branch creation  
**Trigger**: `push` to `my-first-branch`  
**Validation**: Confirms branch name matches exactly

**Key Validation Logic**:
```yaml
on:
  push:
    branches:
      - "my-first-branch"  # Exact match required
```

---

#### `2-commit-a-file.yml`
**Purpose**: Validate file commit  
**Trigger**: Commit with `PROFILE.md` file  
**Validation**: 
- File exists in repository root
- User is on `my-first-branch`
- File contains expected content

---

#### `3-open-a-pull-request.yml`
**Purpose**: Validate pull request creation  
**Trigger**: Pull request opened against `main`  
**Validation**:
- PR source is `my-first-branch`
- PR target is `main` branch
- PR is in open state

---

#### `4-merge-your-pull-request.yml`
**Purpose**: Validate merge completion  
**Trigger**: Pull request closed with merge  
**Actions**:
- Confirms successful merge
- Posts completion celebration
- Provides next steps and resources

---

## Usage Instructions

### For Learners

#### Getting Started
1. **Fork Repository**: Create your own copy of this repository
2. **Navigate to Issues**: Find the automatically created exercise issue
3. **Follow Instructions**: Complete each step as guided in issue comments
4. **Watch for Feedback**: Automated responses provide real-time validation

#### Best Practices
- **Read Carefully**: Each step builds on previous knowledge
- **Use Exact Names**: Automation requires precise naming (e.g., `my-first-branch`)
- **Check Issue Comments**: All feedback and instructions appear there
- **Take Your Time**: This is self-paced learning

#### Troubleshooting Steps
1. **Verify Names**: Ensure exact spelling of branches, files, etc.
2. **Check Location**: Files must be in correct directories
3. **Review Comments**: Look for specific error messages in issues
4. **Refresh Pages**: Sometimes GitHub UI needs a refresh

---

### For Instructors/Administrators

#### Customization Options
- **Step Content**: Modify `.github/steps/*.md` files for custom lessons
- **Validation Logic**: Adjust workflow triggers and validation rules
- **Branding**: Update references and images for institutional use
- **Prerequisites**: Add setup requirements or knowledge checks

#### Deployment Considerations
- **Permissions**: Ensure proper GitHub permissions for automation
- **Dependencies**: Monitor exercise-toolkit version compatibility
- **Scale**: Consider rate limits for large classroom deployments

---

## API Reference

### Exercise Toolkit Integration

The repository integrates with `skills/exercise-toolkit@v0.6.0` for common functionality:

#### `find-exercise-issue.yml`
```yaml
uses: skills/exercise-toolkit/.github/workflows/find-exercise-issue.yml@v0.6.0
outputs:
  issue-url: URL of the exercise tracking issue
```

#### `start-exercise.yml`
```yaml
uses: skills/exercise-toolkit/.github/workflows/start-exercise.yml@v0.6.0
with:
  exercise-title: "Introduction to GitHub"
  intro-message: "Welcome message content"
```

#### Template Variables
```yaml
uses: skills/action-text-variables@v1
with:
  template-file: "path/to/template.md"
  template-vars: |
    next_step_number=2
    custom_variable=value
```

---

### GitHub CLI Commands

Workflows use GitHub CLI for issue management:

#### Comment Creation
```bash
gh issue comment "$ISSUE_URL" \
  --body-file "path/to/content.md"
```

#### Comment Updates
```bash
gh issue comment "$ISSUE_URL" \
  --body "Updated content" \
  --edit-last
```

#### Workflow Management
```bash
gh workflow enable "Step Name"
gh workflow disable "Step Name"
```

---

### Environment Variables

#### Standard Variables
- `GITHUB_TOKEN`: Automatic authentication token
- `ISSUE_URL`: URL of exercise tracking issue
- `STEP_X_FILE`: Path to step content files

#### Custom Configuration
```yaml
env:
  STEP_1_FILE: ".github/steps/1-create-a-branch.md"
  NEXT_STEP: "2"
  VALIDATION_REQUIRED: "true"
```

---

## Troubleshooting

### Common Issues

#### "No feedback received"
**Symptoms**: User completes step but sees no automation response  
**Causes**:
- Incorrect naming (branch, file, PR title)
- Wrong location (file not in root)
- Timing delays (GitHub Actions processing)

**Solutions**:
1. Verify exact naming requirements
2. Check file locations and content
3. Wait 1-2 minutes for processing
4. Check Actions tab for workflow status

#### "Workflow not triggering"
**Symptoms**: No workflow runs appear in Actions tab  
**Causes**:
- Trigger conditions not met
- Permissions issues
- Workflow disabled

**Solutions**:
1. Review trigger conditions in workflow files
2. Check repository permissions
3. Manually enable workflows if needed

#### "Step validation failing"
**Symptoms**: Workflow runs but reports validation errors  
**Causes**:
- Missing required elements
- Case sensitivity issues
- File content problems

**Solutions**:
1. Review step requirements carefully
2. Check exact spelling and capitalization
3. Verify file content matches expectations

---

### Advanced Troubleshooting

#### Workflow Debugging
1. **Check Actions Tab**: Review workflow run logs
2. **Examine Triggers**: Verify event matches workflow expectations
3. **Validate Permissions**: Ensure adequate repository permissions
4. **Review Dependencies**: Check exercise-toolkit version compatibility

#### Manual Recovery
If automation fails completely:
1. **Disable All Workflows**: Prevent conflicts
2. **Create Manual Issue**: Post step content manually
3. **Enable Target Workflow**: Jump to appropriate step
4. **Notify Learner**: Explain situation and next steps

---

## Contributing

### Development Setup
1. **Fork Repository**: Create development copy
2. **Create Feature Branch**: Use descriptive naming
3. **Test Changes**: Verify workflow functionality
4. **Submit Pull Request**: Include detailed description

### Testing Guidelines
- **Workflow Testing**: Use separate test repositories
- **Content Validation**: Ensure educational accuracy
- **Accessibility**: Verify screen reader compatibility
- **Browser Testing**: Check across different platforms

### Code Standards
- **YAML Formatting**: Consistent indentation and structure
- **Markdown Style**: Follow GitHub Flavored Markdown
- **Documentation**: Comment complex workflow logic
- **Error Handling**: Provide helpful error messages

---

## License

This project is licensed under the MIT License. See the [`LICENSE`](LICENSE) file for details.

**Copyright (c) GitHub, Inc.**

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

---

## Additional Resources

### GitHub Documentation
- [GitHub Skills](https://skills.github.com): More interactive learning
- [GitHub Docs](https://docs.github.com): Complete platform documentation
- [GitHub Education](https://education.github.com): Student and educator resources

### Related Learning Paths
- [Communicating using Markdown](https://github.com/skills/communicate-using-markdown)
- [GitHub Pages](https://github.com/skills/github-pages)
- [Hello GitHub Actions](https://github.com/skills/hello-github-actions)

### Community
- [GitHub Skills Discussions](https://github.com/orgs/skills/discussions)
- [GitHub Community](https://github.community)
- [GitHub Explore](https://github.com/explore)

---

*This documentation covers all public APIs, workflows, components, and usage instructions for the Introduction to GitHub Skills repository. For questions or contributions, please open an issue or discussion in the appropriate GitHub Skills community forum.*