# iCatX API Specification

iCat API will be a REST API with Create, Read, and Update functionality over the content of the WHOFIC Foundation.

## API Endpoints

[Get projects](#getprojects) <br /> 
[Reading an entity](#readingentity) <br />
[Updating an entity](#updatingentity) <br />
[Adding a new entity](#addingentity) <br />
[Deleting an entity](#deletingentity) <br />
[Get children for an entity](#getchildren) <br />
[Comments for an entity](#comments) <br />
[Entities that have been updated since a certain time](#updatedentities) <br />
[Change History for a single entity](#changehistory) <br />
[Get linearization definitions](#getlindefs) <br /><br />


## Get projects <a name="getprojects"></a>

This endpoint will return a list of available projects with their metadata (id, title, description) for the requestor. The list may be constrained by access policies, i.e., a user may have read access only to certain projects.

` <baseUrl>/icat/projects/getProjects`

This call only supports GET.

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


## Reading an entity <a name="readingentity"></a>
GET request to the following endpoint will return **all the information on the entity both ontological and non-ontological** as a JSON object.

` <baseUrl>/icat/projects/{projectId}?entityIri={URL escaped entity URI} `

The history of changes and comments will not be included in this information. For that, use the `changeHistory` call.

### Returned object 
The returned object structure is defined in [this document](https://github.com/who-icatx/icatx-project/blob/main/docs/jsonForAPISpec.md).

All information such as textual properties, linearization definitions, postcoordination, logical definitions, etc. for the entity will be available in this object.

### Last-Modified HTTP response header
Last-Modified response header will be included in the response (it will contain the last time the entity is updated) in the format defined in the HTTP specification.


### ETag HTTP response header
ETag response header will be included in the response (it will contain a Hash of the JSON response or for performance reasons it could contain the Last Modification date & time).

### Not Found 404
If the entity does not exist in iCat http response code 404 will be returned.


## Updating an entity <a name="updatingentity"></a>
This call is used to update (i.e. write) the content of an entity in the WHOFIC Foundation.
Use the PUT request to the following endpoint with the JSON payload with the updated content (same format as returned in the GET request).

`<baseUrl>/icat/projects/{projectId}/entities`

The request body will contain the JSON structure of the entity, exactly how you receive it on the `getEntity` request, but with the new values to be set.

For example, if the definition of an entity needs to be updated, then the `label` from the `definition` structure should contain the new value for the definition. The `termId` should remain the same. First step is to do a `getEntity` request, then modify the `definition.label` and then send it as the JSON payload in the `update` request. The response of this call will return the updated JSON structure with the new definition value, with the same structure of the `getEntity` request. An abridged example of the JSON that is sent in the `update` request for the definition is shown below:

```JSON
        {
            "entityIRI": "http://id.who.int/icd/entity/1205958647",
            "languageTerms": {
                "title": {
                    "label": "Cholera due to Vibrio cholerae O1, biovar cholerae",
                    "termId": "http://who.int/icd#10305_735007d5_2555_4eb5_a762_282e008a1468"
                },
                "definition": {
                    "label": "This is the new definition that we changed via the API",
                    "termId": "http://www.example.org/RwdAFkGF7imWiOfjWpBm98"
                }
            ...
    }
 ```

When updating the language terms for an entity, if the `termId` is not specified, then we consider that a new `termId` needs to be created. The `termId` needs to be set as `null` or completely omitted from the JSON for a new `termId` to be created. 
If the `termId` is specified, then the update will change the label of that `termId` with the new value.

### Avoiding update conflicts
Before updating the entity, the system will check `If-Match` header of the request. The update will be performed only if the `If-Match` header matches the `ETag` of the entity. If it does not match, the API will return HTTP 412 Precondition failed response.

### Not Found 404
If the entity with the URI does not exist response code 404 will be returned.

### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- The content is not acceptable due to the business rules such as (entity cannot be it's parent). (We can discuss what basic checks could be added for this last type)


## Adding a new entity <a name="addingentity"></a>
POST request to the following endpoint with the JSON payload of the new entity. The POST request will contain only the title and one parent for the entity to be created. All other changes on the new entity (e.g., syns, narrower terms, linearizations, postcoordination, etc.) will be done via a PUT command, as defined above.

`<baseUrl>/icat/projects/{projectId}/createEntity`

The system will return the newly created object similar to the response for the `getEntity` request.

### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- Minimum information is not provided (title and at least one parent)
- The content is not acceptable due to other business rules 


## Deleting an entity <a name="deletingentity"></a>
The API does not need to support deletion as it could be performed as a move operation to the retired folder as it is done in the UI.


## Get children for an entity <a name="getchildren"></a>

This enpoint will return a list of ordered children of an entity.

` <baseUrl>/icat/projects/{projectId}/getChildren?entityIRI={URL escaped entity URI} `

This call will support only GET. Any updates to the entity, including the parents, should be done via the `update` call.

Returned JSON could be a simple array or URIs
```JSON
{
    "children": ["...", "..."]
}
```


## Comments for an entity <a name="comments"></a>
The GET request to the following endpoint will return the comments attached to the entity:

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
If the entity with the URI does not exist response code 404 will be returned.


## Entities that have been updated since a certain time <a name="updatedentities"></a>

The GET request to the following endpoint

` <baseUrl>/icat/history/changedEntities?projectId={projectId}&changedAfter={ISOdatetimeInUTC} `

This call will return URIs of all entities that have changed, added or deleted after a certain time (not including the changes that occurred at that exact time). 

* `updatedEntities`: list of URIs of entities that have changed after the provided time;
* `createdEntities`: list of URIs of entities that have been created after the provided time;
* `deletedEntities`: list of URIs of entities that have been deleted after the provided time. Normally we don't expect anything to be deleted as the deletions are performed by moves, but still there may be cases when we delete entities


An example response:

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

The GET request to the following endpoint will return the change history of the entity:

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
If the entity with the URI does not exist response code 404 will be returned.


## Get linearization definitions <a name="getlindefs"></a>

This endpoit will return the linearization definitions as they are used in iCAT-X. This is a static file that will rarely change (e.g., only if a new linearization is added, or an existing one is deleted). The response provides metadata about each linearization: the id, description, display label, sorting code, linearization mode (core or telescopic).

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
