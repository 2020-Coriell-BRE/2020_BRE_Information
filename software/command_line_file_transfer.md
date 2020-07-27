## Command Line Options for Transferring Files

Because MacOS Catalina is too secure

### Secure File Transfer Protocol (SFTP)

This logs you into the server, similarly to `ssh` so you can look around and navigate the filesystem, and allows to upload and download files. In addition to what I show below, there's a helpful list of commands at the link <https://www.uppmax.uu.se/support/user-guides/basic-sftp-commands/>

---

#### Logging In

To get started, log in to the server using `sftp` instead of `ssh`

```bash
### log in using sftp instead of ssh
sftp kkeith@10.1.105.13
```
#### Downloading

To transfer stuff from your local (personal) computer to the server, use the command `get`. This is what you'll primarily need to do for the rest of the experience.

```bash
### EXAMPLE: tranfer stuff from the server to your machine
# look around on the server
sftp> ls
data              rnaseq_practice
# go to the folder you want to grab stuff from
sftp> cd rnaseq_practice/data/fastqc
sftp> ls
ls
dac1_chr21_R1_fastqc.html  dac1_chr21_R1_fastqc.zip   dac1_chr21_R2_fastqc.html  dac1_chr21_R2_fastqc.zip   
dac2_chr21_R1_fastqc.html  dac2_chr21_R1_fastqc.zip   dac2_chr21_R2_fastqc.html  dac2_chr21_R2_fastqc.zip   
dac3_chr21_R1_fastqc.html  dac3_chr21_R1_fastqc.zip   dac3_chr21_R2_fastqc.html  dac3_chr21_R2_fastqc.zip   
siC1_chr21_R1_fastqc.html  siC1_chr21_R1_fastqc.zip   siC1_chr21_R2_fastqc.html  siC1_chr21_R2_fastqc.zip   
siC2_chr21_R1_fastqc.html  siC2_chr21_R1_fastqc.zip   siC2_chr21_R2_fastqc.html  siC2_chr21_R2_fastqc.zip   
siC3_chr21_R1_fastqc.html  siC3_chr21_R1_fastqc.zip   siC3_chr21_R2_fastqc.html  siC3_chr21_R2_fastqc.zip
# download all the html files
sftp> get *.html
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac1_chr21_R1_fastqc.html to dac1_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac1_chr21_R1_fastqc.html         100%  243KB  33.0MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac1_chr21_R2_fastqc.html to dac1_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac1_chr21_R2_fastqc.html         100%  238KB  42.4MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac2_chr21_R1_fastqc.html to dac2_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac2_chr21_R1_fastqc.html         100%  234KB  42.3MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac2_chr21_R2_fastqc.html to dac2_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac2_chr21_R2_fastqc.html         100%  232KB  46.3MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac3_chr21_R1_fastqc.html to dac3_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac3_chr21_R1_fastqc.html         100%  237KB  51.6MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/dac3_chr21_R2_fastqc.html to dac3_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/dac3_chr21_R2_fastqc.html         100%  234KB  53.7MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC1_chr21_R1_fastqc.html to siC1_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC1_chr21_R1_fastqc.html         100%  243KB  53.1MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC1_chr21_R2_fastqc.html to siC1_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC1_chr21_R2_fastqc.html         100%  234KB  55.8MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC2_chr21_R1_fastqc.html to siC2_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC2_chr21_R1_fastqc.html         100%  240KB  56.6MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC2_chr21_R2_fastqc.html to siC2_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC2_chr21_R2_fastqc.html         100%  233KB  59.4MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC3_chr21_R1_fastqc.html to siC3_chr21_R1_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC3_chr21_R1_fastqc.html         100%  236KB  60.9MB/s   00:00    
Fetching /home/kkeith/rnaseq_practice/data/fastqc/siC3_chr21_R2_fastqc.html to siC3_chr21_R2_fastqc.html
/home/kkeith/rnaseq_practice/data/fastqc/siC3_chr21_R2_fastqc.html         100%  233KB  63.4MB/s   00:00 
```

#### Uploading

To upload to the server from your local (personal) computer, use the command `put`.

```bash
### upload files to the server
### Generally, to run commands to see stuff on your local (personal computer), put an l in front fo the command
# check your local (personal computer) location 
sftp> lpwd
Local working directory: /Users/kelsey/Documents/2020_bioinformatics_research_experience/rnaseq-demo
# list the files  on your local (personal computer) location; for example I can see the FastQC html reports I just downloaded
sftp> llls
README.md			dac3_chr21_R1_fastqc.html	siC2_chr21_R2_fastqc.html
dac1_chr21_R1_fastqc.html	dac3_chr21_R2_fastqc.html	siC3_chr21_R1_fastqc.html
dac1_chr21_R2_fastqc.html	siC1_chr21_R1_fastqc.html	siC3_chr21_R2_fastqc.html
dac2_chr21_R1_fastqc.html	siC1_chr21_R2_fastqc.html
dac2_chr21_R2_fastqc.html	siC2_chr21_R1_fastqc.html
# If I want to upload my README file with my documentation for the project to the main rnaseq_practice directory, use put and specify the file path
sftp> put README.md ../../
# show that it's where you expect
sftp> cd ../../
sftp> pwd
Remote working directory: /home/kkeith/rnaseq_practice
sftp> ls
README.md   analysis    data
```