---
Created by: Shudipto Trafder
Created time: 2024-04-15T12:03
Last edited by: Shudipto Trafder
Last edited time: 2024-04-15T12:04
tags:
  - git
---
### **Removing sensitive files and their commits from Git history**

To remove sensitive files and their commit history in Git, follow these series of steps to rewrite and cleanse the repository's history.

1. **Backup your repository**: Before making any significant changes, it's good practice to create a backup of your repository. You can do this by simply cloning it to a different location on your machine or by making a zip archive.
2. **Use the** `**filter-branch**` **command:** To remove a specific file from the entire history, you can use the `filter-branch` command. Here's how:

```Python
git·filter-branch·--force·--index-filter·"git·rm·--cached·--ignore-unmatch·PATH-TO-YOUR-FILE"·--prune-empty·--tag-name-filter·cat·--·--all
```

Command to rewrite the history of the repository

This command rewrites the entire history of the repository to remove references to the specified file. Here's a breakdown:  
•  
`--force`: Ensures the command runs even if the repository seems to be already filtered.  
•  
`--index-filter`: Rewrites the staging area (or `index`). In this case, it uses the `git rm` command to remove a specific file.  
◦  
`--cached`: Tells `git rm` to untrack the file but also keep it in your working directory.  
◦  
`--ignore-unmatch`: This ensures that the command doesn't fail if the file is absent in some commits.  
•  
`PATH-TO-YOUR-FILE`: This placeholder should be replaced with the actual path to the file you want to remove.  
•  
`--prune-empty`: Removes commits that become empty as a result (i.e., commits that only included changes related to the removed file).  
•  
`--tag-name-filter cat`: Rewrites tags to point to the new commits resulting from the filtered branch. The `cat` command simply updates the tags.  
•  
`-- --all`: Applies the filter to all refs in the repository, including branches and tags. The extra `--` separates the command from `git filter-branch` options`.`  
1.  
**Garbage collection**: After the above step, the commits with the sensitive files are disassociated but still present. To remove these old commits, run:

```Python
git·for-each-ref·--format="%(refname)"·refs/original/·|·xargs·-I·{}·git·update-ref·-d·{}
```

Command to list the references and then delete them

> This command lists all reference names (like branches and tags) under refs/original/ and then deletes each of those references from the Git repository.

Next, run the garbage collector:

```Python
git gc --prune=now

git·gc·--aggressive·--prune=now
```

Commands to prune the non-referenced objects and optimize the repository

The first command immediately prunes objects not referenced by any commit, and the second aggressively optimizes the repository to further reduce its size after the sensitive data removal.  
1.  
**Push the changes to the remote repository**: If you have pushed the sensitive file to a remote repository, you need to force push the changes to overwrite the history:

```Python
git push origin --force --all
```

Command to forcefully push branches to remote repository

> This command forcefully pushes all branches to the remote repository origin, overwriting its history to reflect the changes made locally, which includes the removal of the sensitive files from the commit history.

If you have tags, you'll also want to push them:

```Python
git push origin --force --tags
```

Command to forcefully push tags to remote repository

This command forcefully pushes all tags to the remote repository "origin," ensuring that the tags' history on the remote aligns with the local modifications made, such as the removal of sensitive files from the commit history.