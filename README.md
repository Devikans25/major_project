<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Travel Planner</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://kit.fontawesome.com/dfd287a03e.js" crossorigin="anonymous"></script>
</head>
<body>

    <!-- Header -->
    <header class="header">
        <button class="openbtn" onclick="openNav()">☰</button>
        <div id="mySidenav" class="sidenav">
            <button class="closebtn" onclick="closeNav()">☰</button>
            <div class="profile-dropdown">
                <img src="default-profile.png" id="userProfilePic" alt="User Profile Picture" class="profile-pic" onclick="toggleProfileMenu()">
                <br><span id="username"><br>Guest<br></span>
            </div>
            <div id="footer" class="Footer">
                <div class="profile-menu" id="profileMenu">
                    <a href="profile.html">View Profile</a>
                    <a href="settings.html">Settings</a>
                    <a href="about.html">About</a>
                    <a href="#" onclick="logout()">Logout</a>
                </div>
            </div>
        </div>
        
        <div class="container">
            <h1 class="logo">Online Travel Planning & Booking Platform</h1>
            <nav class="navigation">
                <ul>
                    <li><a href="#">Home</a></li>
                    <li><a href="#features">Features</a></li>
                    <li><a href="destinations.html">Destinations</a></li>
                    <li><a href="contact.html">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <h2>Plan Your Adventure</h2>
            <p>Discover amazing destinations, create custom itineraries, and make your dream trip a reality.</p>

            <!-- Search Box -->
            <div class="searchbox">
                <input type="text" id="input-box" placeholder="Search Your Destination..." 
                    autocomplete="off" autocorrect="off" 
                    onkeyup="showSuggestions()" onkeypress="handleEnter(event)">
                <button onclick="redirectToPage(document.getElementById('input-box').value)">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </button>
                <div id="suggestions" class="suggestion-box"></div>
            </div>
        </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features">
        <div class="container">
            <h3>Why Choose Us?</h3>
            <div class="feature-cards">
                <div class="card"><h4>Custom Itineraries</h4><p>Detailed plans tailored to your preferences.</p></div>
                <div class="card"><h4>Top Destinations</h4><p>Explore curated lists of popular and hidden gems.</p></div>
                <div class="card"><h4>Seamless Booking</h4><p>Book flights, hotels, and activities all in one place.</p></div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <p>&copy; 2025 Travel Planner. All Rights Reserved.</p>
            <p>Follow us on: <a href="https://www.facebook.com/">Facebook</a> | <a href="https://www.instagram.com/">Instagram</a> | <a href="https://x.com/i/flow/">Twitter</a></p>
        </div>
    </footer>

    <!-- JavaScript -->
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            checkLoginStatus();

            document.addEventListener("click", function(event) {
                let menu = document.getElementById("profileMenu");
                if (!event.target.closest(".profile-dropdown")) {
                    menu.style.display = "none";
                }
            });
        });

        function openNav() {
            document.getElementById("mySidenav").style.width = "250px";
        }

        function closeNav() {
            document.getElementById("mySidenav").style.width = "0";
        }

        function checkLoginStatus() {
            let user = JSON.parse(localStorage.getItem("currentUser"));
            if (user) {
                document.getElementById("username").textContent = user.name || "Guest";
                document.getElementById("userProfilePic").src = user.profilePic || "default-profile.png";
            } else {
                document.getElementById("username").textContent = "Guest";
            }
        }

        function toggleProfileMenu() {
            let menu = document.getElementById("profileMenu");
            menu.style.display = menu.style.display === "block" ? "none" : "block";
        }

        function logout() {
            localStorage.removeItem("currentUser");
            window.location.href = "login.html";
        }

        const places = [
            "Paris", "Pattaya", "Prague", "Philippines", "Peru",
            "Amsterdam", "Athens", "Agra", "Alaska", "Australia",
            "Bangkok", "Bali", "Barcelona", "Berlin", "Brazil",
            "New York", "Nepal", "Norway", "Nairobi", "New Delhi",
            "Switzerland", "Sweden", "Singapore", "South Africa", "Seoul"
        ];

        function showSuggestions() {
            let input = document.getElementById("input-box").value.toLowerCase().trim();
            let suggestionBox = document.getElementById("suggestions");
            suggestionBox.innerHTML = "";

            if (!input) {
                suggestionBox.style.display = "none";
                return;
            }

            let suggestions = places.filter(place => place.toLowerCase().includes(input));

            if (suggestions.length > 0) {
                suggestionBox.style.display = "block";
                suggestions.forEach(place => {
                    let div = document.createElement("div");
                    div.textContent = place;
                    div.classList.add("suggestion-item");
                    div.onclick = () => {
                        document.getElementById("input-box").value = place;
                        suggestionBox.style.display = "none";
                        redirectToPage(place);
                    };
                    suggestionBox.appendChild(div);
                });
            } else {
                suggestionBox.style.display = "none";
            }
        }

        function redirectToPage(query) {
            if (!query.trim()) return;
            window.location.href = `search.html?q=${encodeURIComponent(query)}`;
        }

        function handleEnter(event) {
            if (event.key === "Enter") {
                redirectToPage(document.getElementById("input-box").value);
            }
        }
    </script>

</body>
</html>
