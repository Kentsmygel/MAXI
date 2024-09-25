<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dog Animation</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            background-image: url('MAXI.jpg'); /* Replace with your background image URL */
            background-size: cover; /* Ensures the image covers the entire screen */
            background-position: center; /* Centers the image */
            background-repeat: no-repeat; /* Prevents the image from repeating */
            overflow: hidden; /* Prevents scrollbars */
            position: relative; /* Allows positioning of the dog */
        }

        #dog {
            position: absolute;
            width: 100px; /* Adjust the width of the dog image */
            bottom: 50px; /* Position above the bottom */
            left: -100px; /* Start position off-screen to the left */
            display: none; /* Initially hidden */
        }
    </style>
</head>
<body>

    <img id="dog" src="DOG_IMAGE_URL" alt="White Labrador"> <!-- Replace with your dog image URL -->

    <script>
        // Select the dog image and the body
        const dog = document.getElementById('dog');
        const body = document.body;

        // Function to make the dog run back and forth
        function makeDogRun() {
            // Show the dog
            dog.style.display = 'block';

            // Reset position
            dog.style.left = '-100px'; // Start position off-screen to the left

            // Animate the dog running across the screen
            let start = null;

            function animateDog(timestamp) {
                if (!start) start = timestamp;
                const progress = timestamp - start;

                // Move the dog to the right
                dog.style.left = Math.min(progress / 5, window.innerWidth) + 'px';

                // If the dog has reached the end, reset the position
                if (parseInt(dog.style.left) >= window.innerWidth) {
                    dog.style.left = '-100px'; // Reset to the left
                    start = null; // Reset start time
                }

                requestAnimationFrame(animateDog);
            }

            requestAnimationFrame(animateDog);
        }

        // Event listener for clicking on the body
        body.addEventListener('click', makeDogRun);
    </script>
</body>
</html>
