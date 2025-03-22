# Design and implement an interactive image gallery using JavaScript, HTML, and CSS. 
## AIM
To create an interactive, visually stunning image gallery with smooth animations, hover effects, and modal functionality using HTML, CSS, and JavaScript.
## PROCEDURE
- Create an HTML structure.
- Add a CSS file for styling.
- Implement JavaScript for interactivity.
Design the Layout
- Use Flexbox for responsive alignment.
- Add hover animations and transition effects.
- Implement a dark gradient background for a modern look.
- Implement Functionality
- Enable horizontal scrolling for images.
- Add a modal popup to enlarge images on click.
- Include navigation buttons for smooth scrolling.
- Testing and Debugging
- Test responsiveness on different devices.
- Ensure smooth animations and transitions.
## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Gallery</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            color: #fff;
            margin: 0;
            padding: 0;
        }

        .heading {
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            padding: 20px;
            font-size: 32px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
            border-radius: 0 0 15px 15px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
        }

        .gallery-container {
            display: flex;
            align-items: center;
            overflow-x: auto;
            scroll-behavior: smooth;
            white-space: nowrap;
            padding: 20px;
            gap: 15px;
            max-width: 90%;
            margin: auto;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.5);
        }

        .gallery-item {
            position: relative;
            flex: 0 0 auto;
            width: 280px;
            border-radius: 12px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            background: #1a1a1a;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
            border: 3px solid transparent;
        }

        .gallery-item:hover {
            transform: scale(1.1);
            box-shadow: 0px 6px 15px rgba(255, 255, 255, 0.2);
            border: 3px solid #00c3ff;
        }

        .gallery-item img {
            width: 100%;
            height: auto;
            display: block;
        }

        .caption {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            text-align: center;
            padding: 12px;
            opacity: 0;
            transition: opacity 0.3s ease-in-out;
        }

        .gallery-item:hover .caption {
            opacity: 1;
        }

        .nav-btn {
            background: #007bff;
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 18px;
            cursor: pointer;
            margin: 15px;
            border-radius: 6px;
            transition: 0.3s;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
        }

        .nav-btn:hover {
            background: #0056b3;
            transform: scale(1.05);
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            padding-top: 100px;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.9);
        }

        .modal-content {
            margin: auto;
            display: block;
            max-width: 90%;
            max-height: 90%;
            border-radius: 10px;
            box-shadow: 0px 6px 15px rgba(255, 255, 255, 0.3);
        }

        .close {
            position: absolute;
            top: 15px;
            right: 35px;
            color: #f1f1f1;
            font-size: 40px;
            cursor: pointer;
            transition: 0.3s;
        }

        .close:hover {
            color: #bbb;
            transform: scale(1.1);
        }

        footer {
            margin-top: 40px;
            background: #1e3c72;
            color: white;
            padding: 15px;
            font-size: 16px;
            text-transform: uppercase;
            border-radius: 15px 15px 0 0;
        }
    </style>
</head>
<body>

    <div class="heading">
        <h1>Image Gallery</h1>
    </div>

    <button class="nav-btn" onclick="scrollGallery(-1)">Previous</button>
    <button class="nav-btn" onclick="scrollGallery(1)">Next</button>

    <div class="gallery-container" id="gallery">
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="img4.jpg" alt="Nature">
            <div class="caption">Nature</div>
        </div>
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="tech.jpg" alt="Technology">
            <div class="caption">Technology</div>
        </div>
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="space.jpg" alt="Space">
            <div class="caption">Space</div>
        </div>
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="architect .jpg" alt="Architecture">
            <div class="caption">Architecture</div>
        </div>
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="city.jpg" alt="City">
            <div class="caption">City</div>
        </div>
        <div class="gallery-item" onclick="openModal(this.querySelector('img').src)">
            <img src="wildlife.jpg" alt="Wildlife">
            <div class="caption">Wildlife</div>
        </div>
    </div>
    <div id="myModal" class="modal">
        <span class="close" onclick="closeModal()">&times;</span>
        <img class="modal-content" id="modalImage">
    </div>

    <footer>
        Name Deepika S and Register Number 212222230028
    </footer>

    <script>
        function openModal(src) {
            document.getElementById("modalImage").src = src;
            document.getElementById("myModal").style.display = "block";
        }

        function closeModal() {
            document.getElementById("myModal").style.display = "none";
        }

        function scrollGallery(direction) {
            let gallery = document.getElementById("gallery");
            let scrollAmount = 300;
            gallery.scrollBy({ left: direction * scrollAmount, behavior: 'smooth' });
        }
    </script>

</body>
</html>

```
## OUTPUT
![IG1](https://github.com/user-attachments/assets/c87d8e2a-b7bd-469e-a471-e8ed4e379d2a)
![IG2](https://github.com/user-attachments/assets/f1d01f53-59bd-4d2a-837f-d8bda8cd91b6)
## RESULT
 The Interactive Image Gallery delivers a visually captivating and highly responsive experience, featuring smooth animations, hover effects, seamless scrolling, and a dynamic modal viewer for enhanced user engagement.



