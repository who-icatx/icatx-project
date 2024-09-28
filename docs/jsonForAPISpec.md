# JSON Specification for the iCAT-X API

This document specifies the JSON format used by the [iCAT-X API](https://github.com/who-icatx/icatx-project/blob/main/docs/icatAPISpecs.md).

## Reading an entity
GET request to the following endpoint should return **all the information on the entity both ontological and non-ontological** as a JSON object.

` <baseUrl>/icat/entity/<URL escaped entity URI> `

#### Returned object 
Returned object  will look like

```json

{
    "whoficEntityIri": "http://id.who.int/icd/entity/257068234",
    
    "parents": [
        "http://id.who.int/icd/entity/1776745893",
        "http://id.who.int/icd/entity/367882675"],
    
    "languageTerms": {
    
        "title" : {
            "label": "Title 1",
            "termId": "http://who.int/icd#TitleTerm_716"
        },
        
        "fullySpecifiedName" : {
            "label": "Fully specified name 1",
            "termId": "http://who.int/icd#TitleTerm_717"
        },
        
        "definition" : {
            "label": "Definition 1",
            "termId": "http://who.int/icd#Term_718"
        },
        
        "longDefinition" : {
            "label": "Long definition 1",
            "termId": "http://who.int/icd#Term_719"
        },
        
        "baseIndexTerms": [
            {
                "label": "Syonym 1",
                "indexType": "Synonym",
                "isInclusion": "true",
                "termId": "http://who.int/icd#Term_720"
            },
            {
                "label": "Narrower 1",
                "indexType": "Narrower",
                "isInclusion": "false",
                "termId": "http://who.int/icd#Term_721"
            }
        ],
        
        "subclassBaseInclusions": [
            "http://id.who.int/icd/entity/1776745893",
            "http://id.who.int/icd/entity/367882675",
            "http://id.who.int/icd/entity/974967764"
        ],
        
        "baseExclusionTerms": [
            {
                "label": "Alternate exclusion label 1",
                "foundationReference": "http://id.who.int/icd/entity/1851734799",
                "termId": "http://who.int/icd#Term_720"
            },
            {
                "label": "Alternate exclusion label 2",
                "termId": "http://who.int/icd#Term_721"
            },
            {
                "foundationReference": "http://id.who.int/icd/entity/257068234",
                "termId": "http://who.int/icd#Term_722"
            }
        ],
        
        "isObsolete": "false"
     
    },

    "whoficEntityLinearizations": 
        {
            "suppressUnspecifiedResiduals": "true",
            "suppressOtherSpecifiedResiduals": "false",
            "otherSpecifiedResidualTitle": {
                "label": "Other specified Dengue" 
            },
         
          "linearizations": [
            {
              "isAuxiliaryAxisChild": "false",
              "isGrouping": "false",
              "isIncludedInLinearization": "true",
              "linearizationParent": "http://id.who.int/icd/entity/921595235",
              "linearizationView": "http://id.who.int/icd/release/11/mms"
            },
            {
              "isAuxiliaryAxisChild": "false",
              "isGrouping": "false",
              "isIncludedInLinearization": "unknown",
              "linearizationParent": "http://id.who.int/icd/entity/921595235",
              "linearizationView": "http://id.who.int/icd/release/11/der"
            }
          ]
        },
        
    "postcoordination": {
        
      "postcoordinationSpecifications": [
        {
        "requiredAxes": [
            "http://id.who.int/icd/schema/associatedWith",
            "http://id.who.int/icd/schema/infectiousAgent"
          ],
          "linearizationView": "http://id.who.int/icd/release/11/mms"
        },
        {
          "allowedAxes": [
            "http://id.who.int/icd/schema/hasManifestation",
            "http://id.who.int/icd/schema/temporalPatternAndOnset"
          ],
          "linearizationView": "http://id.who.int/icd/release/11/ner"
        },
        {
          "linearizationView": "http://id.who.int/icd/release/11/research"
        },
        {
          "linearizationView": "http://id.who.int/icd/release/11/der"
        }
      ],
      
       "scaleCustomizations": [
        {
          "postcoordinationScaleValues": [
            "http://id.who.int/icd/entity/1882742628"
          ],
          "postcoordinationAxis": "http://id.who.int/icd/schema/associatedWith"
        },
        {
          "postcoordinationScaleValues": [
            "http://id.who.int/icd/entity/1434326374"
          ],
          "postcoordinationAxis": "http://id.who.int/icd/schema/hasManifestation"
        },
        {
          "postcoordinationScaleValues": [
            "http://id.who.int/icd/entity/83217129"
          ],
          "postcoordinationAxis": "http://id.who.int/icd/schema/infectiousAgent"
        }
      ]
      
    },
    
    "logicalDefinitions": [
        {
            "logicalDefinitionSuperclass": "http://id.who.int/icd/entity/1434326374",
            "relationships": [
                {
                    "axis":"http://id.who.int/icd/schema/infectiousAgent",
                    "filler":"http://id.who.int/icd/entity/1434326374"
                },
                {
                    "axis":"http://id.who.int/icd/schema/associatedWith",
                    "filler":"http://id.who.int/icd/entity/83217129"
                }
            ]
        },
        {
            "logicalDefinitionSuperclass": "http://id.who.int/icd/entity/1435646374",
            "relationships": [
                {
                    "axis":"http://id.who.int/icd/schema/hasManifestation",
                    "filler":"http://id.who.int/icd/entity/1434323374"
                }
            ]
        }
    ],
    
    "necessaryConditions": [
        {
            "axis":"http://id.who.int/icd/schema/infectiousAgent",
            "filler":"http://id.who.int/icd/entity/1434326322"
        },
        {
            "axis":"http://id.who.int/icd/schema/specificAnatomy",
            "filler":"http://id.who.int/icd/entity/83217134"
        },
        {
            "axis":"http://id.who.int/icd/schema/temporalPatternAndOnset",
            "filler":"http://id.who.int/icd/entity/1434323378"
        }
    ]
}

```
