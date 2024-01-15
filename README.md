## Using the kotlin_fmt hook

```
$ :) git add src/Hello.kt
$ :) git commit -s -m 'Add Hello.kt'
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

```
$ :( gd src/Hello.kt
diff --git a/src/Hello.kt b/src/Hello.kt
index 51a1d56718..0b69e213e7 100644
--- a/src/Hello.kt
+++ b/src/Hello.kt
@@ -1,3 +1,3 @@
-fun main(args : Array<String>) {
+fun main(args: Array<String>) {
     println("Hello, World!")
 }
```

```
$ :) git add src/Hello.kt
$ :) git commit -s -m 'Add Hello.kt'
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
[ktlint-test1 eb3ddbf909] Add Hello.kt
 1 file changed, 3 insertions(+)
 create mode 100644 src/Hello.kt
```
