# SPARQL Query 
~~~
1)	List preferred names and synonyms for diseases which are Congenital Disorders of Glycosylation
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?preferred_name ?synonym
from <http://rdf.glycoinfo.org/ggdonto>
where {
 ?disease_uri a ggdon:DiseaseDescriptionGGDonto .
 ?disease_uri ggdon:diseaseType ggdon:CDG .
 ?disease_uri ggdon:diseasePreferredTerm ?preferred_name.
 OPTIONAL {
  ?disease_uri ggdon:diseasePreferredTerm ?preferred_name.
  ?disease_uri ggdon:diseaseSynonyms ?synonym.
  FILTER ( lang(?preferred_name) = lang(?synonym) )
 }
}
order by ?preferred_name ?synonym

2)	List OMIM names of causative genes for diseases which are Lysosomal Storage Diseases
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?omim_name
from <http://rdf.glycoinfo.org/ggdonto>
where {
 ?disease_uri a ggdon:DiseaseDescriptionGGDonto .
 ?disease_uri ggdon:diseaseType ggdon:LSD.
 ?disease_uri ggdon:omimGene ?omim_name.
}

3)	Get symptoms of disease for which the UMLS CUI (Concept Unique Identifier from Unified Medical Language System) is ‘C2931008’
prefix skos: <http://www.w3.org/2004/02/skos/core#>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>
prefix gmncbi: <http://jcggdb.jp/rdf/diseases/gmncbi-schema#>

select distinct ?text_p 
from <http://rdf.glycoinfo.org/ggdonto>
where {
 ?disease_uri a ggdon:DiseaseDescriptionGGDonto .
 ?disease_uri ggdon:umlsCUI "C2931008".
 ?disease_uri gmncbi:hasManifestation ?manifestation_uri .
 ?manifestation_uri skos:prefLabel ?text_p .
}

4)	Get references for disease which has a name or aliases like ‘CDG-IIa’
prefix skos: <http://www.w3.org/2004/02/skos/core#>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?reference
from <http://rdf.glycoinfo.org/ggdonto>
where {
 ?disease_uri a ggdon:DiseaseDescriptionGGDonto.
 {?disease_uri skos:prefLabel  "CDG-IIa"@en.}
 UNION
 {?disease_uri skos:altLabel "CDG-IIa"@en.}
 ?disease_uri ggdon:referencesInfo ?reference.
}


~~~
