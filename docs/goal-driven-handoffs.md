# Improvement request: keep multi-agent work moving toward a goal

## Problem

A user can ask agents in a group chat to collaborate on a goal, but the exchange may stop after a few replies. Agents report findings or describe a next step, then wait for another user message even though safe work remains. The user has to keep restarting the discussion, and the original goal can lose momentum.

This is especially visible when one agent works on a separate machine from another. Bot Mode documents @mentions as a handoff that waits for a reply and reports back. That covers a single exchange, but it does not describe ownership of a longer task across multiple turns.

## Requested improvement

Add an optional goal-driven handoff mode for multi-agent work. When a user explicitly assigns a goal, the coordinating agent should retain that goal and continue with safe, useful next steps after each reply. It should pause for the user only when it needs a decision, permission for a consequential action, or a missing piece of information. Each agent should report a concrete blocker or hand off a specific next action rather than ending with a status update alone.

The mode should be opt-in and bounded. It must not authorize external writes, deployments, or other consequential actions that the user has not approved. It should support a clear stop/cancel action and prevent duplicate or circular handoffs.

## Acceptance criteria

- A user can explicitly start a multi-agent task with a goal and a coordinator.
- The coordinator tracks progress and the next action across replies, including when agents run on separate machines.
- The coordinator continues read-only or otherwise authorized work without requiring a fresh user prompt after every turn.
- When a real blocker is reached, the coordinator asks one focused question or names the exact approval needed.
- Agents do not treat an unapproved consequential action as authorized just because it advances the goal.
- The user can stop the workflow, and the coordinator does not loop or duplicate a completed handoff.
- The user receives a concise completion report grounded in completed and verified work.

## Scope note

This request concerns durable coordination across turns and machines. It is separate from the existing single @mention reply flow and from live interruption of a bot that is already running.
