# branching

LinuxGSM has now moved from a rolling release to scheduled releases. This is due to the size of the project and the requirement to better manage features and bug fixes.

LinuxGSM uses the GitFlow method of releases. Relying on master, develop, feature and hotfix branches. [http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/)

The "master" branch will be the stable release branch. The "develop" branch is for developing stable code. All code is to be developed in a feature branch. This can also contain the developers username. e.g feature-dgibbs-newgame Once it is stable it can be merged in to the "develop" branch.

When code from the "develop" branch when ready is split off in to a "release" branch. The "release" branch does not have any more features added to it. It is then tested and any bugs fixed it will be released in to master and tagged as a version number. The release will also be merged back in to the develop branch.

Should there be a critical issue that needs resolving in the master branch that cannot wait for the next release a "hotfix" branch is created from the master branch. The issue is resolved and merged in to master and develop

Only Daniel Gibbs is designated to complete releases. Code can be merged in to develop if you are happy with your code. However if there are any doubts it is recommended that a pull request is made to allow peer review before it is merged.

Any non-group developers please submit pull requests to the "develop" branch and use "develop" branch as a base.

It is also a good idea to start using [Git Kracken](https://www.gitkraken.com/) as the git client. It is a little more complex that GitHub Desktop but will give you a much better understanding of the development process.

![Git Model](http://nvie.com/img/git-model@2x.png)

![feature release flowchart](http://i.imgur.com/E241CSR.jpg)
