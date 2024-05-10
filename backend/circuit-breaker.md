# Circuit Breaker

## Resiliency

- A failure in a service should not break the user experience
- The API should automatically take corrective action when 1 of its service dependencies fails
- The API should be able to show us what's happening right now or at past. (error logging)

## Why use CB ?

Service A -> Service B

- Wasteful calls can pile up in the target service, further escalating the problem.
- Dangling Calls might use the initiator's thread while waiting for the target.
- The issue can cascade since the initiator can be brought down by waiting.
- Log pollution

## States

- Closed
- Open
- Half-Open

```
{
    failureCount: 0,
    successCount: 0,
    nextAttempt: 0
}
```
