####
#### Testing and load helpers for GOlr
####

###
### User variables.
###
### Remember that those with "?=" can be overridden with
### environmental variables. Helpful if you are trying to automate
### things, like with Jenkins for example.
###

## Options.
OWLTOOLS_MAX_MEMORY ?= 12G
OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS = --merge-support-ontologies --remove-subset-entities upperlevel --reasoner elk

## Bins.
MAVEN_EXE ?= ~/local/src/java/apache-maven-3.0.5/bin/mvn

## URLs.
SOLR_URL ?= http://localhost:8983/solr/biggo/
ANATOMY_SOLR_URL ?= http://localhost:8983/solr/anatomy/
DISEASE_SOLR_URL ?= http://localhost:8983/solr/disease/
GO_SOLR_URL ?= http://localhost:8983/solr/go/
LIFESTAGE_SOLR_URL ?= http://localhost:8983/solr/lifestage/
PHENOTYPE_SOLR_URL ?= http://localhost:8983/solr/phenotype/
MOUSEPHENE_SOLR_URL ?= http://localhost:8983/solr/mousephene/

## Paths.
OWLTOOLS_ROOT ?= ~/local/src/git/owltools/
BBOP_JS_ROOT ?= ~/local/src/git/bbop-js/
PANTHER_FILES_DIR ?= ~/local/src/svn/geneontology.org/trunk/experimental/trees/panther_data/
SOLR_DATA_ROOT ?= /srv/solr

## Files.
SOLR_LOAD_LOG ?= /tmp/golr_timestamp.log
SOLR_USE_CATALOG_XML ?= /tmp/catalog.xml

## File lists.
SCHEMA_METADATA ?= \
 ../metadata/ont-config.yaml \
 ../metadata/bio-config.yaml \
 ../metadata/ann-config.yaml \
 ../metadata/protein-family-config.yaml \
 ../metadata/general-config.yaml \
 ../metadata/ann_ev_agg-config.yaml
ONTOLOGY_METADATA ?= ../metadata/ont-config.yaml

ANATOMYONTOLOGY ?= \
	http://caltech.wormbase.org/ontology/anatomy_ontology.WS294.obo.xunion \
	/home/raymond/local/src/git/ncbitaxon/subsets/taxslim.owl

DISEASEONTOLOGY ?= \
	http://caltech.wormbase.org/ontology/disease_ontology.WS294.obo \
	/home/raymond/local/src/git/ncbitaxon/subsets/taxslim.owl

# GOONTOLOGY ?= http://www.geneontology.org/ontology/obo_format_1_2/gene_ontology_ext.obo
GOONTOLOGY ?= \
	http://caltech.wormbase.org/ontology/gene_ontology.WS294.obo \
	/home/raymond/local/src/git/ncbitaxon/subsets/taxslim.owl

LIFESTAGEONTOLOGY ?= \
	http://caltech.wormbase.org/ontology/development_ontology.WS294.obo \
	/home/raymond/local/src/git/ncbitaxon/subsets/taxslim.owl

PHENOTYPEONTOLOGY ?= \
	http://caltech.wormbase.org/ontology/phenotype_ontology.WS294.obo \
	/home/raymond/local/src/git/ncbitaxon/subsets/taxslim.owl

MAMMALPHENEONTOLOGY ?= \
	http://purl.obolibrary.org/obo/mp.owl


ONTOLOGIES ?= \
 http://purl.obolibrary.org/obo/go.owl \
 http://purl.obolibrary.org/obo/ncbitaxon/subsets/taxslim.owl \
 http://purl.obolibrary.org/obo/cl/cl-basic.owl \
 http://purl.obolibrary.org/obo/eco.owl \
 http://geneontology.org/ontology/extensions/gorel.owl \
 http://purl.obolibrary.org/obo/ma.owl \
 http://purl.obolibrary.org/obo/pato.owl \
 http://purl.obolibrary.org/obo/po.owl \
 http://purl.obolibrary.org/obo/emap.owl

## Next:
# http://purl.obolibrary.org/obo/uberon/basic.owl

