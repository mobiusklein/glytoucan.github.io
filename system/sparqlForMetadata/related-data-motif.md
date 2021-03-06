---
title: SPARQL Query for Motif in Related data
layout: default
---
このSPARQL Queryは、GlyTouCanの糖鎖構造のエントリー画面にあるRelated dataにあるMotifの情報を取得するクエリです。

### Input
Sample Accession number : G00051MO  
`?glycan glytoucan:has_primary_id "Input Accession number"`


### Output

| Variable | Data|
|---------|------|
| ?MotifName | Motif name |
| ?moAccNum | Accession number of the Motif |

[SPARQL endpoint](http://test.ts.glytoucan.org/sparql)

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX glycan:  <http://purl.jp/bio/12/glyco/glycan#>
PREFIX glytoucan:  <http://www.glytoucan.org/glyco/owl/glytoucan#>

SELECT DISTINCT ?MotifName (STR(?label) AS ?property) ?moAccNum
FROM <http://purl.jp/bio/12/glyco/glycan#>
FROM <http://rdf.glytoucan.org>
FROM <http://rdf.glytoucan.org/core>
FROM <http://rdf.glytoucan.org/motif>
WHERE{
    # Accession Number
    ?glycan a glycan:saccharide.
    ?glycan glytoucan:has_primary_id "G00051MO" .

    ## Motif
    ?glycan glycan:has_motif ?motif .
    ?motif a glycan:glycan_motif ;
    rdfs:label ?motifLabel .
    BIND((str(?motifLabel) AS ?MotifName))
    ?motif glytoucan:has_primary_id ?moAccNum .

	## Property label
    glycan:has_motif rdfs:label ?label .

}
```
