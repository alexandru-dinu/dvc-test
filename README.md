# DVC test

Testing [Data Version Control](https://dvc.org/doc/start/data-versioning).

## Getting started

Initialize `dvc` repo.
```
$ dvc init
```

Get sample data (or simply add some existent files)
```
$ mkdir data
$ dvc get https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
```

Let `dvc` know that this is a large file (e.g. dataset, model etc.)
```
dvc add data/data.xml
```

Now, `data/data.xml.dvc` is created:
```
outs:
- md5: a304afb96060aad90176268345e10355
  size: 37891850
  path: data.xml
```

And the original, raw data is ignored:
```
$ cat data/.gitignore
/data.xml
```

These two files can now be committed:
```
$ git add data/data.xml.dvc data/.gitignore
$ git commit -m "Run 'dvc get' on sample data, add .dvc file."
```


## Making changes to raw data

```
$ vim data/data.xml # make some changes
$ dvc add data/data.xml
$ git add data/data.xml.dvc
```

This results in a modified hash in the `data.xml.dvc` file, and an updated `.dvc/cache`, now containing both file versions,
identified by their hashes.
