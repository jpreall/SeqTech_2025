# SeqTech_2025
**CSHL Advanced Sequencing Technologies and Bioinformatics Analysis Course**  
Jon Preall  
Research Associate Professor @ CSHL

## Lecture Slides
[11/10: Single Cell Sequencing]([https://www.dropbox.com/scl/fi/o2kjzpdcm5iuokdotdh3p/Preall_SeqTech_2023.pptx?rlkey=bfl3n7vw1ubz0jq93v8hr65mv&dl=0](https://www.dropbox.com/scl/fi/2fgj4dfuwbpuuadtanzjz/Preall_SingleCell_SeqTech_2025.pdf?rlkey=wfhdc2sqyf7kjobyki6poj4ut&dl=0)) (13MB .pdf file)  
[11/19: Intro to scRNA-seq Analysis](https://www.dropbox.com/scl/fi/yrkwawtortfgwq8hfsiyn/Intro_to_scRNAseq_2023.pptx?rlkey=we58cjp366l7z5v1yzm8vnhix&dl=0) (36MB .pptx file)

## 11/19: Intro to Python

**Connect to your instance**
```
AWSIP=107.22.88.84
PEM=cshl_2025_student.pem
ssh -i $PEM ubuntu@$AWSIP
```
**Start Jupyter Lab**
```
cd workspace
jupyter lab
```
** Modify the URL that Jupyter tells you to use to connect to your Lab server**
```
To access the server, open this file in a browser:
        file:///home/ubuntu/.local/share/jupyter/runtime/jpserver-1707-open.html
    Or copy and paste one of these URLs:
        http://**ip-172-31-37-238**:8888/lab?token=c541badc8c933eabcf38054d6dc21621340fe62aa1b86fc3
     or http://127.0.0.1:8888/lab?token=c541badc8c933eabcf38054d6dc21621340fe62aa1b86fc3
```
will become
`http://**107.22.88.84**:8888/lab?token=c541badc8c933eabcf38054d6dc21621340fe62aa1b86fc3`


```
print('Hello World!')
```

## 11/19: Intro to Single Cell Visualization in Loupe
[Link to download Loupe Data](https://www.dropbox.com/scl/fi/ymv71xz7bb9pphoege4cc/SeqTech2023_iMac_data.tar.gz?rlkey=9d29poys1cat4a1ste3vis7a9&dl=0) (.tar.gz file)  
[Visium SD dataset](https://www.dropbox.com/scl/fi/53050l6vqgqvfnscxpua3/Castellanos_MC05_DS4M_D1.cloupe?rlkey=lcl1rva9mk5ga9fy0d4g5v25g&dl=0) (.cloupe file)  


## 11/20 9:00 - 10:30am: Intro to Pandas and Data Visualization

## 11/20 10:45 - 12:00pm: Python Exercises
[CCLE data download](https://www.dropbox.com/scl/fi/uwgg1d1qus6izwoplrzgh/CCLE_rpkm_forcourse.csv.gz?rlkey=qcf1vna500x0q4j2ma25rvs2w&dl=0) (.tar.gz)

## 11/20 2:00-5:30pm: Scanpy Lab
[Scanpy Data Package](https://www.dropbox.com/scl/fi/ft369bh8ggj0141a1kggm/AWS_package.tar.gz?rlkey=u7i0x1rncerlajnwmq28c0tt9&dl=0) (.tar.gz)
```
JP=3.86.4.253
cd /workspace/
wget http://$JP/pbmc.tar
tar -xvf SingleCell.tar
```

## 11/21 9:10-10:30am: Cell Typing Lab
[Scanpy Data Package]

## 11/21 10:45am-12:00pm: Woodbury Tour!

## 11/21 1:00pm-2:00pm: Spatial Analysis: How to Publish Your First Dataset in Nature
```
print('Nature Paper')
```

  
