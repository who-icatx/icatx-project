# iCatX API Specification

iCat API will be a REST API with Create, Read, and Update functionality over the content of the WHOFIC Foundation.

## API Endpoints

[Reading an entity](#readingentity) <br />
[Updating an entity](#updatingentity) <br />
[Adding a new entity](#addingentity) <br />
[Deleting an entity](#deletingentity) <br />
[Entities that have been updated since a certain time](#updatedentities) <br />
[Change History for a single entity](#changehistory) <br />
[Comments for an entity](#comments) <br />
[Get children for an entity](#getchildren) <br />
[Get projects](#getprojects) <br /> 
[Get linearization definitions](#getlindefs) <br /><br />


## Reading an entity <a name="readingentity"></a>
GET request to the following endpoint should return **all the information on the entity both ontological and non-ontological** as a JSON object.

` <baseUrl>/icat/projects/{projectId}?entityIri={URL escaped entity URI} `

The history of changes and comments should not be included in this information

### Returned object 
The returned object structure is defined in [this document](https://github.com/who-icatx/icatx-project/blob/main/docs/jsonForAPISpec.md).

All information such as textual properties, linearization definitions, postcoordination, logical definitions, etc. for the entity should be available in this object

### Last-Modified HTTP response header
Last-Modified response header should be included in the response (it should contain the last time the entity is updated) in the format defined in the HTTP specification


### ETag HTTP response header
ETag response header should be included in the response (it should contain a Hash of the JSON response or for performance reasons it could contain the Last Modification date & time ).

### Not Found 404
If the entity does not exist in iCat http response code 404 should be returned


## Updating an entity <a name="updatingentity"></a>
PUT request to the following endpoint with the JSON payload of the updated content (same format as returned in the GET request)

`<baseUrl>/icat/projects/{projectId}/entities`

The request body will contain the JSON structure of the entity exactly how you receive it on the getEntity request, but with the new values to be set.

```JSON
        {
            "entityIRI": "http://id.who.int/icd/entity/1205958647",
            "languageTerms": {
                "title": {
                    "label": "Cholera due to Vibrio cholerae O1, biovar cholerae",
                    "termId": "http://who.int/icd#10305_735007d5_2555_4eb5_a762_282e008a1468"
                },
                "definition": {
                    "label": "This is a short description for this disease",
                    "termId": "http://www.example.org/RwdAFkGF7imWiOfjWpBm98"
                },
                "longDefinition": {
                    "label": "Some aditional info",
                    "termId": "http://www.example.org/RB6hEJbIPRZmf452hQk0742"
                },
                "fullySpecifiedName": {
                    "label": "This is a test for json fetching",
                    "termId": "http://www.example.org/RBeDVm7VIGfiSExMRRtJqKG"
                },
                "baseIndexTerms": [
                    {
                        "label": "classical cholera",
                        "indexType": "Synonym",
                        "isInclusion": true,
                        "termId": "http://who.int/icd#IndexType.Synonym"
                    }
                ],
                "subclassBaseInclusions": [
                    "http://id.who.int/icd/entity/1959883044"
                ],
                "baseExclusionTerms": [
                    {
                        "label": "This isalternative label for exclusion",
                        "foundationReference": "http://id.who.int/icd/entity/1264126483",
                        "termId": ""
                    }
                ],
                "isObsolete": false
            },
            "entityLinearizations": {
                "suppressOtherSpecifiedResiduals": null,
                "suppressUnspecifiedResiduals": null,
                "unspecifiedResidualTitle": {
                    "label": null
                },
                "otherSpecifiedResidualTitle": {
                    "label": null
                },
                "linearizations": [
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "UNKNOWN",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/rar",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/research",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/ocu",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/mnh",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "UNKNOWN",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/oph",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/mus",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/ped",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "UNKNOWN",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/env",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "FALSE",
                        "linearizationPathParent": "http://id.who.int/icd/entity/257068234",
                        "linearizationId": "http://id.who.int/icd/release/11/mms",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/der",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "UNKNOWN",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/icd-o",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/pch",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/ner",
                        "codingNote": null
                    },
                    {
                        "isAuxiliaryAxisChild": "UNKNOWN",
                        "isGrouping": "FALSE",
                        "isIncludedInLinearization": "UNKNOWN",
                        "linearizationPathParent": "",
                        "linearizationId": "http://id.who.int/icd/release/11/pcl",
                        "codingNote": null
                    }
                ]
            },
            "postcoordination": {
                "postcoordinationSpecifications": [
                    {
                        "linearizationId": "ICHI",
                        "requiredAxes": [],
                        "allowedAxes": [],
                        "notAllowedAxes": [
                            "http://id.who.int/icd/schema/hasSeverity",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity1",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity2",
                            "http://id.who.int/icd/schema/course",
                            "http://id.who.int/icd/schema/temporalPatternAndOnset",
                            "http://id.who.int/icd/schema/timeInLife",
                            "http://id.who.int/icd/schema/causality",
                            "http://id.who.int/icd/schema/infectiousAgent",
                            "http://id.who.int/icd/schema/chemicalAgent",
                            "http://id.who.int/icd/schema/medication",
                            "http://id.who.int/icd/schema/hasCausingCondition",
                            "http://id.who.int/icd/schema/histopathology",
                            "http://id.who.int/icd/schema/laterality",
                            "http://id.who.int/icd/schema/relational",
                            "http://id.who.int/icd/schema/distribution",
                            "http://id.who.int/icd/schema/regional",
                            "http://id.who.int/icd/schema/specificAnatomy",
                            "http://id.who.int/icd/schema/serotype",
                            "http://id.who.int/icd/schema/genomicAndChomosomalAnomaly",
                            "http://id.who.int/icd/schema/fractureSubtype",
                            "http://id.who.int/icd/schema/fractureOpenOrClosed",
                            "http://id.who.int/icd/schema/jointInvolvementInFracture",
                            "http://id.who.int/icd/schema/typeOfInjury",
                            "http://id.who.int/icd/schema/extentOfBurnByBodySurface",
                            "http://id.who.int/icd/schema/extentOfFullThicknessBurnByBodySurface",
                            "http://id.who.int/icd/schema/outcomeOfFullThicknessBurn",
                            "http://id.who.int/icd/schema/durationOfComa",
                            "http://id.who.int/icd/schema/levelOfConsciousness",
                            "http://id.who.int/icd/schema/diagnosisConfirmedBy",
                            "http://id.who.int/icd/schema/hasManifestation",
                            "http://id.who.int/icd/schema/associatedWith"
                        ],
                        "overwrittenAllowedAxes": [],
                        "overwrittenRequiredAxes": [],
                        "overwrittenNotAllowedAxes": []
                    },
                    {
                        "linearizationId": "MMS",
                        "requiredAxes": [],
                        "allowedAxes": [],
                        "notAllowedAxes": [
                            "http://id.who.int/icd/schema/hasSeverity",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity1",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity2",
                            "http://id.who.int/icd/schema/course",
                            "http://id.who.int/icd/schema/temporalPatternAndOnset",
                            "http://id.who.int/icd/schema/timeInLife",
                            "http://id.who.int/icd/schema/causality",
                            "http://id.who.int/icd/schema/infectiousAgent",
                            "http://id.who.int/icd/schema/chemicalAgent",
                            "http://id.who.int/icd/schema/medication",
                            "http://id.who.int/icd/schema/hasCausingCondition",
                            "http://id.who.int/icd/schema/histopathology",
                            "http://id.who.int/icd/schema/laterality",
                            "http://id.who.int/icd/schema/relational",
                            "http://id.who.int/icd/schema/distribution",
                            "http://id.who.int/icd/schema/regional",
                            "http://id.who.int/icd/schema/specificAnatomy",
                            "http://id.who.int/icd/schema/serotype",
                            "http://id.who.int/icd/schema/genomicAndChomosomalAnomaly",
                            "http://id.who.int/icd/schema/fractureSubtype",
                            "http://id.who.int/icd/schema/fractureOpenOrClosed",
                            "http://id.who.int/icd/schema/jointInvolvementInFracture",
                            "http://id.who.int/icd/schema/typeOfInjury",
                            "http://id.who.int/icd/schema/extentOfBurnByBodySurface",
                            "http://id.who.int/icd/schema/extentOfFullThicknessBurnByBodySurface",
                            "http://id.who.int/icd/schema/outcomeOfFullThicknessBurn",
                            "http://id.who.int/icd/schema/durationOfComa",
                            "http://id.who.int/icd/schema/levelOfConsciousness",
                            "http://id.who.int/icd/schema/diagnosisConfirmedBy",
                            "http://id.who.int/icd/schema/hasManifestation",
                            "http://id.who.int/icd/schema/associatedWith"
                        ],
                        "overwrittenAllowedAxes": [],
                        "overwrittenRequiredAxes": [],
                        "overwrittenNotAllowedAxes": []
                    },
                    {
                        "linearizationId": "ICF",
                        "requiredAxes": [],
                        "allowedAxes": [],
                        "notAllowedAxes": [
                            "http://id.who.int/icd/schema/hasSeverity",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity1",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity2",
                            "http://id.who.int/icd/schema/course",
                            "http://id.who.int/icd/schema/temporalPatternAndOnset",
                            "http://id.who.int/icd/schema/timeInLife",
                            "http://id.who.int/icd/schema/causality",
                            "http://id.who.int/icd/schema/infectiousAgent",
                            "http://id.who.int/icd/schema/chemicalAgent",
                            "http://id.who.int/icd/schema/medication",
                            "http://id.who.int/icd/schema/hasCausingCondition",
                            "http://id.who.int/icd/schema/histopathology",
                            "http://id.who.int/icd/schema/laterality",
                            "http://id.who.int/icd/schema/relational",
                            "http://id.who.int/icd/schema/distribution",
                            "http://id.who.int/icd/schema/regional",
                            "http://id.who.int/icd/schema/specificAnatomy",
                            "http://id.who.int/icd/schema/serotype",
                            "http://id.who.int/icd/schema/genomicAndChomosomalAnomaly",
                            "http://id.who.int/icd/schema/fractureSubtype",
                            "http://id.who.int/icd/schema/fractureOpenOrClosed",
                            "http://id.who.int/icd/schema/jointInvolvementInFracture",
                            "http://id.who.int/icd/schema/typeOfInjury",
                            "http://id.who.int/icd/schema/extentOfBurnByBodySurface",
                            "http://id.who.int/icd/schema/extentOfFullThicknessBurnByBodySurface",
                            "http://id.who.int/icd/schema/outcomeOfFullThicknessBurn",
                            "http://id.who.int/icd/schema/durationOfComa",
                            "http://id.who.int/icd/schema/levelOfConsciousness",
                            "http://id.who.int/icd/schema/diagnosisConfirmedBy",
                            "http://id.who.int/icd/schema/hasManifestation",
                            "http://id.who.int/icd/schema/associatedWith"
                        ],
                        "overwrittenAllowedAxes": [],
                        "overwrittenRequiredAxes": [],
                        "overwrittenNotAllowedAxes": []
                    },
                    {
                        "linearizationId": "ICD-O",
                        "requiredAxes": [],
                        "allowedAxes": [],
                        "notAllowedAxes": [
                            "http://id.who.int/icd/schema/hasSeverity",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity1",
                            "http://id.who.int/icd/schema/hasAlternativeSeverity2",
                            "http://id.who.int/icd/schema/course",
                            "http://id.who.int/icd/schema/temporalPatternAndOnset",
                            "http://id.who.int/icd/schema/timeInLife",
                            "http://id.who.int/icd/schema/causality",
                            "http://id.who.int/icd/schema/infectiousAgent",
                            "http://id.who.int/icd/schema/chemicalAgent",
                            "http://id.who.int/icd/schema/medication",
                            "http://id.who.int/icd/schema/hasCausingCondition",
                            "http://id.who.int/icd/schema/histopathology",
                            "http://id.who.int/icd/schema/laterality",
                            "http://id.who.int/icd/schema/relational",
                            "http://id.who.int/icd/schema/distribution",
                            "http://id.who.int/icd/schema/regional",
                            "http://id.who.int/icd/schema/specificAnatomy",
                            "http://id.who.int/icd/schema/serotype",
                            "http://id.who.int/icd/schema/genomicAndChomosomalAnomaly",
                            "http://id.who.int/icd/schema/fractureSubtype",
                            "http://id.who.int/icd/schema/fractureOpenOrClosed",
                            "http://id.who.int/icd/schema/jointInvolvementInFracture",
                            "http://id.who.int/icd/schema/typeOfInjury",
                            "http://id.who.int/icd/schema/extentOfBurnByBodySurface",
                            "http://id.who.int/icd/schema/extentOfFullThicknessBurnByBodySurface",
                            "http://id.who.int/icd/schema/outcomeOfFullThicknessBurn",
                            "http://id.who.int/icd/schema/durationOfComa",
                            "http://id.who.int/icd/schema/levelOfConsciousness",
                            "http://id.who.int/icd/schema/diagnosisConfirmedBy",
                            "http://id.who.int/icd/schema/hasManifestation",
                            "http://id.who.int/icd/schema/associatedWith"
                        ],
                        "overwrittenAllowedAxes": [],
                        "overwrittenRequiredAxes": [],
                        "overwrittenNotAllowedAxes": []
                    }
                ],
                "scaleCustomizations": []
            },
            "logicalConditions": {
                "jsonRepresentation": {
                    "logicalDefinitions": [
                        {
                            "logicalDefinitionSuperclass": "http://id.who.int/icd/entity/257068234",
                            "relationships": [
                                {
                                    "axis": "http://id.who.int/icd/schema/hasSeverity",
                                    "filler": "http://id.who.int/icd/entity/815889539"
                                }
                            ]
                        }
                    ],
                    "necessaryConditions": [
                        {
                            "axis": "http://id.who.int/icd/schema/distribution",
                            "filler": "http://id.who.int/icd/entity/169306432"
                        },
                        {
                            "axis": "http://id.who.int/icd/schema/histopathology",
                            "filler": "http://id.who.int/icd/entity/411368752"
                        },
                        {
                            "axis": "http://id.who.int/icd/schema/infectiousAgent",
                            "filler": "http://id.who.int/icd/entity/194483911"
                        },
                        {
                            "axis": "http://id.who.int/icd/schema/infectiousAgent",
                            "filler": "http://id.who.int/icd/entity/194483911"
                        }
                    ]
                },
                "functionalRepresentation": {
                    "owlSyntax": "OWLFunctionalSyntax",
                    "axioms": [
                        "EquivalentClasses(<http://id.who.int/icd/entity/1205958647> ObjectIntersectionOf(<http://id.who.int/icd/entity/257068234> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/hasSeverity> <http://id.who.int/icd/entity/815889539>) ObjectSomeValuesFrom(<http://id.who.int/icd/schema/infectiousAgent> <http://id.who.int/icd/entity/194483911>)))",
                        "SubClassOf(<http://id.who.int/icd/entity/1205958647> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/distribution> <http://id.who.int/icd/entity/169306432>))",
                        "SubClassOf(<http://id.who.int/icd/entity/1205958647> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/infectiousAgent> <http://id.who.int/icd/entity/194483911>))",
                        "SubClassOf(<http://id.who.int/icd/entity/1205958647> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/histopathology> <http://id.who.int/icd/entity/411368752>))",
                        "SubClassOf(<http://id.who.int/icd/entity/1205958647> ObjectSomeValuesFrom(<http://id.who.int/icd/schema/infectiousAgent> <http://id.who.int/icd/entity/194483911>))"
                    ]
                }
            },
            "parents": [
                "http://id.who.int/icd/entity/257068234",
                "http://id.who.int/icd/entity/487269828"
            ]
        }
```

When updating languageTerms for an entity if termId is not specified then we consider that a new termId needs to be created. The termId needs to be set as null or completely omitted from the JSON for a new termId to be created. 
If the termId is specified then the update will change the label of that termId with the new value.

### Avoiding update conflicts
Before updating the entity, the system should check `If-Match` header of the request. The update should be performed only if the `If-Match` header matches the `ETag` of the entity. If it does not match, the API should return HTTP 412 Precondition failed response

### Not Found 404
If the entity with the URI does not exist response code 404 should be returned

### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- The content is not acceptable due to the business rules such as (entity cannot be it's parent). (We can discuss what basic checks could be added for this last type)


## Adding a new entity <a name="addingentity"></a>
POST request to the following endpoint with the JSON payload of the new entity. The POST request will contain only the title and one parent for the entity to be created. All other changes on the new entity (e.g., syns, narrower terms, linearizations, postcoordination, etc.) will be done via a PUT command, as defined above.

`<baseUrl>/icat/projects/{projectId}/createEntity`

The system should return the newly created object similar to the response for the GET request

### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- Minimum information is not provided (title and at least one parent)
- The content is not acceptable due to other business rules 

## Deleting an entity <a name="deletingentity"></a>
The API does not need to support deletion as it could be performed as a move operation to the retired folder as it is done in the UI

## Entities that have been updated since a certain time <a name="updatedentities"></a>
GET request to the following endpoint

` <baseUrl>/icat/history/changedEntities?projectId={projectId}&changedAfter={ISOdatetimeInUTC} `

This should return URIs of all entities that have changed, added or deleted after a certain time (not including the changes that occurred at that exact time). 
* `updatedEntities`: list of URIs of entities that have changed after the provided time;
* `createdEntities`: list of URIs of entities that have been created after the provided time;
* `deletedEntities`: list of URIs of entities that have been deleted after the provided time. Normally we don't expect anything to be deleted as the deletions are performed by moves, but still there may be cases when we delete entities


Response should look like:

```JSON
{
    "createdEntities": [
        "http://id.who.int/icd/entity/000000002",
        "http://id.who.int/icd/entity/000000011"
    ],
    "updatedEntities": [
        "http://id.who.int/icd/entity/000000027",
        "http://id.who.int/icd/entity/000000028"
    ],
    "deletedEntities": [
        "http://id.who.int/icd/entity/000000013"
    ]
}
```

## Change History for a single entity <a name="changehistory"></a>
GET request to the following endpoint should  return the change history of the entity
` <baseUrl>/icat/history/entityHistorySummary?projectId={projectId}&entityIRI={URL escaped entity URI} `

```JSON
{
    "changes": [
        {
            "changeSummary": "Update parents through API",
            "userId": "service-account-icatx_application",
            "dateTime": "2024-11-22T13:51:40.828"
        },
        ...
        {
            "changeSummary": "Created class api created entity 8 as a subclass of Birth injury due to scalpel wound",
            "userId": "service-account-icatx_application",
            "dateTime": "2024-11-22T13:31:51.596"
        }
    ]
}
```


### Not Found 404
If the entity with the URI does not exist response code 404 should be returned

## Comments for an entity <a name="comments"></a>
GET request to the following endpoint should  return the comments attached to the  entity
` <baseUrl>/icat/projects/{projectId}/entityComments/entityIRI={URL escaped entity URI} `

```JSON
    {
        "commentThreads": [
            {
                "projectId": "03a3f282-8671-45bf-901e-362e0e1ac3e2",
                "entityIRI": "http://who.int/icd#ICDEntity",
                "status": "CLOSED",
                "comments": [
                    {
                        "createdBy": "soimugeo",
                        "createdAt": "2024-11-14T14:16:30.673Z",
                        "updatedAt": null,
                        "body": "geoo thread"
                    },
                    {
                        "createdBy": "soimugeo",
                        "createdAt": "2024-11-14T14:16:38.191Z",
                        "updatedAt": "2024-11-15T14:08:40.097Z",
                        "body": "response updated"
                    }
                ]
            },
            {
                "projectId": "03a3f282-8671-45bf-901e-362e0e1ac3e2",
                "entityIRI": "http://who.int/icd#ICDEntity",
                "status": "OPEN",
                "comments": [
                    {
                        "createdBy": "soimugeo",
                        "createdAt": "2024-11-15T14:07:19.116Z",
                        "updatedAt": "2024-11-15T14:09:00.788Z",
                        "body": "asd some other thread updated"
                    }
                ]
            }
        ]
    }
```

### Not Found 404
If the entity with the URI does not exist response code 404 should be returned

## Get children for an entity <a name="getchildren"></a>

This enpoint should return a list of ordered children of an entity.

` <baseUrl>/icat/projects/{projectId}/getChildren?entityIRI={URL escaped entity URI} `

This should support only GET so that the updates are only done by using the main entity endpoint.

Returned JSON could be a simple array or URIs
```JSON
{
    "children": ["...", "..."]
}
```

## Get projects <a name="getprojects"></a>

This endpoint will return a list of available projects with their metadata (id, title, description) for the requestor. The list may be constrained by access policies, i.e., a user may have read access only to certain projects.

` <baseUrl>/icat/projects/getProjects`

This should support only GET.

Example for returned JSON:

```JSON
{
    "projects": [
        {
            "id": "8cc2df91-d42f-441e-b586-0d502af60193",
            "title": "WHOFIC Foundation v3.1",
            "description": "This is the WHOFIC Foundation as of May 30, 2024 and it is used for testing."
        },
        {
            "id": "61f24481-8df3-4591-8a9c-a49702a33a21",
            "title": "ICD Parasitic + ICF Mental + ICHI Target Mental v3",
            "description": "This is the parasitic ICD + mental ICF + mental target ICHI + label = annotation property."
        }
    ]
}
```

## Get linearization definitions <a name="getlindefs"></a>

This endpoit will return the linearization definitions as they are used in iCAT-X. This is a static file that will rarely change (e.g., only if a new linearization is added, or an existing one is deleted). It provides metadata about each linearization: the id, description, display label, sorting code, linearization mode (core or telescopic).

` <baseUrl>/icat/linearization-definitions`

Example for returned JSON:

```JSON
{
        "Id": "MMS",
        "whoficEntityIri": "http://id.who.int/icd/release/11/mms",
        "oldId": null,
        "Description": "ICD-11 for Mortality and Morbidity Statistics",
        "DisplayLabel": "MMS",
        "rootId": "http://id.who.int/icd/entity/455013390",
        "sortingCode": "01",
        "linearizationMode": "LinMode.Basic",
        "coreLinId": null
    },
    {
        "Id": "PCL",
        "whoficEntityIri": "http://id.who.int/icd/release/11/pcl",
        "oldId": null,
        "Description": "ICD-11 Primary Care Low Resource Setting Linearization",
        "DisplayLabel": "Primary Care - Low Res. Set.",
        "rootId": "http://id.who.int/icd/entity/455013390",
        "sortingCode": "03",
        "linearizationMode": "LinMode.TelescopicFromAnotherLinearization",
        "coreLinId": "MMS"
    },
    ...
}
```
