


# Git Tools
Number of useful tools which are designed to simplify rather complex git 
operations (at least from the users perspective)
Mostly wrappers over 
## git-transpose
Moves a branch to a new parent
### Usage
`git transpose <base branch> (--branch) <moving branch>`
`git transpose <base branch> (--branch) <moving branch>`
`git transpose <base branch> <base commit> (--branch) <moving branch>`
`git transpose <base branch> <base commit> (--single) <moving branch> <moving commit>`
`git transpose <base branch> <base commit> (--range) <moving branch> <first moving commit> <last moving commit>`
`git transpose <base branch> <base commit> (--range) <moving branch> <first moving commit> <last moving commit>`

> Can omit `<base branch>` if to be transposed onto `<current branch>`
#### *Options*
   Long Form    | Short Form | Description
----------------|------------|-------------
`--base-branch` |            | The branch onto which other branch will be transposed
`--base-commit` |            | The commit within the branch which will become the parent commit to the branch
`--new-branch`  |            | Creates a branch with given name which will be used to transpose commits
`--branch`      |            | Identifies the branch which will be transposed
`--single`      |            | Identifies the single commit which will be transposed
`--range`       |            | Identifies the contiguous set of commits which will be transposed
`--range-start` |            | Identifies the first commit of the contiguous set of commits which will be transposed
`--range-end` |            | Identifies the last commit of the contiguous set of commits which will be transposed
`--multiple`    |            | Identifies the set of commits (not guaranteed to be continguous) which will be transposed, order which passed used to determine order in which they are transposed
`--preserve`    |            | Preserves the original commit(s), or if branch transposed prefixes original with '-old'
## git-inject
Moves commits from one location and places them within commits
### Usage
`git inject <host branch> <preceding host commit> <moving commit>`
> Can omit `<base branch>` if to be transposed onto `<current branch>`
#### *Options*
   Long Form                       | Short Form | Description
-----------------------------------|------------|----------------------
`--host-branch`                    |            | Branch which will host the injected commit(s)
`--host-before`                    |            | Commit which will become the ancestor of the injected commits
`--host-after`                     |            | Commit which will become the decendent of the injected commits
`--branch`                         |            | Identifies the branch which will be injected
`--single`<br>`--donor-single`     |            | Identifies the single commit which will be transposed
`--range`<br>`--donor-range`       |            | Identifies the contiguous set of commits which will be injected
`--range-start`<br>`--donor-start` |            | Identifies the first commit of the contiguous set of commits which will be injected
`--range-end`<br>`--donor-end`     |            | Identifies the last commit of the contiguous set of commits which will be injected
`--multiple`<br>`--donor-multiple` |            | Identifies the set of commits (not guaranteed to be continguous) which will be transposed, order which passed used to determine order in which they are injected.<br>***Input must be comma seperated and without spaces*** 

