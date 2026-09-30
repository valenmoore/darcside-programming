# Learning Github

Github is the version control we use for our codebase, kind of like Google Docs for code. It allows us to collaborate on the same project (repository) from different computers.

Here are a few links to somewhat-useful articles about GitHub: [About GitHub](https://docs.github.com/en/get-started/using-git/about-git), [GitHub for FRC](https://docs.wpilib.org/en/latest/docs/software/basic-programming/git-getting-started.html). 

## Basics
These links go into a little more detail than we need, but the basics are that we have a repository of code, which contains all of our files. Rather than staying only on one person's computer, all of the files stay on GitHub, and each member of the programming team has a folder on their computer that's a copy of what's in GitHub.

![Diagram of GitHub usage](https://learning.nceas.ucsb.edu/2024-06-delta/images/github-collaborators-diagram.png)

A team member can change code on their computer, "push" it to the GitHub so that the repository contains that code, and another team member can "pull" that code onto their computer so that they have the newest version.

## Branches
When working on different parts of the robot, we might want to have different versions of the repository at once; for example, one person might be working on the intake while the other person is working on the shooter. To make this easier, we use branches. Each branch contains a different copy of the code, and people can push and pull to their branch without interfering with each other.

![Diagram of GitHub branches](https://cdn.hashnode.com/res/hashnode/image/upload/v1679149719892/bbc52875-92d7-4815-a4cd-035d827e492a.png)

### What to do when you need to create/work on a branch
When you have a task to do, you always want to work on a new or existing branch that is NOT the main branch. We will have a branch that contains fully verified, working code (usually it will be called "production", "main" or something similar), so we don't want any untested code in that branch. To work on a task, you want to make a new branch off of main and give it a name for whatever task you are working on (for example, "fix-intake-jamming" or "improve-shooter-aim"). To do that you can:
- Select the branch you want to make a new branch off of, then click 'New branch from...'
    - Make sure the branch is updated first -- if there's a small blue arrow, checkout the branch and click 'Update Project'
![Checkout branch](images/new-branch.png)
or
- Go to the issue in GitHub and click 'Create a branch for this issue'. Then go to IntelliJ, click 'Update Project' and checkout that branch
![Branch from issue](images/new-branch-from-issue.png)
