# iCatX API Specification

iCat API will be a REST API with Create, Read, and Update functionality over the content of the WHOFIC Foundation.

## API Endpoints

### Reading an entity
GET request to the following endpoint should return **all the information on the entity both ontological and non-ontological** as a JSON object.

` <baseUrl>/icat/entity/<URL escaped entity URI> `

The history of changes and comments should not be included in this information

#### Returned object 
Returned object  will look like

```json
{
    "ontologicalInfo": {
        

    },
    "nonOntologicalInfo": {
        
    }
}
```

All information such as textual properties, linearization definitions, postcoordination, logical definitions, etc. for the entity should be available in this object

Further discussion is needed on deciding how to structure the ontological information and non-ontological information in the JSON object. Existing formats being used in the iCatX software could be used especially for the non-ontological information. 

#### Last-Modified HTTP response header
Last-Modified response header should be included in the response (it should contain the last time the entity is updated) in the format defined in the HTTP specification


#### ETag HTTP response header
ETag response header should be included in the response (it should contain a Hash of the JSON response or for performance reasons it could contain the Last Modification date & time ).

#### Not Found 404
If the entity does not exist in iCat http response code 404 should be returned


### Updating an entity
PUT request to the following endpoint with the JSON payload of the updated content (same format as returned in the GET request)

`<baseUrl>/icat/entity/<URL escaped entity URI>`


#### Avoiding update conflicts
Before updating the entity, the system should check `If-Match` header of the request. The update should be performed only if the `If-Match` header matches the `ETag` of the entity. If it does not match, the API should return HTTP 412 Precondition failed response

#### Not Found 404
If the entity with the URI does not exist response code 404 should be returned

#### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- The content is not acceptable due to the business rules such as (entity cannot be it's parent). (We can discuss what basic checks could be added for this last type)


### Adding a new entity
POST request to the following endpoint with the JSON payload of the new entity.

`<baseUrl>/icat/entity`

The system should return the newly created object similar to the response for the GET request

#### Bad Request 400
If the content of the entity does not meet the requirements. The server will return 400 Bad Request response

This can be because :
- Payload is not a well formed JSON
- It's not in the structure expected by the system
- Minimum information is not provided (title and at least one parent)
- The content is not acceptable due to other business rules 

### Deleting an entity
The API does not need to support deletion as it could be performed as a move operation to the retired folder as it is done in the UI

### Entities that have been updated since a certain time
GET request to the following endpoint

` <baseUrl>/icat/entityChanges?changedAfter={ISOdatetimeInUTC} `

This should return URIs of all entities that have changed, added or deleted after a certain time (not including the changes that occurred at that exact time). 

Response should look like:

```json
{
    updatedEntities: [
        //list of URIs of entities that have changed after the provided time.
    ],
    createdEntities: [
            //list of URIs of entities that have been created after the provided time.
    ],
    deletedEntities:[
            //list of URIs of entities that have been deleted after the provided time.
            //normally we don't expect anything to be deleted as the deletions are performed by moves but still there may be cases when we delete entities

    ]
}
```

### Change History for a single entity
GET request to the following endpoint should  return the change history of the entity
` <baseUrl>/icat/changehistory/<URL escaped entity URI> `

We could discuss how to structure the change history information. Existing formats being used in the iCatX software could be used here. At a minimum, the following should be included.
- Textual representation of the change
- Name of the user who made the change
- Datetime when the change is made


#### Not Found 404
If the entity with the URI does not exist response code 404 should be returned

### Comments
GET request to the following endpoint should  return the comments attached to the  entity
` <baseUrl>/icat/comments/<URL escaped entity URI> `

Existing formats being used in the iCatX software could be used to represent the threads and comments.

#### Not Found 404
If the entity with the URI does not exist response code 404 should be returned