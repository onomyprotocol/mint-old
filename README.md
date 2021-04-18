# mint
Onomy Protocol Mint Module

The Onomy Protocol Mint module implements the staking inflation logic outlined here: 
https://docs.onomy.io/proof-of-stake-staking/validator-staking

The Mint module is a subtree fork of the x/mint directory of Comsos-SDK

Because this is a subtree fork, there are special instructions for making changes to your repositories

When you're dealing with your own local and remote repositories, you can use normal git commands. Make sure to do this on the master branch (or some other branch, if you'd like) and not the upstream-skin branch, which should only ever contain commits from the upstream project.
```
git checkout master
echo "My Mint" > README
git add README
git commit -m "Added README"
git push
```
Receiving upstream commits

When you're dealing with the upstream repository, you will have to use a mix of git and git subtree commands. To get new filtered commits, we need to do it in three stages.

In the first stage, we'll update upstream-master to the current version of the Cosmos-SDK repository.

git checkout upstream-master
git pull

This should pull down new commits, if there are any.

Next, we will update upstream-mint with the new filtered version of the commits. Since git subtree ensures that commit hashes will be the same, this should be a clean process. Note that you want to run these commands while still on the upstream-master branch.
```
git subtree split --prefix=x/mint \
--onto upstream-mint -b upstream-mint
```
With upstream-mint now updated, you can update your master branch as you see fit (either by merging or rebasing).
```
git checkout master
git rebase upstream-skin
```
Note that the Cosmos-SDK repository is gigantic, and the git subtree commands will take quite a bit of time to filter through all that history -- and since you're regenerating the split subtree each time you interact with the remote repository, it's quite an expensive operation. I'm not sure if this can be sped up.

This blog post goes into some more detail on the commands above.
https://web.archive.org/web/20131123125622/http://blog.charlescy.com/blog/2013/08/17/git-subtree-tutorial/

Also see the git-subtree docs for even more detail.
https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt
