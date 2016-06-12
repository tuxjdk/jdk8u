# TuxJDK upstream sources

## WHAT
* copy of `jdk8u` source code
* no modifications made
* no patches applied
* no original commit history is stored
* only tags relevant for the `tuxjdk` are commited and tagged

## WHY
* to simplify automation of `tuxjdk`-related tasks
* original OpenJDK commit history is not relevant for the `tuxjdk` project 

## HOW
```bash
# tag we already have:
CURRENT_TAG='jdk8u92-b14'
# tag we want to add:
TAG='jdk8u112-b00'
# cloning the upstream sources:
hg clone 'http://hg.openjdk.java.net/jdk8u/jdk8u'
cd 'jdk8u'
bash 'get_source.sh'
# cloning the git repo and merging:
git clone --no-checkout 'https://github.com/tuxjdk/jdk8u.git' 'git'
mv 'git/.git' .
rm -rf 'git'
# checking if repos are playing along:
git checkout -f
bash ./common/bin/hgforest.sh checkout "$CURRENT_TAG"
# status should not find any changes: 
git status
# now add new tag:
bash ./common/bin/hgforest.sh checkout "$TAG"
git add '*'
git commit -m "$TAG"
git tag "$TAG"
git push --tags
```