*** How to download the Mother of All Unification Studies (MOUS) dataset from Donders Instutute Repository ***

- There are two files you need: folders.txt and files.txt
- To download the files onto Biowulf, you must use a Swarm
- On the Donders Institute Website (https://data.donders.ru.nl/collections/di/dccn/DSC_3011020.09_236?0), acquire your Data Access Password
- Using the script "urlgen" run the following in a bash shell:

		./urlgen folders.txt files.txt https://data.donders.ru.nl/collections/di/dccn/DSC_3011020.09_236?0 <username> <password> /path/to/download_destination wget_commands.txt


- This command will produce the wget_commands.txt file which contains many wget commands which can be used by the Biowulf Swarm to download the files in parralel
- The contents look like:

		wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/code/" --user=0000-0002-5836-9244@orcid.org --password=48332225 -P /data/NDAR/donders/MOUS
		wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/sourcedata/" --user=0000-0002-5836-9244@orcid.org --password=48332225 -P /data/NDAR/donders/MOUS
		wget -r -R "index.html*" --no-parent "https://webdav.data.donders.ru.nl:443/dccn/DSC_3011020.09_236:v1/stimuli/" --user=0000-0002-5836-9244@orcid.org --password=48332225 -P /data/NDAR/donders/MOUS

- To run the Swarm, use the following command on Biowulf:

		swarm -f /path/to/wget_commands.txt --time 48:00:00 --logdir /path/to/logs --job-name MOUS

- Once queued, you can check the status of the download using:

		squeue -u <username>

- Once the download is complete, the files will be stored in:
		
		/path/to/download_destination/webdav.data.donders.ru.nl/dccn/DSC_3011020.09_236_v1