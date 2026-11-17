
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

# Images
It is possible to create custom runners tailored for example to specific frameworks, programming languages and use cases.

These images must be maintained by ourselves.

However there are some steps to take beforehand:

1. Compare which setup steps were avoided and which still ran
2. Compare total runner time and cost
3. Include the cost of creating and storing images
4. Plan updates and a way to return a previous image
5. During cleanup, remove only resources created for this course
6. Still waiting, record pending.


# Avoid work before speeditn it up
Choose which events and changes need a workflow run
Download only the files a job needs
Independent chekcs at the same time
Set time limits so a stuck job cnanot run forever
Measure the problem before choosing a larger runner  

# Checkout settings also protect the job
Submodules link repositories; Git LFS manages large-file downloads

# Sparce checkout: get only selected files
The working tree is your local copy; sparce checkout limits which files appear

The versioning system only requests the required folder/ data required for the change to be made.

If .github/workflow is needed, the traditional checkout would retrieve the entire project, but now instead, it simply retrieves the .github/workflow/

| .github/workflow +
| folder1 -
| folder2 -
| thingA -
| thingB -

Cone-mode: false equals I want nothing but that one thing
Cone-mode: true equals I want everything except that one thing 

Zizmore is a free alternative to GHAS, ideally used for your own envrionments

# Save outputs as seperate artifacts 
## Option 1, upload a zip you already created
Archive: false uploads one file; skip-decompress: true leaves it zipped 

- uses: actions/upload-artifact@v7.0.2
  with:
    path: packages/linux.zip
    archive: /false
    if-no-files-found: error
- uses: actions/download-artifact@v8.0.2
  with:
    name: linux.zip
    skip-decompress: true

## Option 2, give each upload a different name
skip-decompress: false extracts the selected ZIP into files

- uses: actions/upload-artifact@v7.0.2
  with:
    name: test-reports
    path: reports/
    archive: /false
    if-no-files-fo/und: error
- uses: actions/download-artifact@v8.0.2
  with:
    name: test-reports
    skip-decompress: false

