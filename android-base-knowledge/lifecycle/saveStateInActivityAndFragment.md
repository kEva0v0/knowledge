# Activity和Fragment的onSaveInstance、onRestoreInstance

## Activity saveInstance

ActivityThread有一段指的是如果Before Android P 就在onStop前调用，After Android P就在onStop之后调用
```
private void callActivityOnStop(ActivityClientRecord r, boolean saveState, String reason) {
        // Before P onSaveInstanceState was called before onStop, starting with P it's
        // called after. Before Honeycomb state was always saved before onPause.
        final boolean shouldSaveState = saveState && !r.activity.mFinished && r.state == null
                && !r.isPreHoneycomb();
        final boolean isPreP = r.isPreP();
        if (shouldSaveState && isPreP) {
            callActivityOnSaveInstanceState(r);
        }
        ...
    }
```

## Activity restoreInstance

在onStart之后

```
    public void handleStartActivity(ActivityClientRecord r,
            PendingTransactionActions pendingActions) {
        final Activity activity = r.activity;
        if (r.activity == null) {
            // TODO(lifecycler): What do we do in this case?
            return;
        }
        if (!r.stopped) {
            throw new IllegalStateException("Can't start activity that is not stopped.");
        }
        if (r.activity.mFinished) {
            // TODO(lifecycler): How can this happen?
            return;
        }

        // Start
        activity.performStart("handleStartActivity");
        r.setState(ON_START);

        ...

        // Restore instance state
        if (pendingActions.shouldRestoreInstanceState()) {
            if (r.isPersistable()) {
                if (r.state != null || r.persistentState != null) {
                    mInstrumentation.callActivityOnRestoreInstanceState(activity, r.state,
                            r.persistentState);
                }
            } else if (r.state != null) {
                mInstrumentation.callActivityOnRestoreInstanceState(activity, r.state);
            }
        }
        ...
    }
```