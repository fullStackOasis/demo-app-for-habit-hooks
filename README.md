This is a demo app.

# Use Python version 3.11

To start:

```
pyenv local 3.11
```

Now run the sample code from inside src dir:
```
python -c "from a import ATest; print(ATest().say_hello())"
```
Expected output is "Hello, Alice!"

# Test snooze

In order to test snooze, check in two files that both have code smells. Example output:

```
habit-hooks
── too-many-parameters (2 issues) ──

High parameter count is a sign of coupling.
Parameters that travel together across several calls are a missing abstraction.

**Find the missing abstraction:**
1. Look at the call sites and nearby functions — is there an existing class a group of these parameters belongs to?
2. If not, create it — then move behaviour that uses those fields onto it.
3. If one object owns most of the parameters, it may be the natural home for this function.

Useful tip: rewrite each call site with the signature that feels natural there, and let that shape the final method. 

**AVOID**: A `{ ...everything }` bag that merely renames the list hides the coupling instead of removing it.

src/a.py:7
src/b.py:4
```
