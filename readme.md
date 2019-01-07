# Git Tools
Number of useful tools which are designed to simplify rather complex git operations
Mostly wrappers over `git-rebase`
## git-transpose
Moves a branch to a new parent
### Usage
 Command | Description 
---------|------------
`git transpose <base branch> <moving branch>` | Transposes <moving branch> onto head of <base branch>
`git transpose <base branch> <moving branch> <moving commit>` | Transposes <moving commit> onto head of <base branch>
`git transpose <base branch> <moving branch> <first moving commit>...<last moving commit>` | Transposes range of commits onto head of <base branch>
`git transpose <base branch> --onto <base commit> <moving branch>` | Transposes `<moving branch>` base onto `<base commit>` of `<base branch>`
`git transpose <base branch> --onto <base commit> <new branch> <moving branch> <moving commit>` | Creates new branch `<new branch>` base onto `<base commit>` of `<base branch>` with <moving commit>
`git transpose <base branch> --onto <base commit> --inject <moving commit>` | Injects `<moving commit>` into `<base branch>` such the it succeeds `<base commit>`
`git transpose <base branch> --onto <base commit> --inject <moving branch>` | Injects `<moving branch>` history into `<base branch>` such that is succeeds `<base commit>`
`git transpose <base branch> --onto <base commit> --inject <first moving commit>...<last moving commit>` | Inclusively injects commits within the range into `<base branch>` such that is succeeds `<base commit>`

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

### Examples
#### Move branch
```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```
`git transpose master slave`
```
A - B - C - D   (master)
             \
	          E - F - G  (slave)
```

*Onto a specific commit*

```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```
`git transpose master --onto C slave`
```
A - B - C - D   (master)
         \
	      E - F - G  (slave)
```

#### Move a commit
```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```
`git transpose master slave G`
```
A - B - C - D - G  (master)
    \
	 E - F         (slave)
```
If commit from middle of history
```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```
`git transpose master slave F`
```
A - B - C - D - F  (master)
    \
	 E - G         (slave)
```
*Onto specific commit*
```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```
`git transpose master --onto C slave G sub`
```
          G  (sub)
         /
A - B - C - D   (master)
    \
	 E - F  (slave)
```

#### Move a range of commits
```
A - B - C - D   (master)
     \
      E - F - G  (slave)
```
git transpose master slave F...G
```
A - B - C - D - F - G   (master)
     \
      E (slave)
```

```
A - B - C - D   (master)
     \
	   E - F - G  (slave)
```
git transpose master slave E...F

```
A - B - C - D - E - F  (master)
     \
	   G (slave)
```

#### Move branch onto specific commit
```
A - B - C - D   (master)
    \
	 E - F - G  (slave)
```

`git transpose master C -- slave`

```
A - B - C - D   (master)
         \
	      E - F - G  (slave)
```

#### Create branch at point


```
A - B - C - D - E - F - G (master)
```
`git transpose master --split D child`
```
A - B - C - D   (master)
             \
              E - F - G (child)
```

```
A - B - C - D - E - F - G (master)
```
`git transpose master --onto C --split D child`
```
A - B - C - D   (master)
		 \
		  E - F - G (child)
```
