---
marp: true
theme: default
title: "Spec-Driven Development"
description: "From Simple Prompts to Spec-Driven Development"
---

# Spec-Driven Development

## From Simple Prompts to Specification-Driven Development

---

# The Problem with AI-Assisted Development

## Without structure, AI gives you:

- ❌ **Inconsistent results** — different output every run
- ❌ **Lost context** — starts fresh every session
- ❌ **No shared understanding** — each developer prompts differently
- ❌ **Hard to review** — no specification to validate against

## SDD makes specifications the source of truth.

---

# Today's Journey

1. **Simple Prompt**
2. **Prompt Engineering**
3. **Context Engineering**
4. **Plan Mode**
5. **Specification-Driven Development**
6. **Tools**

---

# Task: User Profile Component

**Requirements:**

- Display user information (name, email, avatar)
- Edit mode with form validation
- Save/cancel functionality
- Loading states
- Error handling

> We'll implement this same task using each approach — so you can compare directly.

---

# 1. Simple Prompt

## Prompt:

```text
Create a user profile component
```

## Benefits:

- ✅ Quick to write
- ✅ No preparation needed

## Negatives:

- ❌ Ambiguous - What should it display?
- ❌ Missing context - Which Angular version? Styling?
- ❌ No validation rules - Email format? Required fields?
- ❌ No error handling - What happens when API fails?
- ❌ Inconsistent results - Different AI responses each time

---

# 2. Prompt Engineering

## Prompt:

```markdown
Create a user profile component with:

- Display mode: Show user info (name, email, avatar URL)
- Edit mode: Form with validation (email required, name min 2 chars)
- Actions: Save, Cancel, Edit buttons
- States: Loading, Error, Success

## Context
- Angular 21 with standalone components
- HttpClient for API calls
- Reactive forms for form handling
- Project follows clean architecture

## Requirements
- Use reactive forms
- Implement proper TypeScript types
- Add accessibility attributes
- Include unit tests
- Follow Angular style guide
```

## Benefits over Simple Prompt:

- ✅ Specific - Clear technology stack
- ✅ Structured - Organized sections
- ✅ Complete - Covers all aspects
- ✅ Testable - Includes validation rules

## Negatives vs Context Engineering:

- ❌ AI doesn't know your project structure
- ❌ No existing code patterns
- ❌ No documentation context
- ❌ Manual context creation required

---

# 3. Context Engineering

## Prompt:

```markdown
Create user profile component following existing patterns with reactive forms, proper TypeScript types, accessibility attributes, unit tests, and Angular style guide compliance.

## Project Structure
src/
├── app/
│   ├── components/
│   │   ├── user-profile/
│   │   └── shared/
│   ├── services/
│   │   └── user.service.ts
│   ├── models/
│   │   └── user.model.ts
│   └── store/
│       └── user/

## Existing Code
// user.model.ts
export interface User {
  id: string;
  name: string;
  email: string;
  avatarUrl?: string;
  updatedAt: Date;
}

// user.service.ts
@Injectable({ providedIn: 'root' })
export class UserService {
  getUser(id: string): Observable<User> {
    return this.http.get<User>(`/api/users/${id}`);
  }
  updateUser(id: string, data: Partial<User>): Observable<User> {
    return this.http.patch<User>(`/api/users/${id}`, data);
  }
}
```

> 💻 **Demo**

## Benefits over Prompt Engineering:

- ✅ Consistent with existing patterns
- ✅ Reusable components and services
- ✅ Type-safe with existing models
- ✅ Testable following project conventions

## Negatives vs Plan Mode:

- ❌ No structured planning
- ❌ Limited architecture vision
- ❌ No dependency analysis
- ❌ Single-session focus
- ❌ No iterative refinement
- ❌ Manual context crafting

---

# 4. Plan Mode

## Prompt:

```markdown
Plan and implement a UserProfileComponent. Consider:

- Component architecture (display vs edit mode)
- Data flow from UserService to component
- State management (loading, editing, error states)
- Form validation (name min 2 chars, email required)
- Testing strategy

Angular 21 standalone app. Existing code:

// user.model.ts
export interface User {
  id: string;
  name: string;
  email: string;
  avatarUrl?: string;
  updatedAt: Date;
}

// user.service.ts
@Injectable({ providedIn: 'root' })
export class UserService {
  getUser(id: string): Observable<User> {
    return this.http.get<User>(`/api/users/${id}`);
  }
  updateUser(id: string, data: Partial<User>): Observable<User> {
    return this.http.patch<User>(`/api/users/${id}`, data);
  }
}
```

> 💻 **Demo**

## Benefits over Context Engineering:

- ✅ Clear architecture before coding
- ✅ Identify dependencies early
- ✅ Better estimation of effort
- ✅ Reduced rework during implementation

