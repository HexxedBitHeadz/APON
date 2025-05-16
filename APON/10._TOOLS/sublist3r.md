**Sublist3r is a python tool designed to enumerate subdomains of websites using OSINT**

Usage
Short Form 	Long Form 	Description
-d 	--domain 	Domain name to enumerate subdomains of
-b 	--bruteforce 	Enable the subbrute bruteforce module
-p 	--ports 	Scan the found subdomains against specific tcp ports
-v 	--verbose 	Enable the verbose mode and display results in realtime
-t 	--threads 	Number of threads to use for subbrute bruteforce
-e 	--engines 	Specify a comma-separated list of search engines
-o 	--output 	Save the results to text file
-h 	--help 	show the help message and exit


To list all the basic options and switches use -h switch:

```bash
python sublist3r.py -h
```

To enumerate subdomains of specific domain:

``` bash
python sublist3r.py -d example.com
```

To enumerate subdomains of specific domain and show only subdomains which have open ports 80 and 443 :

```bash
python sublist3r.py -d example.com -p 80,443
```

To enumerate subdomains of specific domain and show the results in realtime:

```bash 
python sublist3r.py -v -d example.com
```

To enumerate subdomains and enable the bruteforce module:

```bash
python sublist3r.py -b -d example.com
```

To enumerate subdomains and use specific engines such Google, Yahoo and Virustotal engines

```bash
python sublist3r.py -e google,yahoo,virustotal -d example.com
```
