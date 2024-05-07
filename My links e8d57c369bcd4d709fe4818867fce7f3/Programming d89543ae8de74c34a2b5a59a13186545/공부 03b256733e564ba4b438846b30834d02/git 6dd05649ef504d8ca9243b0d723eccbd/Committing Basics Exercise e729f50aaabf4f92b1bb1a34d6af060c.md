# Committing Basics Exercise

1. Create a new folder called `Shopping`
2. Initialize a new git repo inside of the Shopping folder (make sure you’re not already inside of a Git repo!)
3. Make a new file called `yard.txt`
4. Make another new file called `groceries.txt`
5. Make a commit that includes both empty files. The message should e “create yard and groceries lists”
6. in the `yard.txt` file, add the following changes
    
    ```
    - 2 bags of potting soil
    - 1 bag of worm castings
    ```
    
7. in the `groceries.txt` file, add the following
    
    ```
    - 6 shallots
    - 1 fennel bulb
    ```
    
8. make a new commit, including ONLY the change from the `groceries.txt` file. The commit message should be “add ingredients for tomato soup”
9. Make a second commit including ONLY the changes to the `yard.txt` file. It should have the commit message “add items needed for garden box”
10. Next up, add the following line to the end of `yard.txt`.
    
    ```
    - couple of seed patatos
    ```
    
11. In the `yard.txt` file, change the first line so that it says “3 bags of potting soil” Instead of “2 bags of potting soil”
    
    ```
    - 3 bags of potting soil
    - 1 bag of worm castings
    ```
    
