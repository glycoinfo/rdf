# SPARQL Query Samples



# GlycoEpitope

```
##########################
#
#List of epitope id and name
#
##########################

DEFINE sql:select-option "order"
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bibo: <http://purl.org/ontology/bibo/>
PREFIX glycan: <http://purl.jp/bio/12/glyco/glycan#> 
PREFIX glycodb: <http://purl.jp/bio/12/database/>
PREFIX glytoucan: <http://www.glytoucan.org/glyco/owl/glytoucan#>
PREFIX glycoepitope: <http://www.glycoepitope.jp/epitopes/glycoepitope.owl#>
PREFIX glycoprot: <http://www.glycoprot.jp/>
PREFIX uniprot: <http://www.uniprot.org/core/>

# epiltope id & epitope name
SELECT distinct ?epitope_id ?epitope_name 
FROM <http://rdf.glycoinfo.org/glycoepitope>
WHERE{
        # epitope id
?epitope  a glycan:Glycan_epitope .
        ?epitope dcterms:identifier ?epitope_id .
        # epitope name
        ?epitope rdfs:label ?epitope_name .
}
```
