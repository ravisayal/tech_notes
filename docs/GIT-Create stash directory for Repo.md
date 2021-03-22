# Create Stash directory at Repo Top 

```shell

REPO_TOP=`git rev-parse --show-toplevel`
cd "$REPO_TOP"
mkdir -p ../stash; git ls-files --others --exclude-standard -z |xargs -0 -t -I {} mv -i {} ../stash

```

