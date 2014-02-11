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
OWLTOOLS_MAX_MEMORY ?= 4G
OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS = --merge-support-ontologies --reasoner elk

## Bins.
MAVEN_EXE ?= ~/local/src/java/apache-maven-3.0.5/bin/mvn

## URLs.
SOLR_URL ?= http://localhost:8080/solr/
ANATOMY_SOLR_URL ?= http://localhost:8080/solr/anatomy/
DISEASE_SOLR_URL ?= http://localhost:8080/solr/disease/
GO_SOLR_URL ?= http://localhost:8080/solr/go/
LIFESTAGE_SOLR_URL ?= http://localhost:8080/solr/lifestage/
PHENOTYPE_SOLR_URL ?= http://localhost:8080/solr/phenotype/

 

## Paths.
OWLTOOLS_ROOT ?= ~/local/src/svn/owltools/
BBOP_JS_ROOT ?= ~/local/src/git/bbop-js/
PANTHER_FILES_DIR ?= ~/local/src/svn/geneontology.org/trunk/experimental/trees/panther_data/

## Files.
SOLR_LOAD_LOG ?= /tmp/golr_timestamp.log

## File lists.
SCHEMA_METADATA ?= \
 ../metadata/ont-config.yaml \
 ../metadata/bio-config.yaml \
 ../metadata/ann-config.yaml \
 ../metadata/protein-family-config.yaml \
 ../metadata/general-config.yaml \
 ../metadata/ann_ev_agg-config.yaml
ONTOLOGY_METADATA ?= ../metadata/ont-config.yaml

ANATOMYONTOLOGY ?= http://caltech.wormbase.org/ontology/anatomy_ontology.obo
DISEASEONTOLOGY ?= http://caltech.wormbase.org/ontology/disease_ontology.obo
GOONTOLOGY ?= http://caltech.wormbase.org/ontology/gene_ontology.obo
LIFESTAGEONTOLOGY ?= http://caltech.wormbase.org/ontology/worm_development.obo
PHENOTYPEONTOLOGY ?= http://caltech.wormbase.org/ontology/phenotype_ontology.obo
 
## Next:
# http://purl.obolibrary.org/obo/uberon/basic.owl

ALL_GAFS ?= \
	http://www.geneontology.org/gene-associations/gene_association.wb.gz \

ANATOMY_GAF ?= http://caltech.wormbase.org/ontology/anatomy_association.wb
GO_GAF ?= http://caltech.wormbase.org/ontology/gene_association.wb
PHENOTYPE_GAF ?= http://caltech.wormbase.org/ontology/phenotype_association.wb

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
	cd $(OWLTOOLS_ROOT) && svn update
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
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ONTOLOGIES) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(SOLR_URL) --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general
	make message-load-clear

## The full and final load.

.PHONY: load-wb-full
load-wb-full:
	make load-wb-anatomy
	make load-wb-disease
	make load-wb-go
	make load-wb-lifestage
	make load-wb-phenotype
	make load-optimize-wb
.PHONY: load-wb-anatomy
load-wb-anatomy: owltools-build clear-load-log
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(ANATOMYONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(ANATOMY_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(ANATOMY_GAF)
	make message-load-clear
.PHONY: load-wb-disease
load-wb-disease: owltools-build clear-load-log
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(DISEASEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(DISEASE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general
	make message-load-clear
.PHONY: load-wb-go
load-wb-go: owltools-build clear-load-log
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(GOONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(GO_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general --solr-load-gafs $(GO_GAF)
	make message-load-clear
.PHONY: load-wb-lifestage	
load-wb-lifestage: owltools-build clear-load-log
	make message-load-start
	OWLTOOLS_MEMORY=$(OWLTOOLS_MAX_MEMORY) $(OWLTOOLS_ROOT)/OWLTools-Runner/bin/owltools $(LIFESTAGEONTOLOGY) $(OWLTOOLS_ONTOLOGY_PROCESSING_FLAGS) --solr-url $(LIFESTAGE_SOLR_URL) --solr-purge --solr-config $(ONTOLOGY_METADATA) --solr-log $(SOLR_LOAD_LOG) --solr-load-ontology --solr-load-ontology-general
	make message-load-clear
.PHONY: load-wb-phenotype	
load-wb-phenotype: owltools-build clear-load-log
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
