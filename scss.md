  npm init
  npm install node-sass

Add this script to package.json;

  "scripts": {
    "sass": "node-sass -w scss/ -o dist/css/ --recursive"
  },

Make an scss folder, create a main.scss in init. Make a dist folder with an index.html

  write some scss; 

    $primary-color: #444;

    body {
      background: $primary-color;
    }
Run sass; 
    npm run sass

Watch the css be generated in dist folder. Dont modify the compiled css file, only write scss in main.scss