12. Makes a commit that includes the changes to BOTH files. The message should read “add items needed to grow potatoes”
13. Use a Git command to display a list of the commits. You should see 4!
- terminal
    
    Last login: Mon Sep 4 22:36:42 on ttys000
    ➜ ~ pwd
    /Users/a
    ➜ ~ ls
    
    Applications Documents Git_Practice Movies
    Desktop Downloads Library Music
    ➜ ~ cd Git_Practice/First_Folder
    ➜ First_Folder git:(main) ls
    
    Chapter1.txt character.txt outline.txt
    ➜ First_Folder git:(main) pwd
    /Users/a/Git_Practice/First_Folder
    ➜ First_Folder git:(main) cd..
    
    zsh: command not found: cd..
    ➜ First_Folder git:(main) cd ..
    ➜ Git_Practice pwd
    /Users/a/Git_Practice
    ➜ Git_Practice mkdir Shopping
    ➜ Git_Practice cd Shopping
    ➜ Shopping git init
    
    `NodeTest
    Pictures`
    
    `Public
    gallery-soma`
    
    힌트:
    ame
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    /Users/a/Git_Practice/Shopping/.git/ 안의 빈 깃 저장소를 다시 초기화했습니다
    ➜ Shopping git:(master) pwd
    
    /Users/a/Git_Practice/Shopping
    ➜ Shopping git:(master) ls
    ➜ Shopping git:(master) ls -a
    . .. .git
    
    ➜ Shopping git:(master) rm -rf .git
    ➜ Shopping git status
    fatal: (현재 폴더 또는 상위 폴더 중 일부가) 깃 저장소가 아닙니다: .git
    ➜ Shopping cd ..
    ➜ Git_Practice git status
    fatal: (현재 폴더 또는 상위 폴더 중 일부가) 깃 저장소가 아닙니다: .git
    ➜ Git_Practice cd ..
    ➜ ~ git status
    fatal: (현재 폴더 또는 상위 폴더 중 일부가) 깃 저장소가 아닙니다: .git
    ➜ ~ cd Git_Practice
    ➜ Git_Practice ls
    First_Folder Shopping
    ➜ Git_Practice cd Shopping
    ➜ Shopping git init
    힌트: Using 'master' as the name for the initial branch. This default branch n
    ame
    
    `Using 'master' as the name for the initial branch. This default branch n`
    
    `is subject to change. To configure the initial branch name to use in all
    of your new repositories, which will suppress this warning, call:`
    
    `git config --global init.defaultBranch <name>`
    
    `Names commonly chosen instead of 'master' are 'main', 'trunk' and
    'development'. The just-created branch can be renamed via this command:`
    
    `git branch -m <name>`
    
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    힌트:
    /Users/a/Git_Practice/Shopping/.git/ 안의 빈 깃 저장소를 다시 초기화했습니다
    ➜ Shopping git:(master) got statis
    
    zsh: command not found: got
    ➜ Shopping git:(master) git status
    현재 브랜치 master
    
    아직 커밋이 없습니다
    
    커밋할 사항 없음 (파일을 만들거나 복사하고 "git add"를 사용하면 추적합니다)
    ➜ Shopping git:(master) touch yard.txt
    ➜ Shopping git:(master) ✗ touch groceries.txt
    ➜ Shopping git:(master) ✗ git add .
    
    ➜ Shopping git:(master) ✗ git status
    현재 브랜치 master
    
    아직 커밋이 없습니다
    
    커밋할 변경 사항:
    (스테이지 해제하려면 "git rm --cached <파일>..."을 사용하십시오)
    
    새 파일: groceries.txt
    새 파일: yard.txt
    
    ➜ Shopping git:(master) ✗ git commit -m "create tard and groceries lists"
    [master (최상위-커밋) 0cfeb7a] create tard and groceries lists
    
    ```
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 groceries.txt
     create mode 100644 yard.txt
    
    ```
    
    ➜ Shopping git:(master) git status
    현재 브랜치 master
    커밋할 사항 없음, 작업 폴더 깨끗함
    ➜ Shopping git:(master) git status
    현재 브랜치 master
    
    커밋하도록 정하지 않은 변경 사항:
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    
    - 수정함: groceries.txt
    - 수정함: yard.txt
        
        커밋할 변경 사항을 추가하지 않았습니다 ("git add" 및/또는 "git commit -a"를
        사용하십시오)
        ➜ Shopping git:(master) ✗ git add groceries.txt
        ➜ Shopping git:(master) ✗ git status
        
        현재 브랜치 master
        
    
    `is subject to change. To configure the initial branch name to use in all
    of your new repositories, which will suppress this warning, call:`
    
    `git config --global init.defaultBranch <name>`
    
    `Names commonly chosen instead of 'master' are 'main', 'trunk' and
    'development'. The just-created branch can be renamed via this command:`
    
    `git branch -m <name>`
    
    커밋할 변경 사항:
    (use "git restore --staged <file>..." to unstage)
    
    수정함: groceries.txt
    
    커밋하도록 정하지 않은 변경 사항:
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    
    수정함: yard.txt
    
    ➜ Shopping git:(master) ✗ git commit -m "add ingrediens for tomato soup"
    [master 2b4d519] add ingrediens for tomato soup
    
    1 file changed, 2 insertions(+)
    ➜ Shopping git:(master) ✗ git status
    현재 브랜치 master
    커밋하도록 정하지 않은 변경 사항:
    
    (무엇을 커밋할지 바꾸려면 "git add <파일>..."을 사용하십시오)
    (use "git restore <file>..." to discard changes in working directory)
    
    수정함: yard.txt
    
    ```
    commit 444b6921fbd72953b0e3517a8a6640f2c8b1ac54 (HEAD -> master)
    Author: Lukas Park <nubddak3@gmail.com>
    Date:   Tue Sep 5 09:38:42 2023 +0900
    
    ```
    
    ```
        add items needed to grow potatoes
    
    ```
    
    ```
    commit 4c798e1e24646250c5b5c029e0d523737c1c0e0e
    Author: Lukas Park <nubddak3@gmail.com>
    Date:   Tue Sep 5 09:36:17 2023 +0900
    
    ```
    
    ```
        add itms needed for garden box
    
    ```
    
    ```
    commit 2b4d519991b9cea18808447faaac2e5483b18089
    Author: Lukas Park <nubddak3@gmail.com>
    Date:   Tue Sep 5 09:35:50 2023 +0900
    
    ```
    
    ```
        add ingrediens for tomato soup
    
    ```
    
    ```
    commit 0cfeb7a2f20587781c0b774c6b2e65d42aec9bd6
    Author: Lukas Park <nubddak3@gmail.com>
    Date:   Tue Sep 5 09:33:15 2023 +0900
    
    ```
    
    ```
        create tard and groceries lists
    (END)
    
    ```