# virtual-4C-interactions-with-Sushi-in-R
plotting virtual 4C interactions with Sushi in R

plotgardener

grep E_segment RT_class_ALL_10kb.bed > RT_class_E_segment_10kb.bed


#######################################################################################


### overlap with bed to find bait_bins

bedtools intersect -wa \
-b <( grep -v scaf_ RT_class_E_segment_10kb.bed ) \
-a <( grep -v scaf_ RT_10000_abs.bed ) > RT_class_E_segment_10kb.bins.bed

#######################################################################################


### overlap with RT iced matrix (at 10kb) to find interactions frequencies, first bin1 and then bin2.

1)    Add RT to the matrix files (ICE from HiC-pro) (https://github.com/Sarachaudry/HiC-contacts-with-RT-annotations)
 

#######################################################################################


join bait_bins with the matrix. Separately with bin1 (columns 1-5)(to retrieve partners_bin2) and with bin2 (column 9-10) (to retrieve partners_bin1), then concatenate and sort

#### CAN FIND INTERACTIONS WITH OTHER BAITS (M, other E, etc.. ) by changing the bins (111685 and 111706).

time cat RT_10000_iced.RT1.RT2.matrix | \
awk '{if (($1 >= 111685) && ($1 <=111706) || ($6 >= 111685) && ($6 <=111706) ) print $0 }' > RT_class_E_segement_10kb.target.matrix

cat RT_class_E_segement_10kb.target.matrix | awk '{print $0"\t"($5_$10) }' > RT_class_E_segement_10kb.target.matrix.index


#######################################################################################


split and plot by distance in R >>> plotgardener
