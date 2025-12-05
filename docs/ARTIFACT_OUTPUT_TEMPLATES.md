# Artifact Output Templates for Browser/Mobile LLMs

**Version:** 1.0  
**Purpose:** Standard format for AI agents to output governance files as downloadable artifacts in browser/mobile LLM sessions (ChatGPT, Claude, Gemini, etc.)

---

## Overview

When working with browser-based or mobile LLM interfaces, AI agents cannot directly write to the file system. Instead, they must output governance files in a downloadable format.

This document defines three methods for artifact output, in order of preference:

1. **Claude Artifacts** (Best UX) - Actual downloadable files with one-click download
2. **ChatGPT Python Script** (Recommended) - Zip file with all governance files
3. **Copy/Paste Fallback** (Universal) - Text in code blocks for manual saving

---

## Method 1: Claude Artifacts (Preferred)

### When to Use
- User is on Claude.ai or Claude mobile app
- Claude supports artifact creation

### How It Works
- Generate each governance file as a separate artifact
- Claude provides "Download" button for each artifact
- User downloads actual `.md` files with one click
- Best user experience, no copy/paste needed

### Implementation
```
Create artifact: AI_CONTEXT_INDEX.md
[Complete file content]

Create artifact: TODO.md
[Complete file content]

Create artifact: SESSION_NOTES.md
[Complete file content]

✅ Download each artifact using the download button
Commit all files to your repository
Next session: Upload all 4 files to continue
```

---

## Method 2: ChatGPT Python Script (Recommended)

### When to Use
- User is on ChatGPT with Code Interpreter enabled
- Want single-download experience (zip file)

### How It Works
- Generate Python script that creates `governance_files.zip`
- Script packages all 3 files into one downloadable archive
- User clicks download button in ChatGPT
- Extract zip to project root

### Implementation Template

````python
import zipfile
from io import BytesIO

# Governance file contents
files = {
    'AI_CONTEXT_INDEX.md': """# AI Context Index

**Purpose:** Central map of project structure and state for AI agents and engineers.

## 1. Project Overview

**Name:** [Your Project Name]
**Description:** [Brief description]
**Status:** Bootstrap

## 2. Documentation

- `AI_RULES_AND_BEST_PRACTICES.md` - Governance framework
- `TODO.md` - Task registry
- `SESSION_NOTES.md` - Work log
- `SESSION_BUFFER.md` - Working memory (active sessions only)

[... complete content ...]
""",
    
    'TODO.md': """# Project TODO

This file tracks tasks for engineers and AI agents.

## Conventions

- Use checkboxes: `- [ ]` for open, `- [x]` for done.

[... complete content ...]
""",
    
    'SESSION_NOTES.md': """# Session Notes

## [2025-12-05] Session 1 - Project Bootstrap

- Agent: ChatGPT
- Goal: Initialize governance framework

[... complete content ...]
""",
    
    'SESSION_BUFFER.md': """# Session Buffer - 2025-12-05

## Working Notes

[Active session working notes go here]

## Decisions to Commit

[Final decisions to move to SESSION_NOTES.md]

## Questions / Uncertainties

[Items requiring engineer input]

## Experiments

[Trial approaches and test results]
"""
}

# Create zip file
zip_buffer = BytesIO()
with zipfile.ZipFile(zip_buffer, 'w', zipfile.ZIP_DEFLATED) as zip_file:
    for filename, content in files.items():
        zip_file.writestr(filename, content)

# Write to downloadable file
with open('governance_files.zip', 'wb') as f:
    f.write(zip_buffer.getvalue())

print("✅ governance_files.zip created!")
print("📥 Click the download button below to save")
print("")
print("📦 Contains:")
for filename in files.keys():
    print(f"  - {filename}")
