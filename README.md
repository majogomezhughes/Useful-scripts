# Useful-scripts
## This is a collection of some scripts that are helpful for handling fasta files

Batch renaming of files with spaces in mac:
`find . -depth -exec bash -c '
  for file; do
    tail=${file##*/}
    alnum_only=${tail//[^[:alnum:].]/_}
    mv -v "$file" "${file%/*}/$alnum_only"
  done
' sh {} +`

For manipulating fasta headers:
- Replacing spaces with underscore:
`sed '/^>/ s/ .*//' file.fasta > file-renamed.fasta`

- Deleting everything after underscore:
`cut -d '-' -f1 ign-1.fasta > ign-1-renamed.fasta`


Finding sequences with the same header and retaining only one:
`awk '/^>/{f=!d[$1];d[$1]=1}f' file.fasta > fasta-no-duplicates.fasta`

How many sequences are there in a fasta:
`grep -c ">" file.fasta`

How long is each sequence in a fasta file:
`awk '/^>/{if (l!="") print l; print; l=0; next}{l+=length($0)}END{print l}' file.fasta`


