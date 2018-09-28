# SPARQL Query 

~~~
1)List of GeneSymbol and GGDB-ID

prefix ggdb: <http://purl.jp/bio/12/ggdb/2015/6/owl#>
prefix dcterms: <http://purl.org/dc/terms/>

select distinct *
from <http://rdf.glycoinfo.org/ggdb>
 where {
 ?gg_uri a ggdb:Glycogene .
 ?gg_uri dcterms:identifier ?gg_id .
 ?gg_uri ggdb:has_gene_symbol ?symbol .
}
~~~