print("")
print("🚀 Next steps:")
print("  1. Download governance_files.zip")
print("  2. Extract files to your project root")
print("  3. Commit to repository:")
print("     git add AI_CONTEXT_INDEX.md TODO.md SESSION_NOTES.md SESSION_BUFFER.md")
print("     git commit -m '[AI] Initialize governance framework'")
print("     git push")
print("")
print("  4. Next session: Upload all governance files:")
print("     - AI_RULES_AND_BEST_PRACTICES.md")
print("     - AI_CONTEXT_INDEX.md")
print("     - TODO.md")
print("     - SESSION_NOTES.md")
print("     - SESSION_BUFFER.md (if continuing same session)")
````

### User Experience
1. ChatGPT executes Python script
2. Download button appears for `governance_files.zip`
3. User clicks download
4. Extract zip to project root
5. Commit files
6. Done!

---

## Method 3: Copy/Paste Fallback (Universal)

### 1. Clear File Headers

Each file MUST be preceded by a clear header that:
- Uses an emoji indicator (📋 for documents, ✅ for success, ⚠️ for warnings)
- States the filename explicitly
- Provides actionable instructions

**Example:**
```
📋 FILE: SESSION_NOTES.md
↓ Download this file and commit it to your repository
```

### 2. Complete File Contents

Output the **entire file contents** in a code block with:
- Proper markdown formatting
- Filename in code fence (if supported by LLM)
- No truncation or "..." ellipsis

**Example:**
````markdown
```markdown filename="SESSION_NOTES.md"
# Session Notes

## [2025-12-05] Session 1 - Project Bootstrap

- Agent: ChatGPT
- Goal: Initialize governance framework
...
```
````

### 3. Download Checklist

After outputting all files, provide a checklist for the user:

```
✅ DOWNLOAD CHECKLIST

Please download and save these files to your repository:

- [ ] SESSION_NOTES.md
- [ ] TODO.md
- [ ] AI_CONTEXT_INDEX.md
- [ ] [Any other modified files]

Then commit them:
```bash
git add SESSION_NOTES.md TODO.md AI_CONTEXT_INDEX.md
git commit -m "[AI] Updated governance files - Session YYYY-MM-DD"
git push
```

📌 IMPORTANT: In your next session, upload ALL governance files so I can reconstruct project context.
```

---

## Template Examples

### Template A: First Session (Bootstrap)

Use this when generating files for the first time:

````markdown
# 🎉 Governance Files Generated!

I've created the required governance files for your project. Please download each file below and commit them to your repository.

---

## 📋 FILE: AI_CONTEXT_INDEX.md
↓ Download and save to project root

```markdown filename="AI_CONTEXT_INDEX.md"
# AI Context Index

**Purpose:** Central map of project structure and state for AI agents and engineers.

## 1. Project Overview

**Name:** [Your Project Name]
**Description:** [Brief description]
**Status:** Bootstrap

## 2. Documentation

- `AI_RULES_AND_BEST_PRACTICES.md` - Governance framework
- `TODO.md` - Task registry
- `SESSION_NOTES.md` - Work log

## 3. Directory Structure

- `/src` - Source code
- `/docs` - Documentation
- `/tests` - Test suite

## 4. Active Tasks

[To be populated from TODO.md]

## 5. Security and Compliance

[Define any security requirements or compliance needs]

## 6. Key Contacts

- Engineer: [Your name]
```

---

## 📋 FILE: TODO.md
↓ Download and save to project root

```markdown filename="TODO.md"
# Project TODO

This file tracks tasks for engineers and AI agents.

## Conventions

- Use checkboxes: `- [ ]` for open, `- [x]` for done.
- Include a short description and optional owner or priority.

## Backlog

### Initial Setup
- [x] Generate governance files
- [ ] Define project requirements
- [ ] Create initial project structure

## In Progress

### [Current date] - Bootstrap Tasks
- [ ] Review and customize governance rules
- [ ] Add project-specific tasks

## Done

- [x] Initialize governance framework
```

---

## 📋 FILE: SESSION_NOTES.md
↓ Download and save to project root

