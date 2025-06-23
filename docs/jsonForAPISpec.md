# JSON Specification for the iCAT-X API

This document specifies the JSON format used by the [iCAT-X API](https://github.com/who-icatx/icatx-project/blob/main/docs/icatAPISpecs.md).

## Reading an entity
GET request to the following endpoint should return **all the information on the entity both ontological and non-ontological** as a JSON object.

` <baseUrl>/icat/entity/<URL escaped entity URI> `

#### Returned object 
Returned object  will look like

```json
{
    "entityURI": "http://id.who.int/icd/entity/1205958647",

    "isObsolete": "false",
    
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
            },
            {
                "label": "Syonym 2",
                "indexType": "Synonym",
                "isInclusion": "true",
                "termId": "http://who.int/icd#Term_725",
                "isDeprecated": "true"
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
        ]
    },

    "diagnosticCriteria": "This is a diagnostic criteria in **markdown format**.",

    "entityLinearizations": 
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
              "linearizationPathParent": "http://id.who.int/icd/entity/921595235",
              "linearizationId": "mms"
            },
            {
              "isAuxiliaryAxisChild": "false",
              "isGrouping": "false",
              "isIncludedInLinearization": "unknown",
              "linearizationPathParent": "http://id.who.int/icd/entity/921595235",
              "linearizationId": "der"
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
          "linearizationId": "mms"
        },
        {
          "overwrittenAllowedAxes": [
            "http://id.who.int/icd/schema/specificAnatomy",
            "http://id.who.int/icd/schema/laterality"
          ],
          "overwrittenRequiredAxes": [
            "http://id.who.int/icd/schema/hasManifestation",
            "http://id.who.int/icd/schema/temporalPatternAndOnset"
          ],
          "overwrittenNotAllowedAxes": [
             "http://id.who.int/icd/schema/causality",
             "http://id.who.int/icd/schema/severity"
          ],
          "linearizationId": "ner"
        },
        {
          "linearizationId": "research"
        },
        {
          "linearizationId": "der"
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
    
    "logicalConditions": {
        
        "logicalConditionsSimplified": {
            "logicalDefinitions": [
                {
                    "logicalDefinitionSuperclass": "http://id.who.int/icd/entity/1776745893",
                    "relationships": [
                        {
                            "axis":"http://id.who.int/icd/schema/infectiousAgent",
                            "filler":"http://id.who.int/icd/entity/1434326373"
                        },
                        {
                            "axis":"http://id.who.int/icd/schema/associatedWith",
                            "filler":"http://id.who.int/icd/entity/83217129"
                        }
                    ]
                },
                {
                    "logicalDefinitionSuperclass": "http://id.who.int/icd/entity/367882675",
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
        },
        
        "logicalConditionsOwl": {
            "owlSyntax":"OWLFunctionalSyntax",
            "aximos": [ 
                "EquivalentClasses(<http://id.who.int/icd/entity/1205958647> ObjectIntersectionOf(<http://id.who.int/icd/entity/1776745893> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/infectiousAgent> <http://id.who.int/icd/entity/1434326373>) ObjectSomeValuesFrom(<http://id.who.int/icd/schema/associatedWith> <http://id.who.int/icd/entity/83217129>)))",
                "EquivalentClasses(<http://id.who.int/icd/entity/1205958647> ObjectIntersectionOf(<http://id.who.int/icd/entity/367882675> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/hasManifestation> <http://id.who.int/icd/entity/1434323374>)))",
                "SubClassOf(<http://id.who.int/icd/entity/1205958647> <http://id.who.int/icd/entity/1776745893>)",
                "SubClassOf(<http://id.who.int/icd/entity/1205958647> <http://id.who.int/icd/entity/367882675>)",
                "SubClassOf(ObjectSomeValuesFrom(<http://id.who.int/icd/schema/infectiousAgent> <http://id.who.int/icd/entity/194483911>))",
                "SubClassOf(ObjectSomeValuesFrom(<http://id.who.int/icd/schema/specificAnatomy> <http://id.who.int/icd/entity/83217134>))",
                "SubClassOf(ObjectSomeValuesFrom(<http://id.who.int/icd/schema/temporalPatternAndOnset> <http://id.who.int/icd/entity/1434323378>))"
            ]
        }
    }
}

```


**Notes about the postcoordination axes representation:**

*For base/core linearizations*: we list only axes that are `allowed` or `required` (i.e., skip `notAllowed`).

*For telescopic linearizations*: we list only the ones that overwrite the base linearization. These can be `allowed`, `required`, or `notAllowed`.

To make this clear, may be we could use `overwrittenAllowedAxes`, `overwrittenRequiredAxes`, and `overwrittenNotAllowedAxes` in the telescopic linearization definitions not to have the confusion with the `allowedAxes`, `requiredAxes` used in the base/core linearization definitions.

