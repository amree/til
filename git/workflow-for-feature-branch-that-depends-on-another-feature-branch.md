# Workflow For Feature Branch That Depends on Another Feature Branch

## The problem
* A was given a task to write a new feature
* A created a new branch called `branch-a` from `master`
* A started doing some commits
* B was given a new task that depends on `branch-a`
* B created a new branch out from `branch-a` called `branch-b`
* A created a PR for early feedback by setting it to compare with
  `master`
* B created a PR for early feedback too by setting it to compare with
  `branch-a` so that reviewers can only see his changes, not changes
including commits from `branch-a`
* A finished writing his feature and wanted to merge to `master`
* Due to the company policy, he needs to squash his commit before
  merging to `master`
* How can A merge his changes to the `master`?
* How can B merge his changes to the `master` after A?

### How not to do it

* A rebased his commits against master into one single commit
* He merged his changes and deleted `branch-a`
* RESULT: PR by B will be closed automatically and cannot be re-opened
  at this point

### One correct way to do it

* A rebased his commits against master into one single commit
* He merged his changes
* B update his local master branch
* B changed base to the `master` for his PR in GitHub
* B rebased to `master` by only playing back his  commits `git rebase
  --onto master HEAD~X`
* B git push force `branch-b`
* After PR reviewed, B merge `branch-b` to `master`

## Note
* B’s PR won’t be closed down if the git history is still available
* Basically, just don’t delete `branch-a`, at least not untill
  `branch-b` has changed the base to `master`

## References

* http://stackoverflow.com/questions/22593087/merging-a-branch-of-a-branch-after-first-branch-is-squashed-when-merged-to-maste
