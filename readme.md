Welcome to the 2016 Design Challenge!
======================================

Introduction
------------------

##The Task
This dataset describes the occurrence of selected vascular plant and mammal in North America between the [last Glacial Maximum (LGM ~21,000 years ago)] (https://en.wikipedia.org/wiki/Last_Glacial_Maximum) and the present.  To date, this data has been used to trace trends in space (e.g., species range at a single time slice), trends through time (e.g., fossil pollen abundance at a particular spatial location through time), and trends in attribute (e.g., species richness).  Previous studies and 
visualizations have primarily focused on a single one of these dimensions.  Your task is to come up with innovative, unique, creative and aesthetically pleasing visualizations capable of communicating spatiotemporal patterns in highly multidimensional space.  The changes that the earth and its ecosystems have undergone in the last 22,000 years can be helpful in understanding how the earth will change under anthropogenic climate warming.  
New ways to visualize past responses to climate change, and in particular, the trends hidden within this dataset, are influential in helping people understanding the magnitude, direction, and heterogeneity of future changes in the earth's system.  

The remainder of this document will introduce the datasets and its origins and try to clarify the fields in the data files.
Still have questions?  Scott Farley, who organized this year's dataset, will be on hand throughout the day on Saturday to answer any questions that you may have.
  

##Where does the data come from?
This data comes from the [Neotoma paleoecological database](http://neotomadb.org), a project dedicated to sharing paleoecological data so that users can easily find, aggregate, explore, and analyze our current understanding of paleoenvironments.  NeotomaDB is composed of thousands of individual studies that report on the relative concentrations of
macro- and micro-fossils and particular spatial locations.  Most often, the plant datasets are derived from fossil pollen studies, which link concentrations of fossilized pollen to depths within a sediment core, and subsequently to ages (years before present).  The mammals datasets are more often obtained 
by excavation of a macrofossil, which is subsequently dated, often by using radiometric dating methods.  

Conceptual description vascular plant dataset:  

	* Plants grow and produce pollen
	* Pollen is dispersed by wind, insects, or other animals
	* Pollen is deposited on a nearby lake or within a watershed and subsequently washed into the lake
	* Pollen settles and is mixed into the sediment on the bottom of the lake
	* As time passes, the process continues, and new layers of pollen and sediment are deposited
	* In the present day, a scientist (like Jack Williams), takes a sediment core that takes a continuous sample of the sediment at the bottom of the lake
	* The core is then split into small samples (1 CM)
	* Each of these samples is linked to an age by using an empirical function that links each depth to an age (called an age to depth model)
	* Each sample is then subjected to lab analyses that include identifying the species of each pollen grain within the sample
	* Pollen counts are turned into relative abundances by comparing the number of pollen grains of a single taxa to the total of all found in that portion of the core. 
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
Several files are provided to help you contextualize the given dataset.  Mammals are more often able to be identified down to the species level, while most plant species, identified through pollen analysis are reported to the genus or even the family level.  Thus, the datasets and associated metadata differ for each group.

## Main.csv
Given for both plants and mammals, this file provides a general overview of the taxa provided in each group, the relative number of records for each taxa within the group, and a pointer to the files that contain the taxa's data.
Fields: 
 
	* Taxon Name:  The scientific (Latin) name of the taxon
	* numSites:  The number of x/y locations for this taxon.  
	* numRecords: The raw number of data points (in x, y, and z) for this taxon.  The number of sites and the number of records can bbe helpful in determining "important" taxa.
	* csv: The relative path to the csv file containing this dataset.
	* shapefile: The relative path to the shapefile containing this dataset.

##Common.csv
Provided only for mammals, this table provides a lookup for the common names of taxa to the English common name.  This file is provided to help you contextualize the dataset and the included taxa.  Plants are sometimes grouped to levels (like family) that do not have standard common names.  Simple google searches may yield informative common names for some plant taxa.
Fields:

	* Taxon  Name: The scientific name of the species (as can be found in main.csv)
	* Common names:  These are possible matches given by the itis.gov service.  Some types have no common names, some have many.  The names are designed to provide context, and it may be beneficial to check wikipedia or another source if an exact match is required. The order of these fields do not correspond to an ordered listed of preference in the common names. Thus, the name listed first in this list may be less likely to be the accepted common name than one later in the list.  
	
	
##Taxonomy.csv
Provded only for mammals, this file enables finding patterns between higher groups of taxa (families, orders, etc).  Some taxa have more detailed hierarchies (i.e., sub-orders) however, most are complete down to the family level, and some go all the way from kingdom to species.  Again, a trip to wikipedia may be helpful here.  
Fields:

	* Taxon Name: The scientific name of the the taxon
	* Taxonomy:  The following fields describe the taxonomic hierarchy of the species from most general (kingdom) to most specific (species).  Completeness varies.

Most mammal species have this general structure:

	* Kingdom
	* Phylum
	* Class
	* Order
	* Family
	* Genus
	* Extra -- an extra taxonomic field that describes another layer of hierarchy (e.g., sub-phylum, sub-class) at some point in the taxonomy

##PollenMap.csv
Designed only for the plant species, this file shows the method of aggregation to get to the higher taxa given in this dataset.  While there is no way to deconstruct (go to a higher level of identification in the taxonomic tree), this data may be interesting to those working with the plant data.
Fields:  

	* ID: The taxa id (not useful)
	* taxon: The taxon that has been subsumed
	* MappedTaxon: The new name for the higher level taxa given in the dataset.


Data Fields
-----------
Both the csv and the shapefiles contain the same fields.   Not all fields will be populated for each taxon, however, every taxon should have, at a minimum, spatial (x/y) coordinates and a value for that taxon at that location.  Most records also include an age (or min/max ages given dating uncertainty) and some include the depth where the species was found.  
NOT ALL RECORDS IN A SINGLE TAXA FILE CONTAIN THE SAME VARIABLES.  This is especially important for mammal species, where some records report the presence/absence of a species, while other report the minimum number of individuals (MNI) found at that site, while still others report the number of specimens present (NISP).  It is recommended that you ensure that you are using the same variable unit when comparing across taxa.
Other attributes that may be difficult to compare across are different [age types] (https://en.wikipedia.org/wiki/Before_Present): Radiocarbon Years B.P., Calendar years B.P, etc. however, for this exercise you may assume that all ages are comparable.  


Mammal Fields:

	* siteID:  This is an integer field that represents the site identifier as specified by the database we used to obtain the data.  It is not essential, however, for the intrepid data explorer, it can be used to link specimens at single sites in a more exact way than say, a spatial join.
	* siteName: The textual name of the site where the specimen was found.
	* lng: The longitude (x-coordinate in WGS1984) of the specimen).  This is the mean of the bounding box longitudes.
	* lat: The latitude (y-coordinate in WGS1984) of the specimen.  This is the mean of the bounding box latitudes.
	* latN: The northern coordinate of the bounding box of the site
	* latS: The southern coordinate of the bounding box of the site
	* lngE: The eastern coordinate of the bounding box of the site
	* lngW: The western coordinate of the bounding box of the site
	* taxaGroup:  The group to which this taxa belongs
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
	* context: The taphonomic context of the record (few records have this attribute)
	* age: The age of this record.  Most plant taxa have this attribute, as generated by an age-depth model.  Most mammal species use the uncertainty bounds.  
	* minAge: The minimum age (young) of the record as generated by uncertainty in the dating procedure
	* maxAge: The maximum age (old) of the record as generated by uncertainty in the dating procedure
	* ageType: The type of date used.  This can be calendar years ad/BC, calendar years BP,  calibrated radiocarbon years BP, radiocarbon years BP, or varve years BP.  
	* unitDepth: The depth below the surface that the specimen was found.  Most plant taxa have this attribute, most mammals do not.  The depth attribute is less meaningful than the age attribute because ages can be compared across sites.
	* altitude: The altitude of the site.  Again, most plant species have this attribute, while fewer mammal species contain this field.  This field could be easily generated in GIS too.
	* datasetType: A textual description of the type of data contained in that record
	** Possible values
		* vertebrate fauna	
	* submitted: The date that the record was integrated into the database.  Generally not a useful field.

Plant Fields:  

	* siteName: The textual name of the site where the pollen core was taken.
	* lng: The longitude (x-coordinate in WGS1984) of the core.  
	* lat: The latitude (y-coordinate in WGS1984) of the core.  
	* ageYouner: The minimum age (young) of the record as generated by uncertainty in the dating procedure
	* ageolder: The maximum age (old) of the record as generated by uncertainty in the dating procedure
	* age: The best dated age of this record. Some species may only have this field, others may only use the min/max ages
	* ageType: The type of date used.  This can be calendar years ad/BC, calendar years BP,  calibrated radiocarbon years BP, radiocarbon years BP, or varve years BP.  
	* taxonName: the scientific name of the taxonomic grouping. Refer to pollenMap if you want to know what this grouping is made up of.
	* value: The raw value of the record for that taxon at that space-time location
	* Pct: The relative abundance of this taxon compared to all others found at that space-time location.  This is a much more meaningful field than the raw value, because it is directly comparable across records.
	* Depth: The depth below the surface that the record was taken.  Most plant taxa have this attribute.  The depth attribute is less meaningful than the age attribute because ages can be compared across sites.
	* handle: The dataset identifier for the site's age basis.  Used in data preparation, generally not a useful field for this exercise.