# Branch making exercise

```
1. Make a new folder called `Patronus`
2. Make a new git repo inside the folder (make sure you're not in an existing repo)
3. Create a new file called `patronus.txt` (leave it empty for now)
4. Add and commit the empty file, with the message "add empty patronus file"
5. Immediately make a new branch called `harry` and another branch called `snape` (both based on the master branch)
6. Move to the `harry` branch using the "new" command to change branches.
7. In the `patronus.txt` file, add the following:         
```    
HARRY'S PATRONUS
 
 /|       |\
`__\\       //__'
 ||      ||
\__`\     |'__/
 `_\\   //_'
 _.,:---;,._
 \_:     :_/
   |@. .@|
	 |     |
   ,\.-./ \
   ;;`-'   `---__________-----.-.
   ;;;                         \_\
   ';;;                         |
    ;    |                      ;
     \   \     \        |      /
      \_, \    /        \     |\
        |';|  |,,,,,,,,/ \    \ \_
        |  |  |           \   /   |
        \  \  |           |  / \  |
         | || |           | |   | |
         | || |           | |   | |
         | || |           | |   | |
         |_||_|           |_|   |_|
	      /_//_/           /_/   /_/
    ```
```     
8. Add and commit the changes, with the commit message "add harry's stag patronus"
9. Move over to the `snape` branch using the "older" command to change branches.
10.  Put the following text in  the `patronus.txt` file:         
```    
SNAPE'S PATRONUS
'''
												.     _,
                       |`\__/ /
                       \  . .(
                        | __T|
                       /   |
          _.---======='    |
         //               {}
        `|      ,   ,     {}
         \      /___;    ,'
          ) ,-;`    `\  //
         | / (        ;||
         ||`\\        |||
         ||  \\       |||
         )\   )\      )||
         `"   `"      `""
'''
11. Add and commit the changes on the `snape` branch with the commit message "add snape's doe patronus"
12. Next, create a new branch based upon the `snape` branch called `lily`
13. Move to the `lily` branch
14. Edit the `patronus.txt` file so that it says `LILY'S PATRONUS` at the top instead of`SNAPE'S PATRONUS` (leave the doe ascii-art alone)
15. Add and commit the change with the message "add lily's doe patronus"
16. Run a git command to list all branches (you should see 4)
17. **Bonus:** delete the `snape` branch (poor Snape)
```

- terminal
    
    ➜  Git_Practice mkdir Patronus
    ➜  Git_Practice ls
    First_Folder  GitBranching  GitIgnoreDemo Patronus      Shopping
    ➜  Git_Practice cd Patronus
    ➜  Patronus git init
    힌트: Using 'master' as the name for the initial branch. This default branch name
    힌트: is subject to change. To configure the initial branch name to use in all
    힌트: of your new repositories, which will suppress this warning, call:
    힌트:
    힌트: 	git config --global init.defaultBranch <name>
    힌트:
    힌트: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    힌트: 'development'. The just-created branch can be renamed via this command:
    힌트:
    힌트: 	git branch -m <name>
    /Users/a/Git_Practice/Patronus/.git/ 안의 빈 깃 저장소를 다시 초기화했습니다
    ➜  Patronus git:(master) touch patronus.txt
    ➜  Patronus git:(master) ✗ git add patronus.txt
    ➜  Patronus git:(master) ✗ git status
    현재 브랜치 master
    
    아직 커밋이 없습니다
    
    커밋할 변경 사항:
    (스테이지 해제하려면 "git rm --cached <파일>..."을 사용하십시오)
    새 파일:       patronus.txt
    
    ➜  Patronus git:(master) ✗ git commit -m "add empty patronous file"
    [master (최상위-커밋) 3bc64fb] add empty patronous file
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 patronus.txt
    ➜  Patronus git:(master) git status
    현재 브랜치 master
    커밋할 사항 없음, 작업 폴더 깨끗함
    ➜  Patronus git:(master) pwd
    /Users/a/Git_Practice/Patronus
    ➜  Patronus git:(master) git branch harry
    ➜  Patronus git:(master) git branch snape
    ➜  Patronus git:(master) git branch
    ➜  Patronus git:(master) git switch harry
    'harry' 브랜치로 전환합니다
    ➜  Patronus git:(harry) git status
    현재 브랜치 harry
    커밋하도록 정하지 않은 변경 사항:
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    수정함:        patronus.txt
    
    커밋할 변경 사항을 추가하지 않았습니다 ("git add" 및/또는 "git commit -a"를
    사용하십시오)
    ➜  Patronus git:(harry) ✗ git add .
    ➜  Patronus git:(harry) ✗ git commit -m "add harry's stag patronus"
    [harry 4c40ca6] add harry's stag patronus
    1 file changed, 29 insertions(+)
    ➜  Patronus git:(harry) git status
    현재 브랜치 harry
    커밋할 사항 없음, 작업 폴더 깨끗함
    ➜  Patronus git:(harry) git checkout snape
    'snape' 브랜치로 전환합니다
    ➜  Patronus git:(snape) git status
    현재 브랜치 snape
    커밋하도록 정하지 않은 변경 사항:
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    수정함:        patronus.txt
    
    커밋할 변경 사항을 추가하지 않았습니다 ("git add" 및/또는 "git commit -a"를
    사용하십시오)
    ➜  Patronus git:(snape) ✗ git add .
    ➜  Patronus git:(snape) ✗ git commit -m "add snape's doe patronus"
    [snape 8df6d85] add snape's doe patronus
    1 file changed, 19 insertions(+)
    ➜  Patronus git:(snape) git branch lily
    ➜  Patronus git:(snape) git switch lily
    'lily' 브랜치로 전환합니다
    ➜  Patronus git:(lily) git status
    현재 브랜치 lily
    커밋하도록 정하지 않은 변경 사항:
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    수정함:        patronus.txt
    
    커밋할 변경 사항을 추가하지 않았습니다 ("git add" 및/또는 "git commit -a"를
    사용하십시오)
    ➜  Patronus git:(lily) ✗ git add .
    ➜  Patronus git:(lily) ✗ git commit -m "add lily's doe patronus"
    [lily 0cf9b4f] add lily's doe patronus
    1 file changed, 1 insertion(+), 1 deletion(-)
    ➜  Patronus git:(lily) git branch
    ➜  Patronus git:(lily) git branch -d snape
    snape 브랜치 삭제 (과거 8df6d85).
    ➜  Patronus git:(lily) git branch
    ➜  Patronus git:(lily)