# GitHub Project Integration Guide

Automatically add Issues to Project on creation for centralized progress management.

---

## Quick Setup

### 1. Create GitHub Project

1. GitHub → Projects → New project
2. Select **Board** template
3. Create the following columns:
   - 📋 **Backlog** - Not started
   - 🔍 **Planning** - AI designing
   - 🛠️ **In Progress** - Implementation
   - 👀 **Review** - Pending verification
   - ✅ **Done** - Completed

### 2. Get Project URL

Copy the Project page URL:
```
https://github.com/users/YOUR_USERNAME/projects/1
```

### 3. Create Personal Access Token (PAT)

1. GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens
2. **Generate new token**
3. Permissions:
   - **Repository access**: Select target repositories
   - **Permissions**:
     - Issues: Read and write
     - Pull requests: Read and write
     - Projects: Read and write
4. Copy the token

### 4. Add Repository Settings

**Settings → Secrets and variables → Actions**

**Secrets:**
| Name | Value |
|------|-------|
| `ADD_TO_PROJECT_PAT` | Created PAT |

**Variables:**
| Name | Value |
|------|-------|
| `PROJECT_URL` | Project URL |

---

## Usage

### Automatic Integration

| Trigger | Action |
|---------|--------|
| Issue created | Auto-add to Project |
| Label added to Issue | Update status |
| PR created | Auto-add to Project |
| PR merged | Add `done` label to Issue |

### Label to Status Mapping

| Label | Project Status |
|-------|----------------|
| `planning` | Planning |
| `in-progress` | In Progress |
| `ready-for-review` | Review |
| `done` | Done |

---

## Workflow Integration

```
/plan
  ↓ Issue created → Auto-add to Project (Backlog)
  ↓ Label: planning → Move to Planning column

/start
  ↓ Label: in-progress → Move to In Progress column

/finish
  ↓ PR created → Auto-add to Project
  ↓ Label: ready-for-review → Move to Review column

/verify (PASS)
  ↓ PR merged → Label: done → Move to Done column
```

---

## Project View Usage

### Kanban View
- Drag & drop to change status
- Filter by assignee

### Table View
- Add custom fields (priority, estimates, etc.)
- Sort/group

### Timeline View
- Sprint planning
- Deadline management

---

## Notes

- Check PAT expiration (90 days, etc.)
- Project can be public or private
- Multiple repositories can be managed in one Project
