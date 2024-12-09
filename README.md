# How to reproduce duplicate entries in GitHub Dependency Graph

Here are the required steps to reproduce duplicate gradle dependencies being introduced in the Dependency Graph. 
The project i was working on had adopted this setup with submission+review based on this demo pointed by the [documentations of the official gradle/actions/dependency-submission action](https://github.com/gradle/actions/blob/895252588e0dfbf80467d2d33f34a3ee85235009/docs/dependency-submission.md).

After having observed duplicates magically appear and dissappear on GitHub and triaging this with the GitHub Support team, we pinpointed the nessecary steps to reproduce as follows:

1. Fork the [official repo](https://github.com/gradle/github-dependency-submission-demo/fork) and enable Dependency Graph on the fork.
2. [Enable Actions to be ran on the fork](https://github.com/lislei/github-dependency-submission-demo-test/actions).
3. When merging a branch, the "dependency snapshot" related to a commit is mutating the Dependency Graph. 
 - This despite the message returned by the Dependency Graph Dependency Submission API REST endpoint:
   > "The snapshot was accepted, but it is not for the default branch. It will not update dependency results for the repository."
 - See #1 - at this point in time the Dependency Graph was of size 7.

