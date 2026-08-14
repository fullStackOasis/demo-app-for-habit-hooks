This is a demo app that is used to test habit hooks.

# Typescript project

The issue is described in this [finding file](https://github.com/habit-hooks/habit-hooks/blob/findings/executable-specs/docs/findings/01-prune-empties-a-filtered-index.spec.md).

You have to set up all the files as described there.

We have done that, including the `.habit-hooks/snooze.json` file.

There are three smells listed in `.habit-hooks/generic/sensors/alpha.json`. Two of them have been ignored, which you can confirm by running `habit-snooze`:

```
habit-snooze --list
src/x.js
src/y.js
```

If you then run this command, you do not get an error, and the snoozed list vanishes.

```
habit-sensors --all | habit-snooze --prune
cat .habit-hooks/snooze.json
[]
```
