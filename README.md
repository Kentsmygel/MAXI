<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dog and Stick Animation</title>
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
            position: relative; /* Allows positioning of elements */
        }

        #dog {
            position: absolute;
            width: 100px; /* Adjust the width of the dog image */
            bottom: 50px; /* Position above the bottom */
            left: -100px; /* Start position off-screen to the left */
            display: none; /* Initially hidden */
        }

        .stick {
            position: absolute;
            width: 50px; /* Adjust the width of the stick image */
            display: none; /* Initially hidden */
        }
    </style>
</head>
<body>

    <img id="dog" src="DOG_IMAGE_URL" alt="White Labrador"> <!-- Replace with your dog image URL -->
    <img id="stick" class="stick" src="STICK_IMAGE_URL" alt="Stick"> <!-- Replace with your stick image URL -->

    <script>
        // Select the dog and stick images
        const dog = document.getElementById('dog');
        const stick = document.getElementById('stick');
        const body = document.body;

        // Function to animate the stick flying and dog running
        function throwStick(event) {
            const clickX = event.clientX; // Get click position
            const direction = Math.random() < 0.5 ? 'left' : 'right'; // Randomly choose direction

            // Show the stick and position it at the click location
            stick.style.display = 'block';
            stick.style.left = clickX + 'px';
            stick.style.top = (event.clientY - 25) + 'px'; // Center the stick vertically

            // Animate the stick flying
            const duration = 1000; // Duration of animation in milliseconds
            const startTime = performance.now();

            function animateStick(time) {
                const elapsed = time - startTime;
                const progress = Math.min(elapsed / duration, 1);
                const distance = (direction === 'left' ? -1 : 1) * (window.innerWidth + 50) * progress; // Fly off screen

                // Calculate the stick's curve
                const curve = Math.sin(progress * Math.PI) * 50; // Slight curve effect

                stick.style.transform = `translate(${distance}px, -${curve}px)`;

                if (progress < 1) {
                    requestAnimationFrame(animateStick);
                } else {
                    // After the stick animation is complete, make the dog run
                    makeDogRun(direction);
                }
            }

            requestAnimationFrame(animateStick);
        }

        // Function to make the dog run to fetch the stick
        function makeDogRun(direction) {
            // Show the dog and reset its position
            dog.style.display = 'block';
            dog.style.transform = direction === 'left' ? 'scaleX(-1)' : 'scaleX(1)';
            dog.style.left = direction === 'left' ? (window.innerWidth + 100) + 'px' : '-100px';
            dog.style.bottom = '50px'; // Reset the dog's vertical position

            // Animate the dog running
            const duration = 2000; // Duration of dog animation in milliseconds
            const startTime = performance.now();

            function animateDog(time) {
                const elapsed = time - startTime;
                const progress = Math.min(elapsed / duration, 1);
                const distance = (direction === 'left' ? -1 : 1) * (window.innerWidth - 100) * progress; // Move the dog across the screen

                dog.style.left = `${direction === 'left' ? (window.innerWidth - distance) : distance}px`;

                if (progress < 1) {
                    requestAnimationFrame(animateDog);
                } else {
                    // Hide the stick and reset the dog position
                    stick.style.display = 'none';
                    dog.style.display = 'none';
                }
            }

            requestAnimationFrame(animateDog);
        }

        // Event listener for clicking on the body
        body.addEventListener('click', throwStick);
    </script>
</body>
</html>
