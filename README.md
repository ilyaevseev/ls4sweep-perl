# ls4sweep readme #

* ls4sweep is a tool intended for use as helper for removing old backups.
* A sweeping policy consists of a set of records that contains the number of intervals or a periods in days to retain.
* It checks creation or modification time of given files and displays names of those when they don't match the policy.
* The output can then be passed to rm.

### Example ###

```
ls4sweep 3:1,2:3,2:10,2:30,3:90,5:365 *.zip
```

This means:

* keep daily ZIP-archives in current directory for last 3 days
* older than 3 days: keep 2 archives with 3-days delta
* older than 9 days ((3 * 1) + (2 * 3)): keep 2 archives with 10-days delta
* older than one month ((3 * 1) + (2 * 3) + (2 * 10)): keep 2 archives with monthly delta
* older than 3 months: keep 3 archives with 90-days delta
* older than one year: keep yearly archive for five years
* display filenames of all remaining stuff

ls4sweep output can be directly passed to the input of '| xargs -r /bin/rm -f' command:
```
ls4sweep 3:1,2:3,2:10,2:30,3:90,5:365 *.zip 2>sweep_errors.log | xargs -r /bin/rm -f 2>remove_errors.log
```

### Requirements ###

* Perl ;)