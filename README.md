
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
  
To find the hex code for any colour by just putting a picture of our desire colour.
