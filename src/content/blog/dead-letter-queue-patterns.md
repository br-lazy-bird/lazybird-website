---
title: "Dead Letter Queue Patterns"
date: 2026-01-18
description: "Understanding dead letter queues and why they need consumers."
tags: ["event-driven", "rabbitmq", "message-queue"]
---

A Dead Letter Queue (DLQ) is where messages go when they can't be processed successfully. But having a DLQ isn't enough — you need to handle the messages in it.

## What is a Dead Letter Queue?

When a message fails processing after multiple retry attempts, it's moved to a DLQ instead of being lost. This is a safety net, but it's not a solution by itself.

## The Silent Failure Anti-Pattern

A common mistake is setting up a DLQ but never consuming from it:

```python
# Worker only consumes main queue
channel.basic_consume(queue='orders.queue', on_message_callback=process)

# DLQ exists but nobody reads from it!
# Failed messages accumulate silently...
```

## Proper DLQ Handling

A DLQ consumer should:

1. **Retry with backoff** — Give the downstream service time to recover
2. **Limit retries** — Don't retry forever
3. **Mark as failed** — After max retries, update the status and alert

```python
def handle_dlq_message(message):
    retry_count = get_retry_count(message)

    if retry_count < MAX_RETRIES:
        delay = 2 ** retry_count  # Exponential backoff
        republish_with_delay(message, delay)
    else:
        mark_as_failed(message)
        alert_ops_team(message)
```

## Learn by Doing

Try the [Order Processing](/systems) broken system to experience and fix silent DLQ failures!
