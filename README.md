**Title of the project: # JSONPOWERDB**

**Description:** Learn to handle JSON-DB from the scratch


**Benefits of using JSONPowerDB:**

1.Simplest way to retrieve data in a JSON format.

2.Schema-free, Simple to use, Nimble and In-Memory database.

3.It is built on top of one of the fastest and real-time data indexing engine - PowerIndeX.

4.It is low level (raw) form of data and is also human readable.

5.It helps developers in faster coding, in-turn reduces development cost.

**Release History:** Creating first time a very small project to learn basic CRUD operations of JSONDB.

**Screenshots:**

**1.PUT:** PUT inserts single record in the database.

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

**2.GET:** Retrive single row data.

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


**3. UPDATE:** Update multiple records in the database or add a new column in a record.

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


**4. REMOVE:** Remove records from the database.

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






**Data saved in database using CRUD operations:**

![image](https://user-images.githubusercontent.com/112716091/188201200-c5379e51-3f6a-4306-bff2-6234b295888f.png)



**Sending data to database from web page:**

code:

<html lang="en">
    <head>
        <title>Bootstrap Example</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
            src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
            src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
            </head>

    <body>
        <div class="container">
            <h2> Vertical basic form </h2>
            <form id="studForm" method="post">
                <div class="form-group">
                    <span><label for="studId">Student ID: </label></span>
                    <input type="text" class="form-control" name="studid" id="studId"
                           placeholder="Enter Student ID:" required>
                </div>
                <div class="form-group">
                    <label for="studName"> Student Name: </label>
                    <input type="text" class="form-control" name="studname" id="studName"
                           placeholder="Enter Student Name:">
                </div>
                 <div class="form-group">
                    <label for="studEmail"> Email: </label>
                    <input type="email" class="form-control" name="studemail" id="studEmail"
                           placeholder="Enter Student Email:">
                 </div>
                    <input type="button" class="btn btn-primary" id="studSave" value="Save"
                           onclick="saveStudent();">
            </form>
        </div>
        <script>
            $("#studId").focus();
            function validateAndGetFormData(){
                var studidvar=$("#studId").val();
                if(studidvar === ""){
                    alert("Student ID Required Value");
                    $("#studId").focus();
                    return "";
                }
                
                var studnamevar=$("#studName").val();
                if(studnamevar === ""){
                    alert("Student Name is Required Value");
                    $("#studName").focus();
                    return "";
                }
                
                var studemailvar=$("#studEmail").val();
                if(studemailvar === ""){
                    alert("Student Email is Required Value");
                    $("#studEmail").focus();
                    return "";
                }
                var jsonStrObj={
                    studId: studidvar,
                    studName: studnamevar,
                    studEmail: studemailvar
                };
                return JSON.stringify(jsonStrObj);
            }
            
            function createPUTRequest(connToken, jsonObj, dbName, relName){
                var putRequest="{\n"
                               + "\"token\" : \""
                               + connToken
                               + "\","
                               + "\"dbName\" : \""
                               + dbName
                               + "\",\n" +"\"cmd\" : \"PUT\", \n"
                               + "\rel\" : \""
                               + relName + "\","
                               + "\"jsonStr\" : \n"
                               + jsonObj
                               + "\n"
                               + "}";
                              
                return putRequest;
            } 
            
            function executeCommand(reqString, dbBaseUrl, apiEndPointUrl){
            var url = dbBaseUrl + apiEndPointUrl;
            var jsonObj;
            $.post([url], reqString, function (result) {
                jsonObj = JSON.parse(result);
                
            }).fail(function (result) {
                var dataJsonObj = result.responseText;
                jsonObj = JSON.parse(dataJsonObj);
            });
            return jsonObj;
        }
            function resetForm() {
                $("#studId").val("");
                $("#studName").val("");
                $("#studEmail").val("");
                $("#studId").focus();
        }
        function saveStudent(){
        var jsonStr = validateAndGetFormData();
        if(jsonStr === ""){
            return;
        }
        var putReqStr=createPUTRequest("90937408|-31949292197571296|90943487", jsonStr, "Student", "Student-Rel");
        alert(putReqStr);
        jQuery.ajaxSetup({async: false});
        var resultObj = executeCommand(putReqStr, "http://api.login2explore.com:5577", "/api/iml");
        jQuery.ajaxSetup({async: true});
        alert(JSON.stringify(resultObj));
        
        resetForm();
    }
    
        </script>
    </body>
</html>


**Screenshot:**

![image](https://user-images.githubusercontent.com/112716091/188199128-16dcd034-f264-4ac7-81ca-9bfe49ae4d8b.png)







![image](https://user-images.githubusercontent.com/112716091/188199228-6507cae0-b55a-4e68-8b33-db52a9688500.png)









![image](https://user-images.githubusercontent.com/112716091/188199398-4140c72d-389c-4e9d-ac4f-88fec1e14ae2.png)









**Learnings:**

1. This is my first project on GitHub. 
2. Learned so many things on JSONPowerDB database which gave me knowledge of database from scratch.
3. I performed all the CRUD operations.
4. Saving records in the JSONPowerDB from web page using HTML, JAVASCRIPT, CSS, AJAX was also very informative for me. 




**Project Status:**  Data is not getting saved in database and response alert is also not coming on web page. I will b updating that too once I solve the issue.



**Sources:** login2explore.com



