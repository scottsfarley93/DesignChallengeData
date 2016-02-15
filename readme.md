Welcome to the 2016 Design Challenge!
======================================

Introduction
------------------

##The Task
This dataset describes the occurrence of selected vascular plant and mammal in North America between 22,000 and 0 years before the present.  This data has been used to trace trends in space (e.g., species range at a single time slice), trends through time (e.g., fossil pollen abundance at a particular spatial location through time), and trends in attribute (e.g., species richness).  Previous studies and 
visualizations have primarily focused on a single one of these dimensions.  Your task is to come up with innovative, unqiue, creative and asthetically pleasing visualizations capable of communicating spatiotemporal patterns in highly multidimensional space.  The remainder of this document will introduce the datasets and its origins and try to clarify the fields in the data files.
Still have questions?  Scott Farley, who culled the dataset from other sources, will be on hand throughout the day on Saturday to answer any questions that you may have.
  

##Where does the data come from?
This data comes from the [Neotoma paleoecological database](http://neotomadb.org), a project dedicated to sharing paleoecological data so that users can easily find, aggregate, explore, and analyze our current understanding of paleoenvironments.  NeotomaDB is composed of thousands of individual studies that report on the relative concentrations of
macro- and micro-fossils and particular spatial locations.  PMost often, the plant datasets are derived from fossil pollen studies, which link concentrations of fossilized pollen to depths within a sediment core, and subsequently to ages (years before present).  The mammals datasets are more often obtained 
by exacation of a macrofossil, which is subsequently dated, often by using radiometric dating methods.  

Conceptual description vascular plant dataset:  
	* Plants grow and produce pollen
	* Pollen is dispersed by wind, insects, or other animals
	* Pollen is deposited on a nearby lake or within a watershed and subsequently washed into the lake
	* Pollen settles and is mixed into the sediment on the bottom of the lake
	* As time passes, the process continues, and new layers of pollen and sediment are deposited
	* In the present day, a scientist (like Jack Williams), takes a sediment core that takes a continuous sample of the sediment at the bottom of the lake
	* The core is then split into small samples (1 cm)
	* Each of these samples is linked to an age by using an empirical function that links each depth to an age (called an age to depth model)
	* Each sample is then subjected to lab analyses that include identifying the species of each pollen grain within the sample
	* Ecological implications are published in the scientific literature and the pollen counts uploaded to NeotomaDB

Conceptual description of mammal dataset:  
	* A mammal (like a woolly mammoth) lives and dies at some point in the past
	* If the body of this mammal is deposited in a suitable location, it will be fossilized
	* In the present day, a scientist uncovers some portion of the fossil
	* This fossil can be dated using radiometric techniques that give an estimate of the age and its uncertainty
	* Ecological implications are published and the locations in space and time of the fossil are uploaded to NeotomaDB

Data Types
----------
Data is provided as esri shapefiles and as csv text files. The attributes and fields provided in each representation is the same. 

Metadata
--------
Several files are provided to help you contextualize the given dataset.  These include a general reference list, and lookup table of common names and a lookup table given the taxonomic hierarchy for each taxon.

## Main.csv
This file gives a listing of the taxa included within the given data sets. 
Fields: 
 
	* Taxon Name:  The scientific (latin) name of the taxon
	* numOccurrences:  The number of records each taxon has (and that you can expect to find within that data file).  This can be used to prioritize "important" species.
	* fileName: A relative path to the file from either the shapefile or the csv data directory.

##Common.csv
This file provides a bridge between the scientific and common/english name of a taxon.
Fields:

	* Taxon  Name: The scientific name of the species (as can be found in main.csv)
	* Common names:  These are possible matches given by the itis.gov service.  Some types have no common names, some have many.  The names are designed to provide context, and it may be beneficial to check wikipedia or another source if an exact match is required.
	
	
##Taxonomy.csv
This file enables finding patterns between higher groups of taxa (families, orders, etc).  Some taxa have more detailed hierarchies (i.e., sub-orders) however, most are complete down to the familiy level, and some go all the way from kingdom to species.  Again, a trip to wikipedia may be helpful here.
Fields:

	* Taxon Name: The scientific name of the the taxon
	* Taxonomy:  The following fields describe the taxonomic hierarchy of the species from most general (kingdom) to most specific (species).  Completeness varies.



Data Fields
-----------
Both the csv and the shapefiles contain the same fields.  Both the mammal and plant taxa have the same field names.  Not all fields will be populated for each taxon, however, every taxon should have, at a minimum, spatial (x/y) coordinates and a value for that taxon at that location.  Most records also include an age (or min/max ages given dating uncertainty) and some include the depth where the species was found.  
NOT ALL RECORDS IN A SINGLE TAXA FILE CONTAIN THE SAME VARIABLES.  This is especially important for mammal species, where some records report the presence/absence of a species, while other report the minimum number of individuals (MNI) found at that site, while still others report the number of specimens present (NISP).  It is recommended taht you ensure that you are using the same variable unit when comparing across taxa.


Fields:

	* siteID:  This is an integer field that represents the site identifier as specified by the database we used to obtain the data.  It is not essential, however, for the intrrepid data explorer, it can be used to link specimens at single sites in a more exact way than say, a spatial join.
	* siteName: The textual name of the site where the specimen was found or the core taken.
	* lng: The longitude (x-coordinate in WGS1984) of the specimen).  This is the mean of the bounding box longitudes.
	* lat: The latitude (y-coordinate in WGS1984) of the specimen.  This is the mean of the bounding box latitudes.
	* latN: The northern coordinate of the bounding box of the site
	* latS: The southern coordianate of the bounding box of the site
	* lngE: The eastern coordinate of the bounding box of the site
	* lngW: The western coordinate of the bounding box of the site
	* taxaGroup:  The group to which this taxa belongs, either vascular plants or mammals
	* taxonName: the scientific name of the taxon
	* value: The value of the record for that taxon at that space-time location
	* variableUnit: The unit in which the value is measured
		** Possible values:
		* NISP: Number of Identified Specimens -- the raw number of specimens identified at that level
		* MNI: Minimum number of individuals -- the fewest possible number of organisms in a skeletal assemblage
		* present/absent: Boolean -- 1 if present
	* element:  The type of material used to generate the value 
		** Possible Values:
		* Bone/Tooth -- for most mammals
		* Spore -- for pollen
		* macrofossil -- for plant macrofossils
	* context: The taphonomic context of the record (few records have this attribute)
	* age: The age of this record.  Most plant taxa have this attribute, as generated by an age-depth model.  Most mammal species use the uncertainty bounds.  
	* minAge: The minimum age (young) of the record as generated by uncertainty in the dating procedure
	* maxAge: The maximum age (old) of the record as generated by uncertainty in the dating procedure
	* ageType: The type of date used.  This can be calendar years ad/bc, calendar years bp,  calibrated radiocarbon years bp, radiocarbon years bp, or varve years bp.  
	* unitDepth: The depth below the surface that the specimen was found.  Most plant taxa have this attribute, most mammals do not.  The depth attribute is less meaningful than the age attribute because ages can be compared across sites.
	* altitude: The altitude of the site.  Again, most plant species have this attribute, while fewer mammal species contain this field.  This field could be easily generated in GIS too.
	* datasetType: A textual description of the type of data contained in that record
	* submitted: The date that the record was integrated into the database.  Generally not a useful field.
	For plant taxa only:
	* pollenSum: The summation of all pollen in that level of the specimen unit. 
	* pollen Pct: The percentage of this taxon in relation to all other taxa in that level, calcualted using the pollenSum attribute.  This attribute is more directly comparable across taxa than the value attribute due to counting procedures as is typically used in the paleoecological literature.

	
	