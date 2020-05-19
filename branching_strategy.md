| [Return to Home](README.md) ▸ **Branching Strategy** |
| ---------------------------------------------------- |

# Branching Strategy

Team Marvel has selected the branching strategy of:  [**GitHub Flow**](https://guides.github.com/introduction/flow/)  
Below are the agreed processes for the project:
- [Branch Naming Conventions](#branch-naming-conventions)
- [Development Process for New Feature](#development-process-for-new-feature)
- [Development Process for Hotfix](#development-process-for-hotfix)
- [Development Process for Documentation](#development-process-for-hotfix)
- [Development Process for Documentation](#development-process-for-hotfix)
- [Team Marvel Considerations](#team-marvel-considerations)

## Branch Naming Conventions

| Branch Name | Pull Request Required? | Base Branch | Description | Example |      
| ------------|------------------------|-------------|-------------|---------|
| `master`    | YES                    | N/A         | The source of truth branch.  Must always be stable and ready for Production deploy. | N/A
| feature | NO                         | `master`    | Used for active development features (such as User Stories or code changes).  Merges into master from a Pull Request (required). | feature-GWEEDRDP-99-create-login-page
| hotfix | NO                      | `master`    | These are critical defect/bug fixes against production. Merges into master from a Pull Request (required). | hotfix-GWEEDRDP-99-broken-link
| documentation | NO                      | `master`    | These are critical defect/bug fixes against production. Merges into master from a Pull Request (required). | documentation-update-branch-strat

## Development Process for New feature

1. Pull from master into defined branch pattern:
   ```
   $ git checkout master
   $ git checkout -b feature-GWEEDRDP-99-create-login-page
   $ git push --set-upstream feature-GWEEDRDP-99-create-login-page
   ```

2. Develop approriate code changes, add, commit, push:
   ```
   $ git add -A .
   $ git commit -m "Added new feature code"
   $ git push
   ```

3. Navigate to the project on [Github](www.github.com):
   1. Open Pull Request with respective branch name (e.g. feature-GWEEDRDP-99-create-login-page)
   2. Pull Request must be reviewed to merge into Master
   3. Once reviewed/approved, merge can be completed into Master
      -NOTE:  Deleting branch is recommended, but for purposes of this project, we will not delete any branches
   4. Deploy master to staging environment.  
      -If build/tests pass in staging, deploy to Production
      -If build/tests fail in staging, rollback changes to previous release and restart process

## Development Process for Hotfix
*use only for critical bugs requiring immediate fix*

1. Make sure your `master` branch is up-to-date

   ```
   $ git checkout master
   $ git fetch
   $ git merge origin/master
   ```

2. Create a hot fix branch based off of `master`

   ```
   $ git checkout -b hotfix-broken-links
   $ git push --set-upstream hotfix-broken-links
   ```

3. Add a test case to validate the bug, fix the bug, and commit
   *When doing a hotfix you should at _least_ pair on the fix with somebody or
   review it in person with one other engineer before releasing it. We're
   running without training wheels here and want to do our best not to have to
   do a stream of hotfixes in production.*
   ```
   ... add test, fix bug, verify
   $ git add -A .
   $ git commit -m "Fix broken links"
   $ git push
   ```

4. Navigate to the project on [Github](www.github.com) and open a pull request
   with the following branch settings:
   * Base: `master`
   * Compare: `hotfix-broken-links`

## Development Process for Documentation

1. Pull from master into defined branch pattern:
   ```
   $ git checkout master
   $ git checkout -b documentation-update-branch-strat
   $ git push --set-upstream documentation-update-branch-strat
   ```

2. Develop approriate code changes, add, commit, push:
   ```
   $ git add -A .
   $ git commit -m "Added new feature code"
   $ git push
   ```

3. Navigate to the project on [Github](www.github.com):
   1. Open Pull Request with respective branch name (e.g. documentation-update-branch-strat)
   2. Pull Request must be reviewed to merge into Master
   3. Once reviewed/approved, merge can be completed into Master
      -NOTE:  Deleting branch is recommended, but for purposes of this project, we will not delete any branches
   4. Deploy master to staging environment.  
      -If build/tests pass in staging, deploy to Production
      -If build/tests fail in staging, rollback changes to previous release and restart process

## Team Marvel Considerations
```
Why did Team Marvel choose this strategy?   
1. Reason 1
2. Reason 2

Other Comments:   
Various branching strategies possible, etc
Important to tack into account infrastructure and project needs when choosing a strategy
```
