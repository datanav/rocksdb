
This repository contains forked version of rocksdb with a couple of sesam-specific tweaks.

To update to a new version of rocksdb, do the following:

1. In a webbrowser, go to https://github.com/datanav/rocksdb and click the "Sync fork"->"Update branch"-button.
2. In your local checkout of datanav/rocksdb, run this command:
   git fetch --tags upstream

3. In your local checkout of datanav/rocksdb, run the command:
     git push --tags --dry-run
   If the resulting new tags look reasonable, run this command:
     git push --tags

4. Checkout the current "sesam_from_tag_<version>" branch. Look at the "git clone" command in this file for the correct
   branch-name: https://github.com/datanav/lake/blob/master/docker/base/rocksdb.sh
   Example: git checkout sesam_from_tag_v6.20.3

5. Make a note of the commit(s) we have made to the "sesam_from_tag_<version>" branch:
     git log
   (The first commit should be called something like "IS-7880: don't write OPTIONS file when creating or deleting columnfamilies")

6. Check out the release you want to update to.
   This will normally be the latest release listed on https://github.com/facebook/rocksdb/releases
   Example: git checkout v6.22.1

7. Create a new "sesam_from_tag_<version>" branch.
   Example: git checkout -b sesam_from_tag_v6.22.1

8. Cherry-pick the commits you found in step 5:
   Example: git cherry-pick 127536003ef693ecb64f21d437965bf58eb7e2d3

9. Push your changes:
   git push
   (You may have to add a '--set-upstream' parameter, but if so
    git will tell you).

10. Create a pull-request in the "datanav/lake" repo with an updated "sesam_from_tag_<version>" in this file:
    https://github.com/datanav/lake/blob/master/docker/base/rocksdb.sh
