# SPARQL Query 
~~~
1)	List diseases names
prefix gdgdb: <http://jcggdb.jp/rdf/diseases/gdgdb-schema#>

select distinct ?disease_name
from <http://jcggdb.jp/rdf/diseases/gdgdb>
where {
 ?disease_uri a gdgdb:DiseaseDescriptionGDGDB.
 ?disease_uri gdgdb:diseaseName ?disease_name.
}

2)	List genes names and official gene symbols
prefix gdgdb: <http://jcggdb.jp/rdf/diseases/gdgdb-schema#>

select distinct ?gene_symbol ?gene_name
from <http://jcggdb.jp/rdf/diseases/gdgdb>
where {
 ?gene_uri a gdgdb:GeneDescriptionGDGDB.
 ?gene_uri gdgdb:geneSymbol ?gene_symbol.
 OPTIONAL {?gene_uri gdgdb:geneNames?gene_name.}
}
order by ?gene_symbol

3)	Get pathogenesis of disease which has a name like ‘CDG Ia’
prefix gdgdb: <http://jcggdb.jp/rdf/diseases/gdgdb-schema#>

select distinct ?pathogenesis
from <http://jcggdb.jp/rdf/diseases/gdgdb>
where {
 ?disease_uri a gdgdb:DiseaseDescriptionGDGDB.
 ?disease_uri gdgdb:pathogenesis ?pathogenesis.
 ?disease_uri gdgdb:diseaseName ?disease_name.
 FILTER regex(?disease_name,"CDG Ia","i").
}

4)	Get name of disease for which the name of causative gene is ‘PMM2’ 
prefix gdgdb: <http://jcggdb.jp/rdf/diseases/gdgdb-schema#>

select distinct ?disease_name
from <http://jcggdb.jp/rdf/diseases/gdgdb>
where {
 ?document_uri a gdgdb:DocumentGDGDB.
 ?gene_uri a gdgdb:GeneDescriptionGDGDB.
 ?disease_uri a gdgdb:DiseaseDescriptionGDGDB.
 ?document_uri gdgdb:diseaseDescription ?disease_uri.
 ?document_uri gdgdb:geneDescription ?gene_uri.
 ?gene_uri gdgdb:geneSymbol ?gene_symbol.
 ?disease_uri gdgdb:diseaseNames ?disease_name.
 FILTER regex(?gene_symbol,"^PMM2$","i")
}
~~~