## Negatives vs SDD:

- ❌ Session-based planning
- ❌ Hard to share and refine
- ❌ No persistent workspace
- ❌ Lost after conversation ends
- ❌ Difficult to track changes over time

---

# 5. Spec-Driven Development

## Specification (`user-profile.spec.md`):

```markdown
# User Profile Component Specification

## Component: UserProfileComponent

### Purpose
Display and edit user profile information with proper validation and state management.

### Interface
interface UserProfileComponent {
  user: User | null;
  isLoading: boolean;
  error: string | null;
  isEditing: boolean;
  
  editUser(): void;
  saveUser(formData: UserProfileForm): void;
  cancelEdit(): void;
}

### Behavior Requirements

1. **Display Mode**
   - Shows user.name, user.email, user.avatarUrl
   - Edit button visible
   - Loading spinner during data fetch
   - Error message display

2. **Edit Mode**
   - Form with name (required, min 2 chars)
   - Form with email (required, valid email)
   - Avatar URL (optional, valid URL)
   - Save and Cancel buttons
   - Validation messages

3. **State Transitions**
   - Display → Edit: Click edit button
   - Edit → Display: Save successful or Cancel
   - Any state → Loading: During API calls
   - Any state → Error: API failures

### Test Cases
- Should display user information correctly
- Should validate form inputs
- Should handle API errors gracefully
- Should maintain state during transitions

## Task
Implement this specification exactly as written.
```

> 💻 **Demo**

## Benefits over Plan Mode:

- ✅ Clear, testable specifications
- ✅ Standardized behavior
- ✅ Comprehensive coverage
- ✅ Living documentation

## Negatives vs Tools:

- ❌ Manual specification writing
- ❌ No template generation
- ❌ No AI assistance
- ❌ No automation

---

# 6. Tools for SDD

## OpenSpec *(live demo)*

```yaml
# openspec.yaml
version: "1.0"
components:
  user-profile:
    type: "angular-component"
    specs:
      - "user-profile.spec.md"
      - "user-profile.test.ts"
```

- ✅ Standardized specification format
- ✅ Multi-language support
- ✅ CI/CD integration

**Slash commands:**

```
/opsx-propose   → create proposal + specs + design + tasks
/opsx-explore   → think through ideas before committing
/opsx-apply     → implement tasks from the current change
/opsx-archive   → archive completed change, update specs
```

**Achieving the UserProfile requirements with OpenSpec:**

```
1. /opsx-propose "add UserProfileComponent with display/edit modes,
   validation and state management"

   → AI generates: proposal.md, specs/, design.md, tasks.md

2. /opsx-apply

   → AI implements tasks from the generated specs

3. /opsx-archive

   → Change archived, specs kept as living documentation
```

- ✅ No manual spec writing
- ✅ AI-generated templates from a single prompt
- ✅ Structured, auditable artifacts per change

## Also worth knowing:

- **spec-kit** — Template-based spec generation (`npm install -g spec-kit`)
- **AWS AI-DLC** — AI-powered spec generation from natural language requirements

---

# Complete SDD Workflow

## Process:

1. **Requirements Gathering** - Business needs → User stories
2. **Specification Writing** - OpenSpec format → Detailed behavior
3. **AI-Assisted Generation** - AWS AI-DLC → Code scaffolding
4. **Implementation** - spec-kit → Component generation
5. **Testing** - Automated tests from specs
6. **Documentation** - Living docs with code

## Final Result:

```typescript
// Generated from specification
@Component({
  selector: 'app-user-profile',
  template: `
    @if (!isEditing) {
      <app-user-profile-display
        [user]="user"
        [isLoading]="isLoading"
        [error]="error"
        (edit)="editUser()" />
    } @else {
      <app-user-profile-edit
        [user]="user"
        (save)="saveUser($event)"
        (cancel)="cancelEdit()" />
    }
  `
})
export class UserProfileComponent implements OnInit {
  // Implementation follows specification exactly
}
```

---

# Key Takeaways

## From Simple Prompt to SDD:

🚀 **Start Simple** - Learn prompt engineering basics
🎯 **Add Context** - Give AI your project knowledge
📋 **Plan First** - Architecture before implementation
📝 **Specify Everything** - Clear, testable requirements
🛠️ **Use Tools** - spec-kit, openspec, AI-DLC

## Benefits Achieved:

✅ **Consistent code** across team members
✅ **Better quality** with comprehensive testing
✅ **Faster development** with automation
✅ **Living documentation** that stays current
✅ **Easier maintenance** with clear specifications

---

# Resources

- **OpenSpec** — Standardized specification format with CI/CD integration
- **spec-kit** — Template-based spec generation
- **AWS AI-DLC** — AI-powered spec generation from natural language requirements

---

# Thank You!

## Questions?
