# Brainlife > Datalad export test repo

This repository exists to demonstrate a possible way to expose Brainlife's published datasets through datalad.

On this repo, you find all datasets published on Brainlife under [Open Diffusion Data Derivatives](https://brainlife.io/pub/5a0f0fad2c214c9ba8624376). In order to download this dataset via Datalad, you can do the following.

1) [Install Datalad](http://docs.datalad.org/en/latest/gettingstarted.html)

2) [Install Brainlife CLI](https://brainlife.io/docs/cli/install/) to issue jwt token

3) Make sure you have Brainlife account, and you've agreed to all data access agreements required to download O3D datasets. Easiest way to do this to go here > https://brainlife.io/pub/5a0f0fad2c214c9ba8624376#5a050966eec2b300611abff2 and click "Download" button at the top. Check all checkboxes when presented.

4) Issue local jwt token

```
$ bl login --ttl 30
username: ...
password: ...
```

5) Install the test datalad repo

```
datalad install https://github.com/soichih/datalad-test.git
```

6) To download datasets from brainlife.io, git-annex needs to access the jwt token issued by "bl login".

```
cd datalad-test
git config annex.http-headers-command 'echo "Authorization: Bearer $(cat ~/.config/brainlife.io/.jwt)"'
```

7) Now you can *download*(datalad get) Brainlife datasets by..

```
datalad get release-2/sub-0001/run-1
```

So on..

# TODOs..

1) All Brainlife datasets are stored in tar balls. Is there a way to auto-untar when datalad *get* them?
2) Is there way to store the .git/config on the repo so that user doesn't have to do step 6 above?
3) Brainlife provides full provenance and dataset metadata. Right now I am ignoring this when I setup the Datalad repo. How can I store this on datalad? Here is an example provenance.json > https://brainlife.io/api/warehouse/dataset/prov/5c0bdef7f6f108004b490dc0
4) This works great for publication. Should I allow user to download dataset directly from brainlife *project* also? (this is something brainlife team needs to discuss)



