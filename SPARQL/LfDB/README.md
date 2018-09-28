# SPARQL Query 
# LfDB

```
##########################
#
#List of LfDB id and lectin name and Pfam, Pfam id
#
##########################

prefix up_core: <http://purl.uniprot.org/core/>
prefix edam:    <http://edamontology.org/> 
prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
prefix sio:   <http://semanticscience.org/resource/> 
prefix skos:  <http://www.w3.org/2004/02/skos/core#> 
prefix dcterms: <http://purl.org/dc/terms/> 
prefix lfdb:  <http://purl.jp/bio/12/lfdb/2014/7/owl#> 
prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> 
prefix bibo:  <http://purl.org/ontology/bibo/> 
prefix obo:   <http://purl.obolibrary.org/obo/> 
prefix glycan: <http://purl.jp/bio/12/glyco/glycan#> 
prefix dc:    <http://purl.org/dc/elements/1.1/> 
prefix foaf:    <http://xmlns.com/foaf/0.1/>

select distinct ?lfdb_id ?lectin_name ?pfam_id ?pfam_name
from <http://purl.jp/bio/12/lfdb>
where{
    ?lectin a glycan:Lectin.
    ?lectin dcterms:identifier ?lfdb_id.
    ?lectin lfdb:has_lectin_name ?lectin_name.
    optional {
        ?lectin lfdb:in_pfam_family ?pfam.
        ?pfam dcterms:identifier ?pfam_id.
        ?pfam rdfs:label ?pfam_name.
    }
} order by ?lfdb_id
```
