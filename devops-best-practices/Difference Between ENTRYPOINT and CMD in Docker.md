# Difference Between ENTRYPOINT and CMD in Docker

Most Docker beginners (and sadly many intermediates) **misuse `ENTRYPOINT` and `CMD`** because they memorize definitions instead of understanding execution behavior.

This file explains the **real difference**, **when to use what**, and **how Docker actually executes containers**.

---

## 1. CMD

### What it does
`CMD` provides **default arguments** for a container.

- Can be **easily overridden** at runtime
- Only **one CMD** is allowed (last one wins)
- Meant to be flexible

### Example
```dockerfile
FROM ubuntu
CMD ["echo", "Hello World"]
```
Run:

docker run my-image

Output:

Hello World

Override CMD:

docker run my-image echo Hi

Output:

Hi

🔴 Important:
When you pass a command at runtime, CMD is completely replaced.

When to use CMD

You want a default command

You expect users to override it

The container behavior should be flexible



---

2. ENTRYPOINT

What it does

ENTRYPOINT defines the main executable of the container.

Not overridden by default

Runtime arguments are appended

Enforces container behavior


Example

FROM ubuntu
ENTRYPOINT ["echo"]

Run:

docker run my-image Hello

Output:

Hello

🔴 Important:
Docker appends runtime arguments to ENTRYPOINT.

When to use ENTRYPOINT

The container has a single responsibility

You want to prevent accidental command replacement

You're building CLI-style containers



---

3. ENTRYPOINT + CMD (Best Practice)

This is how experienced Docker engineers design images.

Example

FROM python:3.11
ENTRYPOINT ["python", "app.py"]
CMD ["--help"]

Run without arguments:

docker run my-image

Equivalent to:

python app.py --help

Override CMD only:

docker run my-image --version

Equivalent to:

python app.py --version

✔ ENTRYPOINT → What always runs
✔ CMD → Default arguments


---

4. Execution Rule (Critical to Remember)

Docker executes containers as:

ENTRYPOINT + CMD

If:

Only CMD exists → it runs directly

Both exist → CMD becomes arguments to ENTRYPOINT

Runtime args override CMD, not ENTRYPOINT



---

5. Common Mistakes

❌ Using CMD for mandatory commands
❌ Expecting ENTRYPOINT to be overridden easily
❌ Not using exec form (["cmd", "arg"])
❌ Writing shell form and causing signal-handling issues


---

6. Exec Form vs Shell Form

Exec Form (Recommended)

CMD ["nginx", "-g", "daemon off;"]

Shell Form (Avoid)

CMD nginx -g "daemon off;"

Why exec form?

Proper signal handling

Correct PID 1 behavior

Cleaner process management



---

7. Quick Comparison Table

Feature	CMD	ENTRYPOINT

Purpose	Default command/args	Main executable
Overridable	Yes	No (by default)
Runtime Args	Replace CMD	Append to ENTRYPOINT
Best Use	Defaults	Enforced behavior



---

Final Takeaway

If you don’t understand ENTRYPOINT vs CMD,
you are not controlling your containers — Docker is.

Learn the execution model.
Design with intent.
Stop guessing.


---

Author

If this helped you, ⭐ the repo and share with your team.

---

