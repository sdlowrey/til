# Working With Git Remotes

## Add another remote to a repository

Say you are working on a project and want to be able to push to another user's repo.

```
$ git remote -v
origin	ssh://git@rainsail.com/devops/fun.git (fetch)
origin	ssh://git@rainsail.com/devops/fun.git (push)

$ git remote add sl git@github.com:sdlowrey/fun.git

$ git remote -v
origin	ssh://git@rainsail.com/devops/fun.git (fetch)
origin	ssh://git@rainsail.com/devops/fun.git (push)
sl	git@github.com:sdlowrey/fun.git (fetch)
sl	git@github.com:sdlowrey/fun.git (push)
```
