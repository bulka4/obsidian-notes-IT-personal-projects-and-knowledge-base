Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
**Trunk-based development** is a Git workflow where developers work on a single main branch (the **trunk**) and integrate changes frequently.

Trunk-based development is common in companies practicing continuous delivery because it reduces merge conflicts and keeps the codebase close to deployable.
# Typical structure
```
main (trunk)
A---B---C---D---E
```

Developers usually:
- make small changes,
- commit often,
- merge to `main` frequently (often daily),
- avoid long-lived feature branches.

For larger changes, they may use very short-lived branches:
```
main:    A---B---C---D
              \
feature:       X---Y
```

The feature branch exists briefly, then is merged:
```
main:    A---B---C---D---M
              \         /
feature:       X---Y----
```
# Key ideas:
- **Small, frequent integrations** instead of big merges.
- **Avoid long-running branches** that diverge for weeks/months.
- Often combined with:
    - CI/CD pipelines
    - automated tests
    - feature flags (merge incomplete features but keep them disabled)
# Compared to Git Flow:
- **Trunk-based:** one main branch, frequent integration.
- **Git Flow:** long-lived branches like `develop`, `release`, `feature`.