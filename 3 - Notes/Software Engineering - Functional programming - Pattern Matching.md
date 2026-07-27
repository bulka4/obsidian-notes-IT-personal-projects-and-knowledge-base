Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Pattern matching is a way to check the structure or type of a value and execute different code depending on what it is.

Instead of using `if / elif`, we use `match / case` (in Python). 

It is more powerful than simple `if/elif` because it can match:
- types
- object structures
- values
- combinations of fields
# Examples
For example, using `match / case` we can write:
```python
for event in events:
    match event:
        case {"type": "user_created", "id": user_id, "name": name}:
            create_user_profile(user_id, name)

        case {"type": "payment_failed", "id": payment_id, "reason": reason}:
            notify_payment_failure(payment_id, reason)

        case {"type": "user_deleted", "id": user_id}:
            delete_user_profile(user_id)
```

which is easier than using `if / elif`:
```python
for event in events:
    if event["type"] == "user_created":
        user_id = event["id"]
        name = event["name"]
        create_user_profile(user_id, name)

    elif event["type"] == "payment_failed":
        payment_id = event["id"]
        reason = event["reason"]
        notify_payment_failure(payment_id, reason)

    elif event["type"] == "user_deleted":
        user_id = event["id"]
        delete_user_profile(user_id)
```
