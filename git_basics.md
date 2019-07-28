# Git notes from datacamp

Basic commands:

```
git status
git add
git commit -m "Message about the commit"
git log
git diff or git diff path/to/file
```

* Each commit has its own unique hash code (40 char) that is used by git to check for changes in the contents of the file
* Organization of a commit contains a tree and blobs
* One can identify a hash with its first 8 characters

```
git show HASH_NUMBER
```

This gives an output as in:

```
commit 472e96ae5d35e8176fad49ab8645f300960f28ac
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Added summary report file.

diff --git a/report.md b/report.md
new file mode 100644
index 0000000..8b90951
--- /dev/null
+++ b/report.md
@@ -0,0 +1,5 @@
+# Northwestern Dental Surgeries 2017-18
+
+TODO: write executive summary.
+
+TODO: include link to raw data.
```

With + for lines that were added, - for lines that were eliminated.

* To show only the last commit details, one can use:

```
git show HEAD
```

To show the penultimate commit details,

```
git show HEAD~1
```

And so on (HEAD~2, HEAD~3,...)

* To show who made the last changes to a file and when it took place:

```
git annotate file
```

* To see the differences between two commits:

```
git diff abc123..def456
git diff HEAD~1..HEAD~3
```

Where the first shows the differences between abc123 def456 commits, while HEAD~1 and HEAD~3 the differences between the penultimate and three commits in the past.

## .gitignore
Always at the root of the repository, contains the file extensions and folders that should be ignored during version control.

* To clean the files that are not being tracked:

```
git clean -n
git clean -f
```

The first shows the files that are not being tracked, the second will permanently delete those files.

* Changing configurations of git:

```
git config --list --system
git config --list --global
git config --list --local
```

* `--system`: settings for every user in this machine
* `--global`: settings for every one of your projects
* `--local`: settings for one specific project

* To change the user email globally:

```
git config --global user.email rep@gmail.com
```
