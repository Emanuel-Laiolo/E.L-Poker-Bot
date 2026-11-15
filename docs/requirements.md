# Poker Bot — Software Requirements

**Version:** 0.1  
**Status:** Draft  
**Language:** Python

## 1. Project Scope

The project aims to develop an autonomous No-Limit Texas Hold'em poker bot capable of recognizing game states, making strategic decisions, and executing legal actions.

### Initial Scope

- Support one 6-max poker table.
- Recognize and track the complete state of a hand.
- Make autonomous preflop and postflop decisions.
- Use precomputed preflop strategies with action frequencies.
- Use GTO-based postflop strategies.
- Record hand histories and opponent actions.
- Operate on Windows.

### Out of Scope — Initial Version

- Multiple simultaneous tables.
- Exploitative strategy optimization.
- Developing a complete GTO solver from scratch.
- Operation in unauthorized poker environments.

## 2. Functional Requirements

### FR-01 — Game State Recognition

The system shall recognize:

- Hero's hole cards and community cards.
- Player positions and dealer position.
- Active players and their stack sizes.
- Pot size, current bets, and required call amount.
- Current betting round: preflop, flop, turn, or river.
- Available legal actions.

### FR-02 — Hand State Tracking

The system shall maintain the current hand state, including the sequence of actions taken by each player.

It shall detect new hands, changes between betting rounds, folds, raises, calls, and all-in situations.

### FR-03 — Preflop Strategy

The system shall:

- Load precomputed preflop strategy files.
- Identify the corresponding strategy using position, betting history, and supported game parameters.
- Retrieve action frequencies for Hero's exact card combination.
- Select actions according to the available frequencies.
- Report unsupported scenarios rather than using an incorrect strategy.

### FR-04 — Postflop Strategy

The system shall:

- Identify the relevant postflop situation.
- Retrieve a strategy from a supported GTO-based strategy provider.
- Interpret available actions, betting sizes, and frequencies.
- Select an action according to the retrieved strategy.
- Detect situations for which no compatible strategy is available.

The postflop strategy provider will be selected after technical feasibility analysis.

### FR-05 — Autonomous Action Execution

The system shall execute the selected action without requiring manual intervention during normal operation.

Before execution, the system shall verify that the action is legal and corresponds to the current hand state.

### FR-06 — Hand History

The system shall record:

- Hand identifier and relevant game state.
- Player actions and betting amounts.
- Decisions made by the bot.
- Available results and outcomes.

### FR-07 — Opponent History

The system shall maintain a history of observed opponent actions for future analysis.

Exploitative adjustments based on this information are excluded from the initial version.

### FR-08 — Configuration

The system shall support configuration of relevant operating parameters without modifying its source code.

### FR-09 — Error Handling

When the system encounters an invalid or uncertain game state, an unsupported strategy, or an execution error, it shall:

- Identify and record the problem.
- Avoid executing an unverified action.
- Allow the system to recover or be safely stopped.

## 3. Non-Functional Requirements

### NFR-01 — Reliability

The system shall validate recognized game states and strategic outputs before executing actions.

### NFR-02 — Performance

The system shall produce decisions within the time limits of the authorized game environment.

Maximum decision latency and resource budgets must be established through feasibility testing.

### NFR-03 — Resource Efficiency

The system shall operate within the available hardware resources.

CPU, RAM, storage requirements, and expected strategy coverage must be estimated and validated before finalizing the postflop architecture.

### NFR-04 — Maintainability

The system shall use a modular architecture with clearly defined responsibilities and interfaces.

Strategy providers, game-state recognition, and action execution must remain independently replaceable where practical.

### NFR-05 — Testability

Core poker logic and strategy selection shall be testable without connecting to a live poker table.

Automated tests shall cover normal scenarios, invalid inputs, and unsupported situations.

### NFR-06 — Platform Compatibility

The initial version shall operate on Windows using Python as its primary programming language.

### NFR-07 — Authorized Use

The system shall operate exclusively within the authorized environment and comply with its applicable rules.

## 4. Acceptance Criteria

The initial system will be considered functionally complete when:

- It can recognize and reconstruct a hand from preflop to completion.
- It can correctly identify supported preflop situations and reproduce their action frequencies.
- It can retrieve compatible postflop strategies for its declared supported scenarios.
- It can execute selected legal actions autonomously.
- It records decisions, relevant game states, and errors.
- It handles unsupported situations without inventing strategic information.
- It meets the performance and hardware limits established during feasibility testing.
- The required automated and end-to-end tests pass.

## 5. Development Milestones

**M1 — Preflop Strategy Engine**

Load preflop strategies, identify supported scenarios, and return correct action distributions using manually provided game states.

**M2 — Game State Recognition**

Recognize table information and reconstruct hand states from visual input.

**M3 — Postflop Strategy Engine**

Integrate a feasible postflop strategy provider and validate its supported scenarios.

**M4 — Autonomous Integration**

Connect recognition, strategy selection, and action execution into a complete system.

**M5 — Validation and Optimization**

Test complete hands, measure performance, identify failures, and improve reliability.

## 6. Open Decisions

The following decisions must be resolved before their dependent features are implemented:

- Exact competition rules, stack depths, rake, and supported betting formats.
- Postflop strategy provider and its coverage.
- Maximum acceptable decision latency.
- Available RAM, CPU, and storage budgets.
- Required recognition accuracy and recovery behavior.
- Exact criteria for the initial release and its supported scenarios.