```markdown filename="SESSION_NOTES.md"
# Session Notes

## [2025-12-05] Session 1 - Project Bootstrap

- Agent: ChatGPT
- Goal: Initialize AI governance framework
- Summary:
  - Generated initial governance files (AI_CONTEXT_INDEX.md, TODO.md, SESSION_NOTES.md)
  - Reviewed AI_RULES_AND_BEST_PRACTICES.md
  - Established project context
- Risk classification: 🟢 LOW (initial file generation)
- Next steps:
  - User to download and commit governance files
  - Define project requirements
  - Begin feature development
```

---

## ✅ DOWNLOAD CHECKLIST

Please complete these steps:

1. Download these files:
   - [ ] AI_CONTEXT_INDEX.md
   - [ ] TODO.md
   - [ ] SESSION_NOTES.md

2. Save them to your project root directory

3. Commit to your repository:
   ```bash
   git add AI_CONTEXT_INDEX.md TODO.md SESSION_NOTES.md
   git commit -m "[AI] Initialize governance framework"
   git push
   ```

4. **For your next session:** Upload ALL 4 files to continue:
   - AI_RULES_AND_BEST_PRACTICES.md
   - AI_CONTEXT_INDEX.md
   - TODO.md
   - SESSION_NOTES.md

This allows me to reconstruct full project context and continue where we left off! 🚀
````

---

### Template B: Subsequent Session (Updates)

Use this when updating existing files:

````markdown
# 📝 Session Complete - Governance Files Updated

I've updated the governance files based on today's work. Please download the updated versions and commit them.

---

## 📋 FILE: SESSION_NOTES.md (UPDATED)
↓ Download and replace in your repository

```markdown filename="SESSION_NOTES.md"
# Session Notes

[Previous entries...]

---

## [2025-12-05] Session 2 - Feature Development

- Agent: ChatGPT
- Goal: Implement user authentication
- Summary:
  - Created auth/login.py and auth/register.py
  - Added unit tests for authentication flow
  - Updated API documentation
- Files modified:
  - src/auth/login.py (NEW)
  - src/auth/register.py (NEW)
  - tests/test_auth.py (NEW)
  - docs/API.md (UPDATED)
- Risk classification: 🔴 HIGH (authentication logic)
- Uncertainty:
  - Password hashing algorithm choice (bcrypt vs argon2)
  - Session timeout duration (30 min vs 1 hour)
- Next steps:
  - Engineer to review authentication implementation
  - Decide on password hashing algorithm
  - Configure session timeout in production
```

---

## 📋 FILE: TODO.md (UPDATED)
↓ Download and replace in your repository

```markdown filename="TODO.md"
# Project TODO

## In Progress

### Authentication Implementation
- [x] Create login endpoint
- [x] Create registration endpoint
- [x] Add authentication tests
- [ ] Engineer review (HIGH PRIORITY)
- [ ] Choose password hashing algorithm
- [ ] Configure production session timeout

## Done

- [x] Initialize governance framework
- [x] Implement basic auth flow
```

---

## 📋 FILE: AI_CONTEXT_INDEX.md (UPDATED)
↓ Download and replace in your repository

```markdown filename="AI_CONTEXT_INDEX.md"
# AI Context Index

[Previous content...]

## 2. Documentation

- `AI_RULES_AND_BEST_PRACTICES.md` - Governance framework
- `TODO.md` - Task registry
- `SESSION_NOTES.md` - Work log
- `docs/API.md` - API documentation (UPDATED 2025-12-05)

## 3. Directory Structure

- `/src` - Source code
  - `/auth` - Authentication module (NEW)
    - `login.py` - Login endpoint
    - `register.py` - Registration endpoint
- `/tests` - Test suite
  - `test_auth.py` - Authentication tests (NEW)
```

---

## ✅ DOWNLOAD CHECKLIST

1. Download updated files:
   - [ ] SESSION_NOTES.md
   - [ ] TODO.md
   - [ ] AI_CONTEXT_INDEX.md

2. Replace existing files in your repository

