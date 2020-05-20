| [Return to README.MD](../README.md)
| ---------------------------------------------------- |

# Branching Strategy

Team Marvel has selected the branching strategy of:  [**GitHub Flow**](https://guides.github.com/introduction/flow/)  
This document outlines the team agreements of this strategy and provides example details of the process.

- [Branch Naming Conventions](#branch-naming-conventions)
- [Development Process for New Feature](#development-process-for-new-feature)
- [Development Process for Hotfix](#development-process-for-hotfix)
- [Development Process for Documentation](#development-process-for-hotfix)
- [Team Marvel Considerations](#team-marvel-considerations)

## Branch Naming Conventions

| Branch Name | Base Branch | Pull Request? | Description | Example |      
| ------------|------------------------|-------------|-------------|---------|
| `master`    | N/A                    | N/A         | The source of truth branch.  Must always be stable and ready for Production deploy. | N/A
| feature | `master`                          | NO   | Used for active development features (such as User Stories or code changes).  Merges into master from a Pull Request (required). | feature-GWEEDRDP-99-create-login-page
| hotfix | `master`                       | NO    | Used for critical defect/bug fixes against production. Merges into master from a Pull Request (required). | hotfix-GWEEDRDP-99-broken-link
| documentation | `master`                   | NO   | Used for updating project documentation. Merges into master from a Pull Request (required). | documentation

## Development Process for New Feature

1. Pull from master into defined branch pattern like so:
   ```
   $ git clone https://github.com/rlennon/GweedoreDP.git
   $ cd GweedoreDP
   $ git checkout master
   $ git checkout -b feature-GWEEDRDP-99-create-login-page
   $ git push --set-upstream origin feature-GWEEDRDP-99-create-login-page
   ```

2. Develop approriate code changes, add, commit, push:
   ```
   $ git add -A
   $ git commit -m "Enter clear description of the commit reason/details"
   $ git push
   ```

3. Navigate to the GweedoreDP project on [Github](https://github.com/rlennon/GweedoreDP):
   1. Open Pull Request with respective branch name (e.g. feature-GWEEDRDP-99-create-login-page)
   2. Pull Request must be reviewed to merge into Master
   3. Once reviewed/approved, merge can be completed into Master
      -*NOTE:  Deleting branch is recommended, but for purposes of this project, we will not delete any branches.*
   4. Deploy master to staging environment.  
      *If build/tests pass in staging, deploy to Production
       If build/tests fail in staging, rollback changes to previous release and restart process*  
   
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

3. Test cases/validation should be done to mitigate deployment risk.  
   ```
   $ git add -A
   $ git commit -m "Enter clear description of the commit reason/details"
   $ git push
   ```

4. Navigate to GweedoreDP project on [Github](https://github.com/rlennon/GweedoreDP) and open a Pull Request

## Development Process for Documentation

1. Pull from master into defined branch pattern:
   ```
   $ git checkout master
   $ git checkout -b documentation
   $ git push --set-upstream origin documentation
   ```

2. Develop approriate code changes, add, commit, push:
   ```
   $ git add -A
   $ git commit -m "Enter clear description of the commit reason/details"
   $ git push
   ```

3. Navigate to the GweedoreDP project on [Github](https://github.com/rlennon/GweedoreDP):
   1. Open Pull Request with respective branch name (e.g. documentation)
   2. Pull Request must be reviewed to merge into Master
   3. Once reviewed/approved, merge can be completed into Master
      -*NOTE:  Deleting branch is recommended, but for purposes of this project, we will not delete any branches.*
   4. Deploy master to staging environment.  
      *If build/tests pass in staging, deploy to Production
       If build/tests fail in staging, rollback changes to previous release and restart process*  
   
## Team Marvel Considerations
**Why did Team Marvel choose this strategy?**  
```
1. There are a variety of different branching strategies, however, we felt Github Flow was the best option for  
this short project.
2. Github Flow provides easy management of branching without over-complicating the process.

Other Comments:   
-Need to refine staging/deploy environments
-Need to create build tests and communication path/rollback if build fails in stating prior to Prod deploy
-Need to define if documentation branch should be merged into master (currently, yes, but might change to no)
```
