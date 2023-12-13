<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
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
            <h2>Vertical (basic) form</h2>
            <form id="stuForm" method="post">
                <div class="form-group">
                    <span><label for="rollNo">Roll No:</label> <label id="45667">
                        </label></span>
                    <input type="number" class="form-control" name="rollNo" id="rollNo"
                           placeholder="Enter Roll No" required>
                </div>
                <div class="form-group">
                    <label for="stuName">Student Name:</label>
                    <input type="text" class="form-control" id="stuName"
                           placeholder="Enter Student Name" name="stuName">
                </div>
                <div class="form-group">
                    <label for="stuAddress">Address:</label>
                    <input type="text" class="form-control" id="stuAddress"
                           placeholder="Enter Student Address" name="stuAddress">
                </div>
                <div class="form-group">
                    <label for="stuClass">Class:</label>
                    <input type="text" class="form-control" id="stuClass"
                           placeholder="Enter Student Class" name="stuClass">
                </div>
                <div class="form-group">
                    <label for="stuBirthDate">Birth Date:</label>
                    <input type="number" class="form-control" id="stuBirthDate"
                           placeholder="Enter Student Birth Date" name="stuBirthDate">
                </div>
                <div class="form-group">
                    <label for="stuEnrollmentDate">Enrollment Date:</label>
                    <input type="text" class="form-control" id="stuEnrollmentDate"
                           placeholder="Enter Student Enrollment Date" name="stuEnrollmentDate">
                </div>
                <div class="form-group text-center">
                    <button type="button" class="btn btn-primary" id="Save" value="Save"
                            onclick="saveData()"disabled>Save</button>
                    <button type="button" class="btn btn-primary" id="change" value="change"
                            onclick="changeData()" disabled>Change</button><!-- comment -->
                    <button type="button" class="btn btn-primary" id="reset" value="reset"
                            onclick="resetData()"disabled>Reset</button>
                </div>
            </form>
        </div>
        <script>
            function validateAndGetFormData() {
                var rollNoVar = $("#rollNo").val();
                if (rollNoVar === "") {
                    alert("Roll No Required Value");
                    $("#rollNo").focus();
                    return "";
                }
                var stuNameVar = $("#stuName").val();
                if (stuNameVar === "") {
                    alert("Student Name is Required Value");
                    $("#stuName").focus();
                    return "";
                }
                var stuClassVar = $("#stuClass").val();
                if (stuClassVar === "") {
                    alert("Student Class is Required Value");
                    $("#stuClass").focus();
                    return "";
                }
                var stuBirthDateVar = $("#stuBirthDate").val();
                if (stuBirthDateVar === "") {
                    alert("Student Birth Date is Required Value");
                    $("#stuBirthDate").focus();
                    return "";
                }
                var stuAddressVar = $("#stuAddress").val();
                if (stuAddressVar === "") {
                    alert("Student Address is Required Value");
                    $("#stuAddress").focus();
                    return "";
                }
                var stuEnrollmentDateVar = $("#stuEnrollmentDate").val();
                if (stuEnrollmentDateVar === "") {
                    alert("Student Enrollment Date is Required Value");
                    $("#stuEnrollmentDate").focus();
                    return "";
                }
                var jsonStrObj = {
                    rollNo: rollNoVar,
                    stuName: stuNameVar,
                    stuBirthDate: stuBirthDateVar,
                    stuAddress: stuAddressVar,
                    stuEnrollmentDate: stuenrollmentDateVar
                };
                return JSON.stringify(jsonStrObj);
            }
            function createPUTRequest(connToken, jsonObj, dbName, relName) {
                var putRequest = "{\n"
                        + "\"token\" : \""
                        + connToken
                        + "\","
                        + "\"dbName\": \""
                        + dbName
                        + "\",\n" + "\"cmd\" : \"PUT\",\n"
                        + "\"rel\" : \""
                        + relName + "\","
                        + "\"jsonStr\": \n"
                        + jsonObj
                        + "\n"
                        + "}";
                return putRequest;
            }
            function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
                var url = dbBaseUrl + apiEndPointUrl;
                var jsonObj;
                $.post(url, reqString, function (result) {
                    jsonObj = JSON.parse(result);
                }).fail(function (result) {
                    var dataJsonObj = result.responseText;
                    jsonObj = JSON.parse(dataJsonObj);
                });
                return jsonObj;
            }
            function resetForm() {
                $("#rollNo").val("")
                $("#stuName").val("");
                $("#stuClass").val("");
                $("#stuBirthDate").val("");
                $("#stuAddress").val("");
                $("#stuEnrollmentDate").val("");
                $("#rollNo").focus();
            }

            function saveStudent() {

                var jsonStr = validateAndGetFormData();
                if (jsonStr === "") {
                    return;
                }
                var putReqStr = createPUTRequest("90931485|-31949303199934787|90960639",
                        jsonStr, "Student", "Stu-REL");
                alert(putReqStr);
                jQuery.ajaxSetup({async: false});
                var resultObj = executeCommand(putReqStr,
                        "http://api.login2explore.com:5577", "/api/iml");
                alert(JSON.stringify(resultObj));
                jQuery.ajaxSetup({async: true});
                resetForm();
            }
        </Script>
    </body>
</html>
