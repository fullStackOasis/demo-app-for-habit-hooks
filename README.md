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

## pyproject.toml is required

As of this writing, if pyproject.toml is not included in the project, habit-hooks will fail with an error.

You can test this by simply removing it from the project (delete the file) and then run `habit-hooks`.

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

## list snoozed files

"Snoozed" files are files that have had "smells" detected, but habit-hooks has been told to ignore them.

Example:

```
habit-sensors --all | habit-snooze --snooze
```
There is no output from this command. However, you can see what happened here:
```
cat .habit-hooks/snooze.json
["src/a.py", "src/b.py"]
```
And then run:
```
habit-snooze --list
src/a.py
src/b.py
```
Despite the fact that these issues have been snoozed, you can still sense the smells as follows:
```
habit-sensors --all --no-snooze
[{"smell": "too-many-parameters", "details": {}, "issues": [{"key": "src/a.py", "details": {"file": "src/a.py", "line": 7, "column": 9, "message": "Too many arguments in function definition (6 > 5)", "source": "ruff:PLR0913"}}, {"key": "src/b.py", "details": {"file": "src/b.py", "line": 4, "column": 5, "message": "Too many arguments in function definition (7 > 5)", "source": "ruff:PLR0913"}}], "language": "python"}]
```

