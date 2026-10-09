# aap.1 patch on django-storages 1.14.6

This branch is upstream release `1.14.6` plus one change to `storages/backends/azure_storage.py`,
versioned `1.14.6+aap.1`:

- the user delegation key is requested with a start time five minutes in the past and a lifetime
  just under the seven-day maximum, so a client clock slightly ahead of Azure's cannot make the key
  "not yet valid";
- every SAS URL carries a `start` one minute in the past for the same reason.

Nothing else differs from upstream. Rebase this branch onto the next upstream release and bump the
label (`+aap.2`) if the change is still needed; upstream `master` does not carry it.

Use it from a project either as a vendored wheel (`pip wheel --no-deps -w vendor .` at the tag, then
`--find-links vendor` and `django-storages==1.14.6+aap.1` in `requirements.txt`) or directly from
git where that is acceptable: `django-storages @ git+https://github.com/andyp05/django-storages@1.14.6-aap.1`.
