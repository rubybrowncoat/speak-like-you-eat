---
id: decision-5
title: Keep host-native SLYE paths and accept OMP asynchronous persistence
date: '2026-09-27 22:41'
status: accepted
---
## Context

Integrating OMP support with the later custom-prompt feature exposed host differences in configuration paths, project trust and persistence acknowledgement. OMP 18.3.5 remaps the shared Pi imports to its own directories, reports projects as trusted and returns from `sendMessage` before asynchronous persistence finishes. Investigation and operator acceptance are recorded in [TASK-17](../tasks/task-17%20-%20Integrate-and-review-PR-5-against-current-main.md).

## Decision

Keep host-native configuration and prompt paths instead of implicitly sharing Pi and OMP files. Follow the host's project-trust policy. Accept OMP's asynchronous persistence limitation rather than adding acknowledgement or retry machinery to this adapter: a later host-owned persistence failure is not observable by SLYE and can leave the target marked complete without a stored card.

## Consequences

Pi and OMP users configure their own host/profile paths. OMP does not acquire a Pi-style approval gate through SLYE. Provider failures remain retryable as specified, but a successful OMP send submission is not proof of durable storage. The [current specification](../docs/specs/doc-1%20-%20SLYE-MVP-specification.md) defines the supported behavior and limitation; the [prompt runbook](../docs/runbooks/doc-6%20-%20Customize-the-SLYE-system-prompt.md) gives host-specific setup instructions.
