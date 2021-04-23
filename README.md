# Cordova Couchbase Plugin

This plugin enables your Cordova and PhoneGap mobile applications to use the Couchbase Lite 2.8.0.

Platforms:

 * Android 9

Available functionality:

* Create or open a pre-existing local couchbase databases.
* Insert a JSONObject document into a local couchbase database.
* Modify a prexisting document stored in a local couchbase database.
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

Creates a new local couchbase database using the provided database name. If the provided the database name happens to correspond to a pre-existing local database, a new database will not be created but
instead the pre-existing database will be opened.

Parameters:
    
    @param {String} dbName - the name of the database you'd like to create.
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

Inserts a JSONObject document into a local couchbase database. 

Parameters:

    @param {String} dbName - the name of the database you're inserting the document to.
    @param {JSONObject} document - JSON Object document you're like to store in the database.
    @param {successCallback} success - Success callback, called upon successful insertion of the document.
    @param {failCallback} error - Error callback.
   

Examples:
    
    // database name
    var dbName = "Fictional Characters";
    
    // json object document
    var document = {
                     "First Name" : "Frodo",
                     "Last Name" : "Baggins",
                     "Species" : "Hobbit",
                     "Trade" : "Ring-bearer"
                   };
                  
                  
    // insert the document into the database
    couchbase.insertDocument(
        dbName,
        document,
        function(successCode)
        {
            console.log('message sent to wearable: ' + successCode);
        },
        function(errorCode)
        {
            console.log('message sent error: ' + errorCode);
        }
    );

