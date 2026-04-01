---
name: pdcpa
description: Execute the PDCPA cycle (Plan-Do-Check-Plan-Action) for AI agents. Use for task management and problem-solving. An enhanced PDCA cycle with a Re-Plan phase after Check, enabling more precise improvement actions through reflection and re-planning before Action. Use this skill whenever the user wants systematic task management, needs a problem-solving framework, or mentions PDCA/PDCPA.
---

# PDCPA Cycle

An enhanced PDCA cycle for AI agents. Traditional PDCA (Plan-Do-Check-Act) feeds Check results directly into Action, but AI agents produce more accurate improvements by pausing to re-plan. This is the core of PDCPA.

## Why PDCPA instead of PDCA

AI agents differ from humans in these ways:
- Can process large amounts of information at once, but lose focus as context grows
- Follow instructions faithfully, but can be weak at mid-course corrections
- Tend toward superficial fixes when Check results feed directly into Action

Inserting a second Plan after Check enables:
1. Organizing insights from Check to identify root causes
2. Comparing multiple improvement options before acting
3. Course-correcting when the original Plan's assumptions were wrong

## The 5 Phases

### Phase 1: Plan

Define the goal and execution plan.

Tasks:
- Define the goal in one sentence
- Set success criteria (what "done" looks like)
- List concrete steps
- Confirm assumptions, constraints, and risks
- Identify required tools and resources

Output format:
```
## Plan
- Goal: [one sentence]
- Success criteria: [specific conditions]
- Steps:
  1. [step 1]
  2. [step 2]
  ...
- Assumptions/Constraints: [if any]
- Risks: [anticipated risks]
```

### Phase 2: Do

Execute the task according to the plan.

Tasks:
- Execute steps from the Plan in order
- Record events, decisions, and deviations during execution
- If something unexpected happens, record it and move on (don't fix it here)

Output format:
```
## Do
- Execution log:
  - [Step 1]: [result/findings]
  - [Step 2]: [result/findings]
  ...
- Unexpected events: [if any]
```

### Phase 3: Check

Evaluate execution results against the Plan's success criteria.

Tasks:
- Check each success criterion: achieved or not achieved
- Describe the gap between expected and actual results
- List what went well and what didn't
- Form a root cause hypothesis (but don't design solutions yet)

Output format:
```
## Check
- Success criteria assessment:
  - [Criterion 1]: Achieved / Not achieved — [reason]
  - [Criterion 2]: Achieved / Not achieved — [reason]
- Gap: [expected vs. actual]
- What went well: [description]
- What didn't go well: [description]
- Root cause hypothesis: [description]
```

### Phase 4: Re-Plan — The core of PDCPA

Re-design the Action plan based on Check results.
This is the key difference from traditional PDCA. After understanding "what happened" in Check, deliberately design "what to do next."

In this phase, rather than the AI deciding unilaterally, present options to the user and decide together. Getting the user's judgment ensures the best option is chosen considering real-world priorities and constraints.

Tasks:
- Validate and refine the root cause hypothesis from Check
- Generate multiple improvement options (at least 2)
- Organize pros, cons, and estimated improvement rate for each option
- **Use the AskUserQuestion tool to present options and let the user choose**
- Build a concrete action plan based on the user's selection
- Review and revise the original Plan's assumptions if needed

#### Presenting options to the user

After completing the Re-Plan analysis, present improvement options via AskUserQuestion.
Each option should include:
- **label**: Option name (append "(Recommended)" to the recommended option)
- **description**: Summary of pros, cons, and estimated improvement rate

Recommendation criteria: Recommend the option with highest feasibility, lowest risk, and greatest improvement impact. Place the recommended option first in the options list.

AskUserQuestion example:
```
question: "Re-Plan: Based on the Check results, I've evaluated these improvement options. Which approach should we take?"
header: "Improvement options"
options:
  - label: "Option A: Add indexes (Recommended)"
    description: "Est. improvement: 80%↑ | Pros: High immediacy, low risk | Cons: May recur as data volume grows"
  - label: "Option B: Full query rewrite + caching"
    description: "Est. improvement: 95%↑ | Pros: Fundamental fix, long-term stability | Cons: High effort (1-2 weeks), regression risk"
  - label: "Option C: Read replica"
    description: "Est. improvement: 60%↑ | Pros: Distributes DB load overall | Cons: Increased infra cost, takes time to build"
```

After the user selects, build the action plan based on their choice. If the user enters a custom response via "Other", adjust the action plan accordingly.

Output format (recorded after user selection):
```
## Re-Plan
- Root cause (refined): [description]
- Options:
  1. [Option A] (Recommended): Est. improvement [X%] / Pros / Cons
  2. [Option B]: Est. improvement [X%] / Pros / Cons
- User selection: [Option X]
- Action plan:
  1. [concrete step 1]
  2. [concrete step 2]
  ...
- Revisions from original Plan: [assumptions to correct, if any]
```

### Phase 5: Action

Execute the action plan from Re-Plan and complete the cycle.

Tasks:
- Execute improvements according to the Re-Plan action plan
- Record execution results
- Summarize lessons learned for future cycles
- Propose starting the next PDCPA cycle if needed

Output format:
```
## Action
- Improvements executed:
  - [Action 1]: [result]
  - [Action 2]: [result]
- Lessons learned: [insights for the future]
- Next cycle: Needed / Not needed — [reason]
```

## Usage

### For task management

When the user says "run this with PDCPA" or "/pdcpa":
1. Confirm the goal with the user, then create Phase 1 (Plan)
2. Get user approval before proceeding to Phase 2 (Do)
3. Present each phase's output in the formats above
4. In Phase 4 (Re-Plan), present options via AskUserQuestion and let the user choose

### As a problem-solving framework

When the user reports a problem or bug and wants a systematic approach:
1. Convert the problem into a goal and create Phase 1 (Plan)
2. Execute investigation/fixes as Phase 2 (Do)
3. Verify results in Phase 3 (Check)
4. If insufficient, design alternative approaches in Phase 4 (Re-Plan)
5. Apply the final fix in Phase 5 (Action)

### Resuming mid-cycle

If the cycle was interrupted, resume from the current phase. Confirm which phase to resume from with the user.

## Guidelines

- Keep each phase's output concise. Prioritize concrete facts and actions over verbose explanations
- Never skip Phase 4 (Re-Plan). This is the core of PDCPA — skipping it reduces it to standard PDCA
- Value dialogue with the user. Especially in Plan and Re-Plan, confirm the user's input
- If one cycle isn't enough, propose the next cycle
