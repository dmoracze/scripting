### Downloading the Mother of All Unification Studies (MOUS) dataset onto Biowulf

[Donders Institute Repository Source](https://data.donders.ru.nl/collections/di/dccn/DSC_3011020.09_236?0)

#### Instructions for download

1. Click the *Request Access* link on the repository's main page.

2. Log in with your ORCID to obtain a ursername and password

3. Generate a swarm file of download commands using the bash script `urlgen`

```
./urlgen folders.txt files.txt https://data.donders.ru.nl/collections/di/dccn/DSC_3011020.09_236?0 <username> <password> /path/to/download_destination wget_commands.txt
```

   `folders.txt` and `files.txt` contain the names of the directories and files within the repository, respectively
   `urlgen` will produce the wget_commands.txt file which contains many wget commands which can be used by `swarm` to download the files in parallel
    The commands within the resulting file should look like:

```bash
wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/code/" --user=<username> --password=<password> -P /data/DSST_dua/donders/MOUS
wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/sourcedata/" --user=<username> --password=<password> -P /data/DSST_dua/donders/MOUS
wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/stimuli/" --user=<username> --password=<password> -P /data/DSST_dua/donders/MOUS
```
4. Use `swarm` to parallelize the downloads:

```bash
swarm -f /path/to/wget_commands.txt --time 48:00:00 --logdir /path/to/logs --job-name MOUS
```

5. Once queued, you can check the status of the download using:

```bash
squeue -u <username>
```

6. Once the download is complete, the files will be stored in:
		
```bash
/path/to/download_destination/webdav.data.donders.ru.nl/dccn/DSC_3011020.09_236_v1
```
