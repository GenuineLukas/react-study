# Git Diff Exercise

### Part 1:Setup

Please run the following commands from your terminal. Make sure you are not inside of a Git repo.

```
git clone https://github.com/Colt/git-diff-exercise
```

- Change into the newly created folder called `git-diff-exercise`. You will be on a branch called `current` by default.
- `Run git switch 1970s`
- You should now ave two branches that you can move between: current and 1970s. Each branch contains two files: `queent.txt` and `fleetwoodmac.txt`

### Part 2: The Diffs

1. Compare the difference between the `1970s` branch and the `current` branch across all files
2. Compare the difference between the `1970s` branch and the `current` branch but only for the queen.txt file.
3. Switch over to the `current` branch if you are no currently on it. Run a diff to com pare the current HEAD to the previous commit (the one with the message “replace John Deacon as Queen’s bassist”
4. While on the `current` branch, change the `queen.txt` file by replacing Adam lambert with your own name. Save the change. Add `queen.txt` to the staging area. DO NOT COMMIT YET!
5. Edit the `fleetwoodmac.txt` file, changing the lead singer from Stevie Nicks to Stevie Chicks (one of my chickens). Save the file, but do not stage it.
6. Run a diff that would reveal the unstaged changes in the working directory (you should see only the change to `fleetwoodmac.txt` printed out)
7. Run a diff that would reveal only the staged changes (you should only see the change to `queen.txt` printed out) 
8. Run a diff that prints all changes (staged and unstaged) since the prior commit (you should see both changes printed out)