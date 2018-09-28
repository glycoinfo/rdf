# SPARQL Query 
~~~
1)	List species names and their strains names
prefix pacon: <http://jcggdb.jp/rdf/diseases/paconto-schema#>
prefix glycan: <http://purl.jp/bio/12/glyco/glycan#>
prefix uniprot: <http://purl.uniprot.org/core/>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?species_name ?strain_name
from <http://jcggdb.jp/rdf/diseases/paconto>
where {
 ?species_uri ggdon:conceptType pacon:PathogenicMicroorganisms.
 ?species_uri uniprot:scientificName ?species_name.
 OPTIONAL {?species_uri glycan:has_strain ?strain_name.}
}
order by ?species_name ?strain_name

2)	List pathogen adherence molecules of infectious agents which have a name like ‘Escherichia coli’
prefix pacon: <http://jcggdb.jp/rdf/diseases/paconto-schema#>
prefix uniprot: <http://purl.uniprot.org/core/>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?pathogen_name
from <http://jcggdb.jp/rdf/diseases/paconto>
where {
 ?pathogen_uri ggdon:conceptType pacon:PathogenAdherenceMolecules.
 ?pathogen_uri uniprot:scientificName ?scientific_name.
 FILTER regex(?scientific_name,"Escherichia coli","i")
 ?pathogen_uri pacon:pathogenAdherMolecName ?pathogen_name.
}

3)	List glycan ligands of hosts with which lectins of infectious agents ‘Haemophilus influenzae’ have binding interactions
prefix pacon: <http://jcggdb.jp/rdf/diseases/paconto-schema#>
prefix glycan: <http://purl.jp/bio/12/glyco/glycan#>
prefix uniprot: <http://purl.uniprot.org/core/>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>

select distinct ?glycan_name ?interaction_type
from <http://jcggdb.jp/rdf/diseases/paconto>
where {
 ?pathogen_uri ggdon:conceptType pacon:PathogenAdherenceMolecules.
 ?pathogen_uri uniprot:scientificName ?scientific_name.
 FILTER regex(?scientific_name,"Haemophilus influenzae","i")
 ?pathogen_reference_uri a pacon:AffinityInReference.
 ?pathogen_reference_uri glycan:has_affinity_to ?pathogen_uri.
 ?pathogen_reference_uri pacon:describedInReference ?reference_uri.
 ?glycan_reference_uri a pacon:InteractionInReference .
 ?glycan_reference_uri pacon:describedInReference ?reference_uri.
 ?pathogen_uri pacon:interactionInReference ?glycan_reference_uri .
 ?glycan_reference_uri pacon:interactionType ?interaction_type .
 ?glycan_reference_uri pacon:hasInteractionWith ?glycan_uri .
 ?glycan_uri a pacon:GlycansPACDB .
 ?glycan_uri pacon:carbohydrateLigandName ?glycan_name .
}


4)	List PMID (from PubMed) for references in which described that lectin-glycan interaction plays a role in Respiratory Tract Diseases
prefix pacon: <http://jcggdb.jp/rdf/diseases/paconto-schema#>
prefix gmncbi: <http://jcggdb.jp/rdf/diseases/gmncbi-schema#>
prefix uniprot: <http://purl.uniprot.org/core/>
prefix ggdon: <http://jcggdb.jp/rdf/diseases/ggdonto-schema#>
prefix gdgdb: <http://jcggdb.jp/rdf/diseases/gdgdb-schema#>
prefix bibo: <http://purl.org/ontology/bibo/>

select distinct ?pmid
from <http://jcggdb.jp/rdf/diseases/paconto>
where {
 ?disease_uri ggdon:conceptType pacon:DiseasesNameAndClass.
 ?disease_uri pacon:diseaseClass ?disease_class .
 ?disease_uri gdgdb:diseaseName ?disease_name .
 FILTER regex(?disease_class,"Respiratory Tract Disease","i")
 ?disease_uri gmncbi:causedBy ?species_uri .
 ?species_reference_uri a pacon:OccurInOrganismInReference.
 ?species_reference_uri uniprot:organism ?species_uri .
 ?species_reference_uri pacon:describedInReference ?reference_uri.
 ?reference_uri ggdon:conceptType pacon:ReferencesData.
 ?reference_uri bibo:pmid ?pmid.
}

~~~
