# GitLab

## 1. SSH connection

```bash
ssh-keygen
cat id_rsa.pub
```

Then copy and paste the public key into the SSH Keys on the GitLab

## 2. Commend for GitLab

https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html

### git clone 

The **git clone command** copies an existing **Git repository**. This is sort of like SVN **checkout**, except the “working copy” is a full-fledged **Git repository**—it has its own history, manages its own files, and is a completely isolated environment from the original **repository**.

```bash
git clone git@git.ita.chalmers.se:xkong/test.git
```

### git push

The **git push command** is used to upload local repository content to a remote repository. **Pushing** is how you transfer commits from your local repository to a remote repo. It's the counterpart to **git** fetch , but whereas fetching imports commits to local branches, **pushing** exports commits to remote branches.

```bash
git push 
```

### git pull

```bash
git pull <REMOTE> <name-of-branch>
```

To work on an up-to-date copy of the project (it is important to do this every time you start working on a project), you `pull` to get all the changes made by users since the last time you cloned or pulled the project. Use `master` for the `` to get the main branch code, or the branch name of the branch you are currently working in.

When you clone a repository, `REMOTE` is typically `origin`. This is where the repository was cloned from, and it indicates the SSH or HTTPS URL of the repository on the remote server. `` is usually `master`, but it may be any existing branch. You can create additional named remotes and branches as necessary.

### create  a new project in GitLab web-page

Remember generate it and initial it with readme. 

## Personal access token

Setting -> Developer setting ->Personal access tokens-> Generate new token->Copy and paste