ALL_GAFS ?= \
	http://current.geneontology.org/annotations/genedb_lmajor.gaf.gz \
	http://current.geneontology.org/annotations/genedb_pfalciparum.gaf.gz \
	http://current.geneontology.org/annotations/genedb_tbrucei.gaf.gz \
	http://current.geneontology.org/annotations/aspgd.gaf.gz \
	http://current.geneontology.org/annotations/cgd.gaf.gz \
	http://current.geneontology.org/annotations/dictybase.gaf.gz \
	http://current.geneontology.org/annotations/ecocyc.gaf.gz \
	http://current.geneontology.org/annotations/fb.gaf.gz \
	http://current.geneontology.org/annotations/goa_chicken.gaf.gz \
	http://current.geneontology.org/annotations/goa_chicken_complex.gaf.gz \
	http://current.geneontology.org/annotations/goa_chicken_rna.gaf.gz \
	http://current.geneontology.org/annotations/goa_cow.gaf.gz \
	http://current.geneontology.org/annotations/goa_cow_complex.gaf.gz \
	http://current.geneontology.org/annotations/goa_cow_isoform.gaf.gz \
	http://current.geneontology.org/annotations/goa_cow_rna.gaf.gz \
	http://current.geneontology.org/annotations/goa_dog.gaf.gz \
	http://current.geneontology.org/annotations/goa_dog_complex.gaf.gz \
	http://current.geneontology.org/annotations/goa_dog_isoform.gaf.gz \
	http://current.geneontology.org/annotations/goa_dog_rna.gaf.gz \
	http://current.geneontology.org/annotations/goa_human.gaf.gz \
	http://current.geneontology.org/annotations/goa_human_complex.gaf.gz \
	http://current.geneontology.org/annotations/goa_human_isoform.gaf.gz \
	http://current.geneontology.org/annotations/goa_human_rna.gaf.gz \
	http://current.geneontology.org/annotations/goa_pig.gaf.gz \
	http://current.geneontology.org/annotations/goa_pig_complex.gaf.gz \
	http://current.geneontology.org/annotations/goa_pig_isoform.gaf.gz \
	http://current.geneontology.org/annotations/goa_pig_rna.gaf.gz \
	http://current.geneontology.org/annotations/goa_uniprot_all_noiea.gaf.gz \
	http://current.geneontology.org/annotations/gonuts.gaf.gz \
	http://current.geneontology.org/annotations/gramene_oryza.gaf.gz \
	http://current.geneontology.org/annotations/jcvi.gaf.gz \
	http://current.geneontology.org/annotations/mgi.gaf.gz \
	http://current.geneontology.org/annotations/pamgo_atumefaciens.gaf.gz \
	http://current.geneontology.org/annotations/pamgo_ddadantii.gaf.gz \
	http://current.geneontology.org/annotations/pamgo_mgrisea.gaf.gz \
	http://current.geneontology.org/annotations/pamgo_oomycetes.gaf.gz \
	http://current.geneontology.org/annotations/pombase.gaf.gz \
	http://current.geneontology.org/annotations/pseudocap.gaf.gz \
	http://current.geneontology.org/annotations/reactome.gaf.gz \
	http://current.geneontology.org/annotations/rgd.gaf.gz \
	http://current.geneontology.org/annotations/sgd.gaf.gz \
	http://current.geneontology.org/annotations/sgn.gaf.gz \
	http://current.geneontology.org/annotations/tair.gaf.gz \
	http://current.geneontology.org/annotations/wb.gaf.gz \
	http://current.geneontology.org/annotations/zfin.gaf.gz \


ANATOMY_GAF ?= http://caltech.wormbase.org/ontology/anatomy_association.WS294.wb.clean
GO_GAF ?= http://caltech.wormbase.org/ontology/gene_association.WS294.wb.clean
PHENOTYPE_GAF ?= http://caltech.wormbase.org/ontology/phenotype_association.WS294.wb.clean.col7
DISEASE_GAF ?= http://caltech.wormbase.org/ontology/disease_association.WS294.wb.clean
LIFESTAGE_GAF ?= http://caltech.wormbase.org/ontology/development_association.WS294.wb.clean
MOUSEPHENE_GAF ?= http://caltech.wormbase.org/ontology/MGI_phenotype_association.tsv

##
DATE = `date +'%Y-%m-%d'`
TIME = `date +'%H:%M'`

###
### Nothing to see below here: targets.
###

all:
	@echo "Not a valid target here. Please read the documentation."

###
### OWLTools operations.
###

.PHONY: owltools-update
owltools-update:
	cd $(OWLTOOLS_ROOT) && git pull
# svn update --accept theirs-full

.PHONY: owltools-build
owltools-build:
	cd $(OWLTOOLS_ROOT)/OWLTools-Parent && $(MAVEN_EXE) clean package -DskipTests

.PHONY: owltools-test
owltools-test:
	cd $(OWLTOOLS_ROOT)/OWLTools-Parent && $(MAVEN_EXE) clean package

###
### GOlr operations.
###

.PHONY: golr-install
golr-install:
	sudo ./tools/golr.el

.PHONY: golr-purge
golr-purge:
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(SOLR_URL) --solr-purge

