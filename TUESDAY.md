
# Choose what to save and reuse
### Store                 What it holds                         How it is used
    Download cache        CodeQL bundle archive                 Verify, extract and check its version
    Artifact              Build: application.tgz                

It is possible to hash the manifest or package.json. Retrieve it later and if a hash is partially correct, the pipeline will simply add the missing packages.

## Cache lookup
Within each accessible branch, stop at the first matching key

Priority:
Exact key > key prefix > restore keys > Next step


### Finding a cache does not verify its contents
Verify the requested CodeQL archive, extract it and check its version every time 

Cache lookup: 