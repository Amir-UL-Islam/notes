- `-O` will saves the file as it is in current directory 
	- Like Here
	  `curl -O www.https://example.com/demo.txt` will download `demo.txt` file under current directory
- `-o` used when we want to rename file and save into specific location
	- Like Here
	  `curl -o /Users/amir/Downloads/example.txt www.https://example.com/demo.txt` will download `demo.txt` file under  this location `/Users/amir/Downloads` and save as `example.txt` 
- `-L` redirects the HTTP URL if a 300 error code occurs.
- `-C`  resumes a previous file transfer if it times out before completion.
### Download all 100 data files

```bash
curl -O https://s3.amazonaws.com/assets.datacamp.com/production/repositories/4180/datasets/files/datafile[001-100].txt
