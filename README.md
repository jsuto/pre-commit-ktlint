## Prerequisites

### Install pre-commit

See https://pre-commit.com/#install for details

### Install the pre-commit git hook

```
$ :) pre-commit install
pre-commit installed at .git/hooks/pre-commit
```

### Install ktlint

See https://github.com/pinterest/ktlint for details. On MacOS simply run:

```
brew install ktlint
```


## Installing the ktlint hook

Add the following to .pre-commit-config.yaml in the repo root, and commit the file.

```
---
repos:
  - repo: https://github.com/jsuto/pre-commit-ktlint
    rev: v0.0.2
    hooks:
      - id: ktlint_fmt
```

Or you may use the ktlint hook, see below the difference.


## Using the ktlint hook

Add a comment with incorrect formatting (missing space)

```
:) git diff src/Hello.kt
diff --git a/src/Hello.kt b/src/Hello.kt
index 0b69e213e7..5f8d7624d5 100644
--- a/src/Hello.kt
+++ b/src/Hello.kt
@@ -1,3 +1,4 @@
+//this is a comment
 fun main(args: Array<String>) {
     println("Hello, World!")
 }
```

Stage it, then try to commit

```
$ :) git add src/Hello.kt
$ :) git commit -s -m 'Added comment to Hello.kt'
check for added large files..............................................Passed
check for merge conflicts................................................Passed
check json...........................................(no files to check)Skipped
check yaml...........................................(no files to check)Skipped
detect aws credentials...................................................Passed
detect private key.......................................................Passed
fix end of files.........................................................Passed
fix python encoding pragma...........................(no files to check)Skipped
fix requirements.txt.................................(no files to check)Skipped
trim trailing whitespace.................................................Passed
Lint Dockerfiles.....................................(no files to check)Skipped
shellcheck...........................................(no files to check)Skipped
yamllint.............................................(no files to check)Skipped
Detect secrets...........................................................Passed
Terraform fmt........................................(no files to check)Skipped
Kotlin linter............................................................Failed
- hook id: ktlint
- exit code: 1

src/Hello.kt:1:1: Missing space after // (standard:comment-spacing)
18:24:20.868 [main] WARN com.pinterest.ktlint.cli.internal.KtlintCommandLine -- Lint has found errors than can be autocorrected using 'ktlint --format'

Summary error count (descending) by rule:
  standard:comment-spacing: 1

```


## Using the ktlint_fmt hook

Update Hello.kt with wrong indentation

```
$ :) gd src/Hello.kt
diff --git a/src/Hello.kt b/src/Hello.kt
index 0b69e213e7..02440433cc 100644
--- a/src/Hello.kt
+++ b/src/Hello.kt
@@ -1,3 +1,4 @@
 fun main(args: Array<String>) {
     println("Hello, World!")
+   println("Hello, Earth!")
 }
```

Stage it, then try to commit

```
$ :) git add src/Hello.kt
$ :) git commit -s -m 'Added hello Earth'
check for added large files..............................................Passed
check for merge conflicts................................................Passed
check json...........................................(no files to check)Skipped
check yaml...........................................(no files to check)Skipped
detect aws credentials...................................................Passed
detect private key.......................................................Passed
fix end of files.........................................................Passed
fix python encoding pragma...........................(no files to check)Skipped
fix requirements.txt.................................(no files to check)Skipped
trim trailing whitespace.................................................Passed
Lint Dockerfiles.....................................(no files to check)Skipped
shellcheck...........................................(no files to check)Skipped
yamllint.............................................(no files to check)Skipped
Detect secrets...........................................................Passed
Terraform fmt........................................(no files to check)Skipped
Kotlin linter............................................................Failed
- hook id: ktlint_fmt
- files were modified by this hook
```

Notice that the file has not been committed, and it has been fixed by ktlint

```
$ :( git status src/Hello.kt
On branch ktlint-test1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   src/Hello.kt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   src/Hello.kt


$ :) git diff src/Hello.kt
diff --git a/src/Hello.kt b/src/Hello.kt
index 02440433cc..6cbc86d44e 100644
--- a/src/Hello.kt
+++ b/src/Hello.kt
@@ -1,4 +1,4 @@
 fun main(args: Array<String>) {
     println("Hello, World!")
-   println("Hello, Earth!")
+    println("Hello, Earth!")
 }
```

Let's accept the modified file, and attempt to commit again.

```
$ :) git add src/Hello.kt
$ :) git commit -s -m 'Added hello Earth'
check for added large files..............................................Passed
check for merge conflicts................................................Passed
check json...........................................(no files to check)Skipped
check yaml...........................................(no files to check)Skipped
detect aws credentials...................................................Passed
detect private key.......................................................Passed
fix end of files.........................................................Passed
fix python encoding pragma...........................(no files to check)Skipped
fix requirements.txt.................................(no files to check)Skipped
trim trailing whitespace.................................................Passed
Lint Dockerfiles.....................................(no files to check)Skipped
shellcheck...........................................(no files to check)Skipped
yamllint.............................................(no files to check)Skipped
Detect secrets...........................................................Passed
Terraform fmt........................................(no files to check)Skipped
Kotlin linter............................................................Passed
[ktlint-test1 ca0f5d81cd] Added hello Earth
 1 file changed, 1 insertion(+)
```

This time the commit has been accepted and created

```
$ :) git show
commit ca0f5d81cdee65b1817ca3d1957d0e060f412eeb (HEAD -> ktlint-test1)
Author: Janos SUTO <sj@acts.hu>
Date:   Mon Jan 15 18:36:01 2024 +0100

    Added hello Earth

    Signed-off-by: Janos SUTO <sj@acts.hu>

diff --git a/src/Hello.kt b/src/Hello.kt
index 0b69e213e7..6cbc86d44e 100644
--- a/src/Hello.kt
+++ b/src/Hello.kt
@@ -1,3 +1,4 @@
 fun main(args: Array<String>) {
     println("Hello, World!")
+    println("Hello, Earth!")
 }
```
