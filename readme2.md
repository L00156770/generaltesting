| [Return to Home](README.md) ▸ **Branching Strategy** |
| ---------------------------------------------------- |

# Branching Strategy

Team Marvel has selected the branching strategy of:  [**GitHub Flow**](https://guides.github.com/introduction/flow/)  
Below are the 
- [Branch Naming Conventions](#branch-naming-conventions)
- [Develop a new feature](#develop-a-new-feature)
- [Develop multiple features in parallel](#develop-multiple-features-in-parallel)
- [Create and deploy a release](#create-and-deploy-a-release)
- [Change in plan, pull a feature from a release](#change-in-plan-pull-a-feature-from-a-release)
- [Change request](#change-request)
- [Production hot fix](#production-hot-fix)
- [Develop in a platform repo](#platform-repo)

## Branch Naming Conventions

| Branch Name | Pull Request Required? | Base Branch | Description | Example |      
| ------------|------------------------|-------------|-------------|---------|
| `master`| YES         | N/A              | The source of truth branch.  Must always be stable and ready for Production deploy. | N/A
| feature | NO          | `master`         | Used for active development features (such as User Stories or code changes).  Merges into master from a Pull Request. |
| `hotfix-*` | NO       | `master`         | These are critical defect/bug fixes against production. Merges into master from a Pull Request. | hotfix-

## Develop a new feature

1. Create a feature branch based off of `master`.

   ```
   $ git checkout master
   $ git checkout -b MYTEAM-123-new-documentation
   $ git push --set-upstream MYTEAM-123-new-documentation
   ```

1. Develop the code for the new feature and commit as you go.

   ```
   $ ... make changes
   $ git add -A .
   $ git commit -m "Add new documentation files"
   $ ... make more changes
   $ git add -A .
   $ git commit -m "Fix some spelling errors"
   $ git push
   ```

1. Navigate to the project on [Github](www.github.com) and open a pull request
with the following branch settings:
   * Base: `master`
   * Compare: `MYTEAM-123-new-documentation`

1. When the pull request has been reviewed and ![+1'd](images/plus1.png)
, merge and close it and then delete the `MYTEAM-123-new-documentation`
branch. This can all be done from the Github pull-request page.

1. Deploy `master` to a staging environment to verify (_some teams have this
    automated, some prefer a manual deploy with some conventions, either is fine_).

1. If everything is good in staging, promote it to production and you're done.
If not, roll back production to the previous release and return to Step 1.

## Develop multiple features in parallel

There's nothing special about that. Each developer follows the above
[Develop a new feature](#develop-a-new-feature) process.

During development, make sure to update from `master` often so that when you
get ready to complete your feature you don't have to deal with large code
conflicts.

## Production hot fix

*In rare situations you may need to get a fix into production fast! Use this
workflow to push a hotfix to production when you can't spare the time to
follow the standard 'Develop a feature' workflow.*

![Hotfix **use rarely**](images/continuous-hotfix.png)

*This is very similar to how we [Develop a new feature](#develop-a-new-feature)
described above.*

1. Make sure your `master` branch is up-to-date

   ```
   $ git checkout master
   $ git fetch
   $ git merge origin/master
   ```

1. Create a hot fix branch based off of `master`

   ```
   $ git checkout -b hotfix-documentation-broken-links
   $ git push --set-upstream hotfix-documentation-broken-links
   ```

1. Add a test case to validate the bug, fix the bug, and commit
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

1. Navigate to the project on [Github](www.github.com) and open a pull request
   with the following branch settings:
   * Base: `master`
   * Compare: `hotfix-documentation-broken-links`

1. When the pull request has been reviewed and ![+1'd](images/plus1.png)
   , merge and close it and then delete the `hotfix-documentation-broken-links`
   branch. This can all be done from the Github pull-request page.

## Develop in a platform repo

A platform repo contains both Progressive Mobile App and Progressive Mobile Web
source code.

The development process is the same as outlined above in
[Develop a new feature](#develop-a-new-feature).

**However**, branches have to be prefixed based on the following rules:
* `app-`, for changes mainly touching Progressive Mobile App code.
* `web-`, for changes mainly touching Progressive Mobile Web code.
* `platform-`, for changes touching both Progressive Mobile App and Web code.