.PHONY: golr-schema
golr-schema:
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-config $(SCHEMA_METADATA) --solr-schema-dump | ./tools/remove-schema-cruft.pl > ./solr/conf/schema.xml

###
### Loading.
###

## Erase the load load and start fresh.
.PHONY: clear-load-log
clear-load-log:
	echo -n "" > $(SOLR_LOAD_LOG)

## Create a warning message about loading.
.PHONY: message-load-start
message-load-start:
	../scripts/global-message.pl -e "GOlr is currently being reloaded (started at $(TIME) on $(DATE)). Any results will be partial at best--please check back later."

## Create a warning message about loading.
.PHONY: message-load-clear
message-load-clear:
	../scripts/global-message.pl -c

## Load the ontology stuff.
.PHONY: load-ontology
load-ontology: owltools-build
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general
	make message-load-clear


## The full and final load.

## Load the ontology stuff without building.
.PHONY: load-ontology-quick
load-ontology-quick:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general
	make message-load-clear

## Test GAF.
.PHONY: load-test-gaf
load-test-gaf: owltools-build
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --read-panther $(PANTHER_FILES_DIR) --solr-log $(SOLR_LOAD_LOG) --solr-load-gafs $(TEST_GAF) --solr-load-panther --solr-load-panther-general
	make message-load-clear

.PHONY: load-gaf
load-gaf: owltools-build
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-log $(SOLR_LOAD_LOG) --solr-load-gafs $(ALL_GAFS)
	make message-load-clear

.PHONY: load-mgi-phene
load-mgi-phene:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(MAMMALPHENEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(MOUSEPHENE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(MOUSEPHENE_GAF)
	make message-load-clear


.PHONY: load-biggo
load-biggo:
	make load-ontology
	make load-gaf
	make load-optimize

.PHONY: load-wb-full
load-wb-full: owltools-build clear-load-log
	make load-wb-anatomy
	make load-wb-disease
	make load-wb-go
	make load-wb-lifestage
	make load-wb-phenotype
	make load-optimize-wb
.PHONY: load-wb-anatomy
load-wb-anatomy:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ANATOMYONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(ANATOMY_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(ANATOMY_GAF)
	make message-load-clear
.PHONY: load-wb-disease
load-wb-disease:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(DISEASEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(DISEASE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(DISEASE_GAF)
	make message-load-clear
.PHONY: load-wb-go
load-wb-go:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(GOONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(GO_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(GO_GAF)
	make message-load-clear
.PHONY: load-wb-lifestage	
load-wb-lifestage:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(LIFESTAGEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(LIFESTAGE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(LIFESTAGE_GAF)
	make message-load-clear
.PHONY: load-wb-phenotype	
load-wb-phenotype:
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(PHENOTYPEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(PHENOTYPE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(PHENOTYPE_GAF)
	make message-load-clear
.PHONY: load-optimize-wb
load-optimize-wb:
	../scripts/global-message.pl -w "GOlr is currently being optimized (started at $(TIME) on $(DATE)). Expect reduced performance."
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(ANATOMY_SOLR_URL) --solr-optimize
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(DISEASE_SOLR_URL) --solr-optimize
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(GO_SOLR_URL) --solr-optimize
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(LIFESTAGE_SOLR_URL) --solr-optimize
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(PHENOTYPE_SOLR_URL) --solr-optimize
.PHONY: load-test
load-test: owltools-build clear-load-log
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(TESTONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(TEST_GAFS)
	make message-load-clear	
## "Silent" variation--useful w/o amigo.
.PHONY: load-full-silent
load-full-silent: owltools-build clear-load-log
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --read-panther $(PANTHER_FILES_DIR) --solr-load-gafs $(ALL_GAFS) --solr-load-panther --solr-load-panther-general

## An option optimizing step.
.PHONY: load-optimize
load-optimize:
	../scripts/global-message.pl -w "GOlr is currently being optimized (started at $(TIME) on $(DATE)). Expect reduced performance."
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(SOLR_URL) --solr-optimize
	../scripts/global-message.pl -c
## "Silent" variation--useful w/o amigo.
.PHONY: load-optimize-silent
load-optimize-silent:
	$(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools --solr-url $(SOLR_URL) --solr-optimize

###
### Services.
###

.PHONY: service-restart-nginx
service-restart-nginx:
	cd /tmp && sudo trash-put golr-rps-cache amigo2-rps-cache && sudo trash-empty && sudo /etc/init.d/nginx restart

.PHONY: service-restart-jetty
service-restart-jetty:
	sudo /etc/init.d/jetty restart
