<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auto-Save Form</title>
    <style>
        body { font-family: Arial, sans-serif; }
        form { max-width: 300px; margin: auto; }
        .form-group { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; }
        input { width: 100%; padding: 8px; box-sizing: border-box; }
        .sec-div { display: none; } /* Initially hide all sec-divs */
        .sec-div {
            padding:10px;
            background-color:#0081ff;
            margin-bottom:10px;
        }
    </style>
</head>
<body>
    
    <div class="sec-div" style="background-color:#0066f0;">
        khggg
        <input class="match-input" value="apple" type="text">
    </div>

    <div class="sec-div" style="background-color:#0066f0;">
        <input class="match-input" value="phon" type="text">
    </div>

    <div class="sec-div" style="background-color:#0066f0;">
        <input class="match-input" value="100" type="text">
    </div>

    <div class="sec-div" style="background-color:#0066f0;">
        <input class="match-input" value="100" type="text">
    </div>
    
    <form id="autoSaveForm">
        <div class="form-group">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name">
        </div>
        <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" name="email">
        </div>
        <div class="form-group">
            <label for="message">Message:</label>
            <textarea id="message" name="message" rows="4"></textarea>
        </div>
    </form>

    <script>
        // Function to save form data to localStorage
        function saveFormData() {
            const form = document.getElementById('autoSaveForm');
            const formData = new FormData(form);
            formData.forEach((value, key) => {
                localStorage.setItem(key, value);
            });
        }

        // Function to load form data from localStorage
        function loadFormData() {
            const form = document.getElementById('autoSaveForm');
            const inputs = form.querySelectorAll('input, textarea');
            inputs.forEach(input => {
                const savedValue = localStorage.getItem(input.name);
                if (savedValue) {
                    input.value = savedValue;
                }
            });
        }

        // Function to show/hide sec-div based on name input
        function filterDivs() {
            const nameValue = document.getElementById('name').value.toLowerCase();
            const divs = document.querySelectorAll('.sec-div');
            divs.forEach(div => {
                const inputValue = div.querySelector('.match-input').value.toLowerCase();
                if (inputValue === nameValue) {
                    div.style.display = 'block';
                } else {
                    div.style.display = 'none';
                }
            });
        }

        // Event listeners
        document.addEventListener('DOMContentLoaded', () => {
            loadFormData();
            filterDivs(); // Initial filter based on loaded data
        });
        document.getElementById('autoSaveForm').addEventListener('input', saveFormData);
        document.getElementById('name').addEventListener('input', filterDivs);
    </script>
</body>
</html>
