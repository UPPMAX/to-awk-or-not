# Multiline Fasta To Single Line Fasta
I got the question, solved it, then I realized it is rather common problem. 
So, I googled for it and the solution, I have to admit, was better than mine. 
Here is the solution and [link to the original](https://www.biostars.org/p/9262/) source.

I have a fasta file with following format

``` fasta
>gi|321257144|ref|XP_003193485.1| flap endonuclease [Cryptococcus gattii WM276]
MGIKGLTGLLSENAPKCMKDHEMKTLFGRKVAIDASMSIYQFLIAVRQQDGQMLMNESGDVTSHLMGFFY
RTIRMVDHGIKPCYIFDGKPPELKGSVLAKRFARREEAKEGEEEAKETGTAEDVDKLARRQVRVTREHNE
ECKKLLSLMGIPVVTAPGEAEAQCAELARAGKVYAAGSEDMDTLTFHSPILLRHLTFSEAKKMPISEIHL
DVALRDLEMSMDQFIELCILLGCDYLEPCKGIGPKTALKLMREHGTLGKVVEHIRGKMAEKAEEIKAAAD
EEAEAEAEAEKYDSDPENEEGGETMINSDGEEVPAPSKPKSPKKKAPAKKKKIASSGMQIPEFWPWEEAK
QLFLKPDVVNGDDLVLEWKQPDTEGLVEFLCRDKGFNEDRVRAGAAKLSKMLAAKQQGRLDGFFTVKPKE
PAAKDAGKGKGKDTKGEKRKAEEKGAAKKKTKK
>gi|321473340|gb|EFX84308.1| hypothetical protein DAPPUDRAFT_47502 [Daphnia pulex]
MGIKGLTQVIGDTAPTAIKENEIKNYFGRKVAIDASMSIYQFLIAVRSEGAMLTSADGETTSHLMGIFYR
TIRMVDNGIKPVYVFDGKPPDMKGGELTKRAEKREEASKQLVLATDAGDAVEMEKMNKRLVKVNKGHTDE
CKQLLTLMGIPYVEAPCEAEAQCAALVKAGKVYATATEDMDSLTFGSNVLLRYLTYSEAKKMPIKEFHLD
KILDGLSYTMDEFIDLCIMLGCDYCDTIKGIGAKRAKELIDKHRCIEKVIENLDTKKYTVPENWPYQEAR
RLFKTPDVADAETLDLKWTQPDEEGLVKFMCGDKNFNEERIRSGAKKLCKAKTGQTQGRLDSFFKVLPSS
KPSTPSTPASKRKVGCIIYLFLYF
```
but I wanna to look sequence in a single line, not in many line as they are. any quick method??


using awk:
``` awk
awk '/^>/ {printf("\n%s\n",$0);next; } { printf("%s",$0);}  END {printf("\n");}' < file.fa

>gi|321257144|ref|XP_003193485.1| flap endonuclease [Cryptococcus gattii WM276]
MGIKGLTGLLSENAPKCMKDHEMKTLFGRKVAIDASMSIYQFLIAVRQQDGQMLMNESGDVTSHLMGFFYRTIRMVDHGIKPCYIFDGKPPELKGSVLAKRFARREEAKEGEEEAKETGTAEDVDKLARRQVRVTREHNEECKKLLSLMGIPVVTAPGEAEAQCAELARAGKVYAAGSEDMDTLTFHSPILLRHLTFSEAKKMPISEIHLDVALRDLEMSMDQFIELCILLGCDYLEPCKGIGPKTALKLMREHGTLGKVVEHIRGKMAEKAEEIKAAADEEAEAEAEAEKYDSDPENEEGGETMINSDGEEVPAPSKPKSPKKKAPAKKKKIASSGMQIPEFWPWEEAKQLFLKPDVVNGDDLVLEWKQPDTEGLVEFLCRDKGFNEDRVRAGAAKLSKMLAAKQQGRLDGFFTVKPKEPAAKDAGKGKGKDTKGEKRKAEEKGAAKKKTKK
>gi|321473340|gb|EFX84308.1| hypothetical protein DAPPUDRAFT_47502 [Daphnia pulex]
MGIKGLTQVIGDTAPTAIKENEIKNYFGRKVAIDASMSIYQFLIAVRSEGAMLTSADGETTSHLMGIFYRTIRMVDNGIKPVYVFDGKPPDMKGGELTKRAEKREEASKQLVLATDAGDAVEMEKMNKRLVKVNKGHTDECKQLLTLMGIPYVEAPCEAEAQCAALVKAGKVYATATEDMDSLTFGSNVLLRYLTYSEAKKMPIKEFHLDKILDGLSYTMDEFIDLCIMLGCDYCDTIKGIGAKRAKELIDKHRCIEKVIENLDTKKYTVPENWPYQEARRLFKTPDVADAETLDLKWTQPDEEGLVKFMCGDKNFNEERIRSGAKKLCKAKTGQTQGRLDSFFKVLPSSKPSTPSTPASKRKVGCIIYLFLYF
```

!!! note
    Note that there is a blank line at the beginning of the output - this is further discusses in the original forum post.  
    This example case will be discussed during the workshop