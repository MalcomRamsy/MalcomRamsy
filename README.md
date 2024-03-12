<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Savings Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Top Banner -->
    <div class="top-banner">
        <!--<h1> </h1>-->
        <img style="height: 14%;
        width: 17%;
        position: relative;
        overflow: hidden;
        border-radius: 14px;
        "  src="S_G.jpg" >
    </div>

    <!-- Notification Area -->
    <div class="notification-area">
        <p id="notification-message"></p>
    </div>

    <!-- Main Content -->
    <div class="main-content">
        <!-- Deposit Form -->
        <div class="deposit-form">
            <h2>Deposit Money</h2>
            <form id="deposit-form">
                <label for="deposit-name">Name:</label>
                <select id="deposit-name" name="deposit-name" required>
                    <option value="" disabled selected>Select a user</option>
                    <option value="none"></option>
                    <option value="Maxwel">Maxwel</option>
                    <option value="Maclean">Maclean</option>
                    <option value="Davis">Davis</option>
                    <option value="Mariana">Mariana</option>
                    <option value="Daniels">Daniels</option>
                    <option value="Malcom">Malcom</option>
                    <option value="Maxine">Maxine</option>
                    <option value="Maclister">Maclister</option>
                </select><br>
                <label for="deposit-amount">Amount:</label>
                <input type="number" id="deposit-amount" name="deposit-amount" required><br>
                <button type="submit">Deposit</button>
            </form>
        </div>

        <!-- Withdraw Form -->
        <div class="withdraw-form">
            <h2>Withdraw Money</h2>
            <form id="withdraw-form">
                <label for="withdraw-name">Name:</label>
                <select id="withdraw-name" name="withdraw-name" required>
                    <option value="" disabled selected>Select a user</option>
                    <option value="none"></option>
                    <option value="Maxwel">Maxwel</option>
                    <option value="Maclean">Maclean</option>
                    <option value="Davis">Davis</option>
                    <option value="Mariana">Mariana</option>
                    <option value="Daniels">Daniels</option>
                    <option value="Malcom">Malcom</option>
                    <option value="Maxine">Maxine</option>
                    <option value="Maclister">Maclister</option>
                </select><br>
                <label for="withdraw-amount">Amount:</label>
                <input type="number" id="withdraw-amount" name="withdraw-amount" required><br>
                <button type="submit">Withdraw</button>
            </form>
        </div>

        <!-- User Balance -->
        <p id="user-balance"></p>
    </div>

    <!-- Bottom Banner -->
    <div class="bottom-banner">&copy; S_G . All rights reserved.</p>
    </div>

    <!-- Scripts -->
    <script src="script.js"></script>
    <script>
        // Function to handle deposit form submission
        document.getElementById('deposit-form').addEventListener('submit', function(event) {
            event.preventDefault(); // Prevent form submission

            // Get name and amount from input fields
            let name = document.getElementById('deposit-name').value.trim();
            let amount = parseFloat(document.getElementById('deposit-amount').value);

            // Call deposit function with name and amount
            if (deposit(name, amount)) {
                displayNotification('Deposited:', 'green', `$${amount}`);
            } else {
                displayNotification('User not found or already deposited twice today', 'red');
            }
        });

        // Function to handle withdraw form submission
        document.getElementById('withdraw-form').addEventListener('submit', function(event) {
            event.preventDefault(); // Prevent form submission

            // Get name and amount from input fields
            let name = document.getElementById('withdraw-name').value.trim();
            let amount = parseFloat(document.getElementById('withdraw-amount').value);

            // Call withdraw function with name and amount
            if (withdraw(name, amount)) {
                displayNotification('Withdrawn:', 'green', `$${amount}`);
            } else {
                displayNotification('User not found, already withdrawn twice today, or insufficient balance', 'red');
            }
        });

        // Function to display user balance
        function displayBalance() {
            let userData = JSON.parse(localStorage.getItem('users')) || [];
            let user = userData.find(u => u.name === document.getElementById('deposit-name').value); // Retrieve user based on selected name
            if (user) {
                let balanceArea = document.getElementById('user-balance');
                balanceArea.textContent = `Balance: $${user.balance}`;
                balanceArea.style.color = 'blue';
            }
        }

        // Call displayBalance function when the page loads
        displayBalance();
        
        // Add event listener to update balance when a user is selected
        document.getElementById('deposit-name').addEventListener('change', displayBalance);
        document.getElementById('withdraw-name').addEventListener('change', displayBalance);
    </script>
</body>
</html>