3. Commit changes:
   ```bash
   git add SESSION_NOTES.md TODO.md AI_CONTEXT_INDEX.md
   git commit -m "[AI] Session 2: Authentication implementation"
   git push
   ```

4. **Next session:** Upload all governance files to continue!

---

## ⚠️ IMPORTANT NOTES

- I flagged authentication implementation as 🔴 HIGH RISK
- Please review `src/auth/login.py` and `src/auth/register.py`
- Two decisions needed:
  1. Password hashing: bcrypt vs argon2?
  2. Session timeout: 30 min vs 1 hour?
````

---

### Template C: Code Files as Artifacts

When outputting new code files:

````markdown
## 💻 FILE: src/auth/login.py (NEW)
↓ Download and save to src/auth/login.py

```python filename="src/auth/login.py"
"""
Authentication login endpoint.

Risk Level: HIGH (authentication logic)
Last Modified: 2025-12-05 by ChatGPT
"""

from flask import request, jsonify
import bcrypt

def login():
    """Handle user login."""
    data = request.get_json()
    
    # Validate input
    if not data or 'email' not in data or 'password' not in data:
        return jsonify({'error': 'Email and password required'}), 400
    
    # TODO: Query database for user
    # TODO: Verify password hash
    # TODO: Create session token
    
    return jsonify({'message': 'Login successful'}), 200
```

---

## 💻 FILE: tests/test_auth.py (NEW)
↓ Download and save to tests/test_auth.py

```python filename="tests/test_auth.py"
"""
Authentication tests.

Last Modified: 2025-12-05 by ChatGPT
"""

import pytest
from src.auth.login import login

def test_login_success():
    """Test successful login."""
    # TODO: Implement test
    pass

def test_login_missing_email():
    """Test login with missing email."""
    # TODO: Implement test
    pass

def test_login_invalid_credentials():
    """Test login with invalid credentials."""
    # TODO: Implement test
    pass
```

---

## ✅ CODE FILES CHECKLIST

1. Download these new files:
   - [ ] src/auth/login.py
   - [ ] tests/test_auth.py

2. Create directories if needed:
   ```bash
   mkdir -p src/auth tests
   ```

3. Save files to correct locations

4. Run tests to verify:
   ```bash
   pytest tests/test_auth.py
   ```

5. Commit:
   ```bash
   git add src/auth/login.py tests/test_auth.py
   git commit -m "[AI] Add authentication login endpoint"
   git push
   ```
````

---

## Mobile Workflow Example

For mobile users, provide condensed instructions:

```markdown
📱 MOBILE USERS

Quick workflow:

1. **GitHub App:** View and download files
2. **ChatGPT/Claude App:** Upload files to chat
3. **Work on tasks:** AI outputs artifacts
4. **GitHub App:** Download artifacts, commit changes

Tip: Use GitHub Codespaces on mobile for direct file system access!
```

---

## Best Practices

### DO:
- ✅ Output complete file contents (no truncation)
- ✅ Use clear file headers with emojis
- ✅ Provide download checklists
- ✅ Include commit commands
- ✅ Remind users to upload files next session
- ✅ Flag high-risk changes prominently

### DON'T:
- ❌ Use "..." or "[previous content]" in actual output
- ❌ Assume files are auto-saved
- ❌ Skip the download checklist
- ❌ Forget to update AI_CONTEXT_INDEX.md when structure changes
- ❌ Output files without clear boundaries/headers

---

## Platform-Specific Notes

### ChatGPT
- Supports code interpreter with downloadable files
- Can output multiple files in one response
- Users can download as .txt or copy contents

### Claude
- Supports artifacts feature
- Can create downloadable files
- Good for markdown rendering

### Gemini
- Supports file generation
- Can output code blocks
- Users copy contents manually

### Mobile Apps
- Most support file uploads
- May need to copy/paste from code blocks
- GitHub mobile app essential for commits

---

## Version History

- **v1.0** (2025-12-05): Initial template creation
  - Added first session bootstrap template
  - Added subsequent session update template
  - Added code file output template
  - Added mobile workflow guidance
