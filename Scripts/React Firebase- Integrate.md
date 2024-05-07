---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:24
Last edited by: Shudipto Trafder
Last edited time: 2023-10-18T21:56
tags:
  - firebase
  - react
---
1. Create a new file with firebase.js

```Plain
import { _apps, initializeApp } from 'firebase/app'
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";
import { getAnalytics } from "firebase/analytics";
import { getPerformance } from "firebase/performance";
import { getMessaging } from "firebase/messaging";

let app = null;

if (!_apps.length) {
    console.log("DEBUG", "adding app")
    app = initializeApp({
        apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
        authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
        databaseURL: process.env.REACT_APP_FIREBASE_DATABASE_URL,
        projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
        storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
        messagingSenderId: process.env.REACT_APP_FIREBASE_MESSAGING_SENDER_ID,
        appId: process.env.REACT_APP_FIREBASE_APP_ID,
    })

    console.log("DEBUG", app)
} else {
    app = _apps[0]
}

export const firebaseAuth = getAuth(app);
export const firebaseDB = getFirestore(app);
export const firebaseAnalytics = getAnalytics(app);
export const firebasePerformance = getPerformance(app);
export const firebaseMessaging = getMessaging(app);

```

now use it from here,

## Problem

But still there is a problem, if you refresh the app, it will thow error, because of firebase auth service not loaded yet from cache.

from example lets, if we use with axios interceptor

```Plain
instance.interceptors.request.use(async function (config) {
    console.log("I am intercepting", config);

    try {
        const idToken = await firebaseAuth.currentUser?.getIdToken() ?? "";
        console.log("DEBUG: token", idToken);
        if (idToken.length !== 0) {
            config.headers.Authorization = idToken;
        }

    } catch (error) {
        // toast.error("Session Expired, Please Login Again");
        window.location.href = "/login";
        console.log("DEBUG: I am rejecting", error);
        throw error; // Propagate the error to the caller of the interceptor
    }

    console.log(config);

    return config;
});
```

Here most of the time idToken will be empty after refresh.

## Fix

lets fix it

1. create a listener firebase onAuthChange, when change lets call the api, we will wait max 5s.

```Plain
const firebaseAuthPromise = new Promise((resolve) => {
    const unsubscribe = firebaseAuth.onAuthStateChanged((user) => {
        unsubscribe();
        resolve(user);
    });
});
```

step2:

```Plain
const timeoutPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(new Error('Firebase app initialization timed out'));
    }, 5000); // Adjust the timeout duration as needed
});
```

### Code

```Plain
instance.interceptors.request.use(async function (config) {
    console.log("I am intercepting", config);
    try {
        await Promise.race([firebaseAuthPromise, timeoutPromise]); // Wait for the Firebase app to initialize or time out
        const idToken = await firebaseAuth.currentUser?.getIdToken() ?? "";
        console.log("DEBUG: token", idToken);
        if (idToken.length !== 0) {
            config.headers.Authorization = idToken;
        }

    } catch (error) {
        // toast.error("Session Expired, Please Login Again");
        // window.location.href = "/login";
        console.log("DEBUG: I am rejecting", error);
        throw error; // Propagate the error to the caller of the interceptor
    }

    console.log(config);

    return config;
});
```