### CSS MAIN PROJECT
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dribble Clone</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f5f5f5;
            color: #333;
        }
        .header {
            background-color: #ea4c89;
            padding: 20px;
            text-align: center;
            color: white;
        }
        .header h1 {
            margin: 0;
            font-size: 2.5em;
        }
        .main {
            padding: 50px;
            text-align: center;
        }
        .main h2 {
            font-size: 2em;
            margin-bottom: 20px;
        }
        .main p {
            font-size: 1.2em;
            margin-bottom: 40px;
            color: #666;
        }
        .auth {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 20px 0;
        }
        .auth input {
            padding: 10px;
            width: 200px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .auth button {
            padding: 10px 20px;
            background-color: #ea4c89;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .auth button:hover {
            background-color: #d04078;
        }
        .gallery {
            position: relative;
            max-width: 800px;
            margin: auto;
            overflow: hidden;
        }
        .gallery img {
            width: 100%;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            cursor: pointer;
        }
        .gallery .slides {
            display: flex;
            transition: transform 0.5s ease-in-out;
        }
        .gallery .prev, .gallery .next {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
        }
        .gallery .prev {
            left: 10px;
        }
        .gallery .next {
            right: 10px;
        }
        .thumbnails {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }
        .thumbnails img {
            width: 100px;
            margin: 0 5px;
            cursor: pointer;
            border-radius: 5px;
            transition: transform 0.3s;
        }
        .thumbnails img:hover {
            transform: scale(1.1);
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            padding-top: 60px;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.9);
        }
        .modal-content {
            margin: auto;
            display: block;
            width: 80%;
            max-width: 700px;
        }
        .modal-content {
            animation-name: zoom;
            animation-duration: 0.6s;
        }
        @keyframes zoom {
            from {transform: scale(0)}
            to {transform: scale(1)}
        }
        .close {
            position: absolute;
            top: 15px;
            right: 35px;
            color: #fff;
            font-size: 40px;
            font-weight: bold;
            transition: 0.3s;
        }
        .close:hover,
        .close:focus {
            color: #bbb;
            text-decoration: none;
            cursor: pointer;
        }
        .footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 20px;
        }
        .footer p {
            margin: 0;
        }
        @media (max-width: 600px) {
            .gallery img, .modal-content {
                width: 100%;
            }
            .thumbnails img {
                width: 60px;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Dribble Clone</h1>
    </div>
    <div class="main">
        <h2>Discover the world's top designers & creatives</h2>
        <div class="auth">
            <input type="text" placeholder="Username">
            <input type="password" placeholder="Password">
            <button onclick="alert('Sign up / Login functionality coming soon!')">Sign Up / Login</button>
        </div>
        <div class="gallery">
            <div class="slides">
                <img src="1 img" alt="Sample Image 1" onclick="openModal(this)">
                <img src="2 img" alt="Sample Image 2" onclick="openModal(this)">
                <img src="3 img" alt="Sample Image 3" onclick="openModal(this)">
                <img src="4 img" alt="Sample Image 4" onclick="openModal(this)">
                <img src="5 img" alt="Sample Image 5" onclick="openModal(this)">
                <img src="6 img" alt="Sample Image 6" onclick="openModal(this)">
            </div>
            <button class="prev" onclick="changeSlide(-1)">&#10094;</button>
            <button class="next" onclick="changeSlide(1)">&#10095;</button>
            <div class="thumbnails">
                <img src="1 img" alt="Sample Image 1" onclick="currentSlide(0)">
                <img src="2 img" alt="Sample Image 2" onclick="currentSlide(1)">
                <img src="3 img" alt="Sample Image 3" onclick="currentSlide(2)">
                <img src="4 img" alt="Sample Image 4" onclick="currentSlide(3)">
                <img src="5 img" alt="Sample Image 5" onclick="currentSlide(4)">
                <img src="6 img" alt="Sample Image 6" onclick="currentSlide(5)">
            </div>
        </div>
    </div>
    <div class="footer">
        <p>&copy; 2024 Dribble Clone. All rights reserved.</p>
    </div>
    <div id="myModal" class="modal">
        <span class="close" onclick="closeModal()">&times;</span>
        <img class="modal-content" id="imgModal">
    </div>
    <script>
        let currentSlideIndex = 0;

        function showSlide(index) {
            const slides = document.querySelector('.gallery .slides');
            const totalSlides = slides.children.length;
            if (index >= totalSlides) {
                currentSlideIndex = 0;
            } else if (index < 0) {
                currentSlideIndex = totalSlides - 1;
            } else {
                currentSlideIndex = index;
            }
            const offset = -currentSlideIndex * 100;
            slides.style.transform = `translateX(${offset}%)`;
        }

        function changeSlide(direction) {
            showSlide(currentSlideIndex + direction);
        }

        function currentSlide(index) {
            showSlide(index);
        }

        // Auto slide every 5 seconds
        setInterval(() => {
            changeSlide(1);
        }, 5000);

        showSlide(currentSlideIndex);

        function openModal(element) {
            const modal = document.getElementById('myModal');
            const modalImg = document.getElementById('imgModal');
            modal.style.display = "block";
            modalImg.src = element.src;
        }

        function closeModal() {
            const modal = document.getElementById('myModal');
            modal.style.display = "none";
        }
    </script>
```

### output:
![Screenshot (13)](https://github.com/chandruiyappan/css-main/assets/123877158/f45700aa-c5cc-4648-a718-82cb7ba75293)
![Screenshot (14)](https://github.com/chandruiyappan/css-main/assets/123877158/f6dc841d-136f-45df-b017-bf3626fe3392)

```
