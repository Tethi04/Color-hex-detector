<html lang="en">
 <head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1" name="viewport"/>
  <title>
   Color Hex Code Detector
  </title>
  <script src="https://cdn.tailwindcss.com">
  </script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" rel="stylesheet"/>
  <style>
   /* Hide the canvas */
    #color-canvas {
      display: none;
    }
  </style>
  Link: https://tethi04.github.io/Color-hex-detector/
 </head>
 <body class="bg-gray-50 min-h-screen flex flex-col items-center p-4">
  <header class="w-full max-w-xl text-center mb-8">
   <h1 class="text-3xl font-bold text-gray-800 mb-2">
    Color Hex Code Detector
   </h1>
   <p class="text-gray-600">
    Upload a photo and click on the image to get the hex code of the color.
   </p>
  </header>
  <main class="w-full max-w-xl flex flex-col items-center space-y-6">
   <label class="cursor-pointer bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded inline-flex items-center" for="image-upload">
    <i class="fas fa-upload mr-2">
    </i>
    Upload Image
    <input accept="image/*" aria-label="Upload an image to detect color" class="hidden" id="image-upload" type="file"/>
   </label>
   <div aria-label="Uploaded image container" class="relative w-full h-64 bg-gray-200 rounded-md overflow-hidden flex justify-center items-center" id="image-container">
    <img alt="Placeholder image with text 'Upload an image to start'" class="max-w-full max-h-full object-contain cursor-crosshair" height="256" id="uploaded-image" src="https://storage.googleapis.com/a1aa/image/50929422-3cb5-4ac6-f389-38f681e9de75.jpg" tabindex="0" width="400"/>
   </div>
   <div aria-atomic="true" aria-live="polite" class="w-full bg-white rounded-md shadow p-4 flex flex-col items-center space-y-3" id="color-info">
    <div aria-label="Detected color swatch" class="w-24 h-24 rounded-md border border-gray-300" id="color-swatch">
    </div>
    <div class="text-center">
     <p class="text-lg font-semibold text-gray-800" id="hex-code">
      #FFFFFF
     </p>
     <p class="text-sm text-gray-600" id="rgb-code">
      RGB(255, 255, 255)
     </p>
    </div>
   </div>
  </main>
  <canvas id="color-canvas">
  </canvas>
  <script>
   const imageUpload = document.getElementById("image-upload");
    const uploadedImage = document.getElementById("uploaded-image");
    const colorSwatch = document.getElementById("color-swatch");
    const hexCodeText = document.getElementById("hex-code");
    const rgbCodeText = document.getElementById("rgb-code");
    const colorCanvas = document.getElementById("color-canvas");
    const ctx = colorCanvas.getContext("2d");

    // Convert RGB to Hex
    function rgbToHex(r, g, b) {
      return (
        "#" +
        [r, g, b]
          .map((x) => {
            const hex = x.toString(16);
            return hex.length === 1 ? "0" + hex : hex;
          })
          .join("")
          .toUpperCase()
      );
    }

    // Load image from file input
    imageUpload.addEventListener("change", (e) => {
      const file = e.target.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = function (event) {
        uploadedImage.src = event.target.result;
      };
      reader.readAsDataURL(file);
    });

    // When image loads, resize canvas to image size
    uploadedImage.addEventListener("load", () => {
      colorCanvas.width = uploadedImage.naturalWidth;
      colorCanvas.height = uploadedImage.naturalHeight;
      ctx.drawImage(uploadedImage, 0, 0);
    });

    // Get color on click or keyboard enter/space on image
    function getColorFromEvent(e) {
      e.preventDefault();
      let rect = uploadedImage.getBoundingClientRect();

      let x, y;
      if (e.type.startsWith("touch")) {
        const touch = e.touches[0] || e.changedTouches[0];
        x = touch.clientX - rect.left;
        y = touch.clientY - rect.top;
      } else {
        x = e.clientX - rect.left;
        y = e.clientY - rect.top;
      }

      // Calculate scale factor for image displayed size vs natural size
      const scaleX = uploadedImage.naturalWidth / rect.width;
      const scaleY = uploadedImage.naturalHeight / rect.height;

      const imgX = Math.floor(x * scaleX);
      const imgY = Math.floor(y * scaleY);

      if (
        imgX < 0 ||
        imgY < 0 ||
        imgX >= colorCanvas.width ||
        imgY >= colorCanvas.height
      ) {
        return;
      }

      const pixel = ctx.getImageData(imgX, imgY, 1, 1).data;
      const [r, g, b, a] = pixel;

      if (a === 0) {
        // Transparent pixel
        hexCodeText.textContent = "Transparent pixel";
        rgbCodeText.textContent = "";
        colorSwatch.style.backgroundColor = "transparent";
        return;
      }

      const hex = rgbToHex(r, g, b);
      colorSwatch.style.backgroundColor = hex;
      hexCodeText.textContent = hex;
      rgbCodeText.textContent = `RGB(${r}, ${g}, ${b})`;
    }

    uploadedImage.addEventListener("click", getColorFromEvent);

    // Keyboard accessibility: allow Enter or Space to pick center pixel color
    uploadedImage.addEventListener("keydown", (e) => {
      if (e.key === "Enter" || e.key === " ") {
        e.preventDefault();
        // Pick center pixel color
        const centerX = Math.floor(colorCanvas.width / 2);
        const centerY = Math.floor(colorCanvas.height / 2);
        const pixel = ctx.getImageData(centerX, centerY, 1, 1).data;
        const [r, g, b, a] = pixel;

        if (a === 0) {
          hexCodeText.textContent = "Transparent pixel";
          rgbCodeText.textContent = "";
          colorSwatch.style.backgroundColor = "transparent";
          return;
        }

        const hex = rgbToHex(r, g, b);
        colorSwatch.style.backgroundColor = hex;
        hexCodeText.textContent = hex;
        rgbCodeText.textContent = `RGB(${r}, ${g}, ${b})`;
      }
    });

    // Touch support for mobile devices
    uploadedImage.addEventListener("touchstart", getColorFromEvent);
  </script>
 </body>
</html>
# Color-hex-detector
To find the hex code for any colour by just putting a picture of our desire colour.
