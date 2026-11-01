# FlameWill sticky disk

A directory whose contents stay between jobs, by key, on [FlameWill](https://flamewill.com) runners.

```yaml
- uses: FlameWill/sticky-disk@v1
  with:
    key: build-cache
    path: .cache/build
```

- The directory is a disk restored from the last save of this key in the same repository. A key never saved starts empty.
- When the job ends, the disk is saved if the job may write the repository's caches: a push, schedule or manual run of the default
  branch, or of a branch FlameWill names for the repository. Pull requests and other branches read it and may write to it during the
  job, but nothing they write is kept.
- Two jobs with the same key each start from the copy saved before they began; the last one to finish saves. Give each writing job
  its own key.
- Up to 5 per job, each up to 50 GB. A key not saved for 7 days is deleted.
- Mount it before anything writes to the path: the path must be empty or not exist.

Off FlameWill, the path is created empty and nothing is kept.
