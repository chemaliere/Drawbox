# Drawbox
 Straw.page-style drawbox component to use for Neocities or other website. Uses Firebase Realtime Database to store sent images.

# Features
- Undo, brush size, and color pickers
- Touch support for mobile
- Firebase Realtime Database, which allows for displaying the b64 image data elsewhere (e.g on a "gallery" page)

# Usage

## Create a Firebase Project
1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Click **"Create a Firebase Project"**
3. Choose a name and follow the setup flow
4. Set up Google Analytics based on whether you want it or not.

## Add Firebase to Your Web App

1. In your Firebase project dashboard, click the **web icon (</>)** to register a new app
2. Give your app a nickname (e.g. `your-drawbox`)
3. Firebase will give you a code snippet like this:
```html
<!-- Add to your <head> or <body> -->
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-database-compat.js"></script>

<script>
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "your-drawbox.firebaseapp.com",
    databaseURL: "https://your-drawbox-default-rtdb.firebaseio.com",
    projectId: "your-drawbox",
    storageBucket: "your-drawbox.appspot.com",
    messagingSenderId: "XXXXXX",
    appId: "APP_ID"
  };

  firebase.initializeApp(firebaseConfig);
  const db = firebase.database();
</script>
```

Replace `"YOUR_API_KEY"` and other values with your actual config from the Firebase dashboard.

## Set Up the Realtime Database

1. In the Firebase Console, go to **Build > Realtime Database**
2. Click **Create Database**
3. Start in **test mode**, which will need to be later set to your own security rules for security
4. Click **“Start”**

Then structure your data however your app expects, for example:

```json
"devlog": {
  "post_id": {
    "title": "Hello World",
    "content": "This is my first post!",
    "date": "2025-04-18T00:00:00Z",
    "hidden": false
  }
}
```

## Security Rules (Optional)
[Google's Documentation] ("https://support.google.com/firebase/answer/7015592#zippy=%2Cin-this-article")

Here’s an example of allowing only read access (good for Neocities):
```json
{
  "rules": {
    ".read": true,
    ".write": false
  }
}
```

For write access through an admin panel, configure rules to allow authenticated writes or use validation rules.

## Set Up on Neocities

If you’re using [Neocities](https://neocities.org/):

- The index.html contains an example of the divs used to set up the drawbox on your index, so set it up like that
- Upload the js and update your CSS
- Firebase access works client-side via JS

## Troubleshooting

- `firebase is not defined`: Make sure you are using the **compat** version of the Firebase scripts
- CORS or CSP issues: You must serve from a trusted domain (Neocities is allowed if CSP is not too strict)
- Images not showing in Realtime DB: Ensure `dataURL` fields are valid base64 strings, or use Firebase Storage