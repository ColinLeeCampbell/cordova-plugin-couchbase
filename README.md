# Cordova Couchbase Plugin

This plugin enables your Cordova and PhoneGap mobile applications to use the Couchbase Lite 2.8.0.

Platforms:

 * Android 9

Available functionality:

* Create or open a pre-existing local couchbase databases.
* Insert a JSONObject document into a local couchbase database.
* Modify a pre-existing document stored in a local couchbase database.
* Perform a `Select *` document query that returns a list of JSONObject documents.
* Upload all documents from a local couchbase database to a remote couchbase database through a php script.

## Download

Clone the repo into the same directory as your cordova project.

## Installation

Install using the Apache Cordova command line:

    cordova plugin add ../cordova-plugin-couchbase

## Future Updates

* Add the ability to use the sync gateway/replication.
* Include example php code to run on a server.

## Quick Guide

### Create or Open a Local Database

Use function `couchbase.createNewDatabase` to create a new local database:

    couchbase.createNewDatabase(dbName ,success, error)

Creates a new local couchbase database using the provided database name. If the provided the database name happens to correspond to a pre-existing local database, a new database will not be created but instead the pre-existing database will be opened. This function reports all successes and errors to the supplied callback functions.

Parameters:
    
    @param {String} dbName - The name of the database you'd like to create.
    @param {successCallback} success - Success callback, called upon successful creation/opening of a database.
    @param {failCallback} error - Error callback.
   

Examples:
    
    // database name
    var dbName = "Fictional Characters";
    
    // create a new database
    couchbase.createNewDatabase(
        dbName,
        function(successCode)
        {
            console.log('database create success: ' + successCode);
        },
        function(errorCode)
        {
            console.log('database create error: ' + errorCode);
        }
    );


### Insert a Document

Use function `couchbase.insertDocument` to insert a document into a local database:

    couchbase.insertDocument(dbName, document, success, error)

Inserts a JSONObject document into a local couchbase database. This function reports all successes and errors to the supplied callback functions.

Parameters:

    @param {String} dbName - The name of the database you're inserting the document to.
    @param {JSONObject} document - JSON Object document you're like to store in the database.
    @param {successCallback} success - Success callback, called upon successful insertion of the document.
    @param {failCallback} error - Error callback.
   

Examples:
    
    // database name
    var dbName = "Fictional Characters";
    
    // json object document
    var document = {
                     "First Name" : "Rick",
                     "Last Name" : "Deckard",
                     "Species" : "Human",
                     "Trade" : "Blade Runner"
                   };
                                    
    // insert the document into the database
    couchbase.insertDocument(
        dbName,
        document,
        function(successCode)
        {
            console.log('document insert success: ' + successCode);
        },
        function(errorCode)
        {
            console.log('document insert error: ' + errorCode);
        }
    );

### Get All Documents

Use function `couchbase.getAllDocuments` to retrieve all documents from a local database:

    couchbase.getAllDocuments(dbName, success, error)

Retrieves all documents from a local database. This function reports a list of JSONObject documents and errors to the supplied callback functions.

Parameters:

    @param {String} dbName - The name of the database you're retrieving the documents from.
    @param {successCallback} success - Success callback, returns a list of documents from the database.
    @param {failCallback} error - Error callback.
   

Examples:
    
    // database name
    var dbName = "Fictional Characters";
                  
    // retrieve all the documents in the database
    couchbase.getAllDocuments(
        dbName,
        function(documents)
        {
            console.log('documents retrieved: ' + documents.length);
        },
        function(errorCode)
        {
            console.log('document retrieval error: ' + errorCode);
        }
    );

### Upload All Documents

Use function `couchbase.uploadDocuments` to retrieve all documents from a local database:

    couchbase.uploadDocuments(url, dbName, success, error)

Uploads all documents from a local database to a url hosting a php script. The php script proceeds to upload all the recieved documents into the remote couchbase server. Upon successful upload, all of the documents will be purged from the local couchbase database on the mobile device. This function reports all successes and errors to the supplied callback functions.

Parameters:
    
    @param {URL} url - The url hosting the php script for the remote couchbase database.
    @param {String} dbName - The name of the database you're uploading the documents from.
    @param {successCallback} success - Success callback, called when documents are uploaded successfully.
    @param {failCallback} error - Error callback.
   

Examples:

    // url hosting the php script
    var url = "http://localhost:8080/uploadcouch.php";
    
    // database name
    var dbName = "Fictional Characters";
                  
    // upload all the documents in the database
    couchbase.uploadDocuments(
        url,
        dbName,
        function(successCode)
        {
            console.log('documents upload success: ' + successCode);
        },
        function(errorCode)
        {
            console.log('documents upload error: ' + errorCode);
        }
    );

