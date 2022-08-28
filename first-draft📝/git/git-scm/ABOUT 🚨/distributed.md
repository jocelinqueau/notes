# Distributed

One of the nicest features of any Distributed SCM, Git included, is that it's distributed. This means that instead of doing a "checkout" of the current tip of the source code, you do a "clone" of the entire repository.

## Multiple Backups

This means that even if you're using a centralized workflow, every user essentially has a full backup of the main server. Assure againt crash

## Any Workflow

Because of Git's distributed nature and superb branching system, an almost endless number of workflows can be implemented with relative ease.

### Subversion-Style Workflow

A centralized workflow is very common, especially from people transitioning from a centralized system. Git will not allow you to push if someone has pushed since the last time you fetched, so a centralized model where all developers push to the same server works just fine.

![Workflow A](https://git-scm.com/images/about/workflow-a@2x.png)

### Integration Manager Workflow

![Workflow B](https://git-scm.com/images/about/workflow-b@2x.png)