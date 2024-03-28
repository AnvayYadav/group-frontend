---
toc: true
comments: false
layout: post
title: Salary Estimater
description: Salary estimater
type: plans
courses: { compsci: {week: 0} }
---

<body>
    <h1>Pay</h1>
    <form id="payForm">
        <div class="form-group">
            <label for="_title">Job Title:</label>
            <input type="text" id="_title" name="_title" class="form-control" required>
        </div>
        <div class="form-group">
            <label for="_field">Field:</label>
            <input type="text" id="_field" name="_field" class="form-control" required>
        </div>
        <div class="form-group">
            <label for="_qualification">Qualification</label>
            <input type="text" id="_qualification" name="_qualification" class="form-control" required>
        </div>
        <button type="button" class="btn btn-primary" onclick="salary_estimate()">Predict Salary</button>
    </form>
    <div id="result"></div>
    <script>
        function salary_estimate() {
            var form = document.getElementById('payForm');
            var formData = new FormData(form);
            fetch('http://127.0.0.1:8082/api/salary_estimate/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                },
                body: JSON.stringify(Object.fromEntries(formData))
            })
            .then(response => response.json())
            .then(data => {
                var resultDiv = document.getElementById('result');
                resultDiv.innerHTML = '<h2>Salary Estimate</h2>';
                for (var key in data) {
                    resultDiv.innerHTML += '<p>' + key + ': ' + data[key] + '</p>';
                }
            })
            .catch(error => {
                console.error('Error:', error);
            });
        }
    </script>
</body>