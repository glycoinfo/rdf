# SPARQL Query 
# GlycoProtDB

```
##########################
#
#List of GlycoProtDB id and taxonomy id, uniprot id
#
##########################

prefix foaf:  <http://xmlns.com/foaf/0.1/> 
prefix dcterms: <http://purl.org/dc/terms/> 
prefix bt:    <http://purl.org/biotop/biotop.owl#> 
prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> 
prefix obo:   <http://purl.obolibrary.org/obo/> 
prefix bto:   <http://purl.obolibrary.org/obo/bto#> 
prefix owl:   <http://www.w3.org/2002/07/owl#> 
prefix xsd:   <http://www.w3.org/2001/XMLSchema#> 
prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
prefix skos:  <http://www.w3.org/2004/02/skos/core#> 
prefix glycan: <http://purl.jp/bio/12/glyco/glycan#> 
prefix faldo: <http://biohackathon.org/resource/faldo#> 
prefix up_core: <http://purl.uniprot.org/core/> 
prefix edam:  <http://edamontology.org/> 
prefix pav:  <http://purl.org/pav/> 
prefix gpdb: <http://purl.jp/bio/12/gpdb/2014/7/owl#>

select distinct ?gpdb_id ?taxonomy_id ?uniprot_id
from <http://purl.jp/bio/12/gpdb/3.0>
where{
    ?gpdb ?a glycan:Glycoprotein.
    ?gpdb dcterms:identifier ?gpdb_id.
    ?gpdb glycan:has_aglycon ?aglycon.
    ?aglycon dcterms:identifier ?uniprot_id.
    ?gpdb glycan:is_from_source ?taxonomy.
    ?taxonomy dcterms:identifier ?taxonomy_id.
}
```
