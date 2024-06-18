<template>
<div class="container form-container">
        <h2>Company Details Form</h2>
        <form id="companyForm">
            <div class="mb-3">
                <label for="companyName" class="form-label">Company Name</label>
                <input type="text" class="form-control" id="companyName" required>
            </div>
            <div class="mb-3">
                <label for="numEmployees" class="form-label">Number of Employees</label>
                <input type="number" class="form-control" id="numEmployees" min="1" required>
            </div>
            <div id="employeeNamesContainer" class="mb-3"></div>
            <div class="mb-3">
                <label for="workShift" class="form-label">Work Shift</label>
                <select class="form-select" id="workShift" required>
                    <option value="morning">Morning</option>
                    <option value="afternoon">Afternoon</option>
                    <option value="night">Night</option>
                </select>
            </div>
            <div class="mb-3">
                <label for="totalHours" class="form-label">Total Number of Hours During the Week</label>
                <input type="number" class="form-control" id="totalHours" min="0" required>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>
<script>
        $(document).ready(function() {
            $('#numEmployees').on('input', function() {
                var numEmployees = $(this).val();
                var employeeNamesContainer = $('#employeeNamesContainer');
                employeeNamesContainer.empty();
                
                for (var i = 0; i < numEmployees; i++) {
                    employeeNamesContainer.append(`
                        <div class="mb-3">
                            <label for="employeeName${i+1}" class="form-label">Employee Name ${i+1}</label>
                            <input type="text" class="form-control" id="employeeName${i+1}" required>
                        </div>
                    `);
                }
            });

            $('#companyForm').on('submit', function(event) {
                event.preventDefault();
                
                var companyName = $('#companyName').val();
                var numEmployees = $('#numEmployees').val();
                var employeeNames = [];
                for (var i = 0; i < numEmployees; i++) {
                    employeeNames.push($(`#employeeName${i+1}`).val());
                }
                var workShift = $('#workShift').val();
                var totalHours = $('#totalHours').val();
                
                var formData = {
                    companyName: companyName,
                    numEmployees: numEmployees,
                    employeeNames: employeeNames,
                    workShift: workShift,
                    totalHours: totalHours
                };
                
                console.log(formData);
                alert('Form submitted! Check the console for details.');
            });
        });
    </script>

<style>
body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
.form-container {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
.form-container h2 {
    margin-bottom: 20px;
}
</style>