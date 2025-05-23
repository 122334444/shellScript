# shellScript
#!/bin/bash

url="https://www.amfiindia.com/spages/NAVAll.txt"
output_file="amfi_data.tsv"

curl -s "$url" | awk -F';' '
    BEGIN { OFS="\t"; print "Scheme Name", "Asset Value" }
    NR > 1 && NF >= 5 { print $4, $5 }
' > "$output_file"

echo "Saved TSV data to $output_file"
