# E2
This is the second excercise.
## Making a directory 
`mkdir -p kata/data`
`cd kata/data`
## Starting a screen
`screen -S kata`
## Saving data
`cp /data-shared/vcf_examples/luscinia_vars.vcf.gz .`
## Extracting information about DP of the whole genome
`< /data-shared/vcf_examples/luscinia_vars.vcf.gz zcat | egrep -o 'DP=[^;]*' | sed 's/DP=//' > g.csv`
## Saving your extracted data from the whole genome
Now you have to run this command on your "home" machine.
`Katerinka$ scp user13@ngs-course.duckdns.org:projects/kata/g.csv .`
## Now, for extracting DP for each chromosome separately, I decided to create a function
`chrfun() { zcat | grep -v '^#' | grep $1| egrep -o 'DP=[^;]*' |  sed 's/DP=//' > $2.csv ;}`
$1 is the name of the chromosome, $2 is the under which I want to safe my file.
`< /data-shared/vcf_examples/luscinia_vars_flags.vcf.gz chrfun  '^chrZ\s' zet`
##Again, we have to save to our local disk
`Katerinka$ scp user13@ngs-course.duckdns.org:projects/kata/zet.csv .`

## In R studio – start by setting a working directory
`setwd("~/Desktop/PřF UK/UNIX"`
## Loading my file
`datag <- read.csv("g.csv", col.names = "DP")`
## Plotting a graph (histogram) for whole genome
`datag %>% 
  ggplot(aes(DP)) +
  geom_histogram() +
  scale_y_log10()`

## For separate chromosome (I took Z as an example)
 `dataz <- read.csv("zet.csv", col.names = "DP")`
## Plotting a graph (histogram) for whole genome
`dataz %>% 
  ggplot(aes(DP)) +
  geom_histogram() +
  scale_y_log10()`



