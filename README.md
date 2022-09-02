**Title of the project: # jsondb-project**

Description: Learn to handle JSON-DB from the scratch


Benefits of using JSONPowerDB:

1.Simplest way to retrieve data in a JSON format.

2.Schema-free, Simple to use, Nimble and In-Memory database.

3.It is built on top of one of the fastest and real-time data indexing engine - PowerIndeX.

4.It is low level (raw) form of data and is also human readable.

5.It helps developers in faster coding, in-turn reduces development cost.

Release History: Creating first time a very small project to learn basic CRUD operations of JSONDB.

Screenshots:

1.PUT: PUT inserts single record in the database.

Query:

{
    "token": "90937408|-31949292197571296|90943487",
    
    "cmd": "PUT",
    
    "dbName": "Student",
    
    "rel": "Student-Rel",
    
    "jsonStr": {
    
        "id": "1",
        
        "name": "Sneha",
        
        "email": "snehadhirajkabra@gmail.com",
        
        "mobileno": 9067825671
    }
}

![image](https://user-images.githubusercontent.com/112716091/188196223-0b436fc7-bcd0-401a-b102-3661d5033573.png)

2.GET: Retrive single row data.

Query:

{
    "token": "90937408|-31949292197571296|90943487",
    
    "dbName": "Student",
    
    "cmd": "GET_BY_KEY",
    
    "rel": "Student-Rel",
    
    "jsonStr": {
    
        "name": "Soniya"
    }

}


![image](https://user-images.githubusercontent.com/112716091/188196946-8f90f1cf-3462-47e6-bd29-808049f621cf.png)


3. UPDATE: Update multiple records in the database or add a new column in a record.

Query:

{
    "token": "90937408|-31949292197571296|90943487",
    
    "cmd": "UPDATE",
    
    "dbName": "Student",
    
    "rel": "Student-Rel",
    
    "jsonStr": {
    
       "2":{
       
        "full_name": "Gargee Mishra"
        

      }
      }
}

![image](https://user-images.githubusercontent.com/112716091/188197333-be396ae1-bd23-4fa2-b2c1-e383aa4fc72f.png)


4. REMOVE: Remove records from the database.

Query:

{
    "token": "90937408|-31949292197571296|90943487",
    
    "cmd": "REMOVE",
    
    "dbName": "Student",
    
    "rel": "Student-Rel",
    
    "record": 1,
    
    "jsonStr" : {}
}

![image](https://user-images.githubusercontent.com/112716091/188197559-09f53758-df0a-4a84-b19a-ecaa11fd4505.png)
