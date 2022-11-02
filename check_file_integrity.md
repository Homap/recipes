for fastq in P26503_1*/*/*/*do
echo $fastq
md5 -r $fastq >> download_md5sum.txt
done

awk -F"/" 'FNR==NR{filearray[$1]=$NF; next }!($1 in filearray){printf "%s has a different md5sum\n",$NF}' P26503_101.md5 download_md5sum.txt
