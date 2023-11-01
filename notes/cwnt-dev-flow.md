1. [rev] Fork the source repository
1. [rev] Clone the repository from my fork (origin) to local
1. [rev] In my local repository, register the source repository as remote
1. [rev] Create a review branch with the same name as the branch I will pull from
1. [rev] Once in this new branch, pull from the branch I will review using git pull source <review-branch>
1. [rev] On the first update with ripi, change the status to review-on-going
1. [rev] Conduct a code review
1. [rev] Once the stage is completed, commit the changes
1. [rev] Push to my origin from this branch
1. [rev] Notify that this step has been completed
1. [exe] Developer pulls the review branch to their local branch
1. [exe] Developer makes their changes
1. [exe] Developer commits locally
1. [exe] Developer pushes to their own origin
1. [exe] Notify that the push has been made
1. [rev] Pull from the source review branch to the local review branch

If the reviewer thinks it is finished:

1. [rev] Commit changes, changing the status to review approved
1. [rev] Make one last push to my origin
1. [rev] Notify the developer that it has been approved

If the reviewer thinks it is finished:

1. [exe] Developer pulls the review branch to their local branch

Closing the issue:

1. [exe] Switch to the develop branch
1. [exe] Once in develop, merge the review branch into it
1. [exe] Resolve what needs to be resolved in develop
1. [exe] Once everything is resolved, give the command to close the issue

Merging develop into master:

1. [aut] Create a tag in develop v0.0.0-rc1 (semantic version)
1. [aut] Merge develop into staging
1. [aut] Create a tag in staging v0.0.0 (semantic version)
1. [aut] Merge staging into master
