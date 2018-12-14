base <http://www.cazy.org/>
prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>
prefix xsd: <http://www.w3.org/2001/XMLSchema#>
prefix skos: <http://www.w3.org/2004/02/skos/core#>
prefix up: <http://www.purl.uniprot.org/core/>
prefix cazy: <http://www.cazy.org/owl/v1>
prefix dcterms: <http://purl.org/dc/terms/>
prefix enzyme: <http://purl.uniprot.org/enzyme/>

select distinct ?label ?organism ?comment ?resource
from <http://rdf.glycoinfo.org/cazy>
where { 
?protein a up:Protein .
?protein rdfs:comment ?comment .
?protein up:organism ?or .
?or up:name ?organism .
?protein skos:altLabel  ?label .
VALUES ?label { "{{id}}" }
?protein rdfs:seeAlso ?resource .
} 
