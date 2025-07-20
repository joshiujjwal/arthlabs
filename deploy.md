# Complete Firebase Setup & Deployment Guide

This guide provides all the necessary steps to set up your Firebase project and deploy the Arth Labs website using Firebase Hosting.

---

## Part 1: Create Your Firebase Project & Database

First, you need a Firebase project and a Firestore database to store the emails.

### Go to the Firebase Console

1. Open your web browser and navigate to the [Firebase Console](https://console.firebase.google.com/).
2. Sign in with your Google account.

### Create a Firebase Project

1. Click on **"Add project"**.
2. Give your project a name (e.g., `arth-labs`).
3. Follow the on-screen steps to create the project.  
   *You can disable Google Analytics for this simple project if you wish.*

### Create the Firestore Database

1. Once your project is created, you'll be on the project dashboard.
2. On the left-hand menu, go to **Build > Firestore Database**.
3. Click the **"Create database"** button.
4. When prompted for security rules, select **Test mode**.
5. Choose a location for your database (e.g., `us-central`).
6. Click **Enable**.

---

## Part 2: Prepare Your Local Project Files

Next, set up the project folder on your computer.

### Create a Project Folder

- On your computer, create a new folder named `arth-labs-site`.

### Create a `public` Subfolder

- Inside `arth-labs-site`, create another folder named `public`.

### Save the HTML File

- Copy the complete code from the `arth_labs_website` artifact.
- Save this code inside the `public` folder as `index.html`.

**Your folder structure should look like:**

```
arth-labs-site/
└── public/
    └── index.html
```

---

## Part 3: Install and Initialize the Firebase CLI

The Firebase Command Line Interface (CLI) is how you'll deploy the site.

### Install Node.js

- If you don't have it, download and install Node.js from [nodejs.org](https://nodejs.org/).

### Install the Firebase CLI

```sh
npm install -g firebase-tools
```

### Log in to Firebase

```sh
firebase login
```

*A browser window will open. Log in to the same Google account you used for Firebase.*

### Initialize Your Project

1. In your terminal, navigate into your `arth-labs-site` folder:

    ```sh
    cd path/to/your/arth-labs-site
    ```

2. Run the initialization command:

    ```sh
    firebase init hosting
    ```

3. **Answer the questions exactly as follows:**

    - Are you ready to proceed? → **Yes**
    - Which Firebase project do you want to associate? → **Use an existing project**
    - Select your `arth-labs` project from the list.
    - What do you want to use as your public directory? → **public** (Press Enter)
    - Configure as a single-page app? → **No**
    - Set up automatic builds and deploys with GitHub? → **No**
    - File `public/index.html` already exists. Overwrite? → **No (Crucial!)**

---

## Part 4: Secure Your Database Rules

This is a critical security step.

### Go to Firestore Rules

- In the Firebase Console, navigate back to your Firestore Database and click the **Rules** tab.

### Update the Rules

- Delete all the existing text and replace it with these rules:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Deny all access by default
    match /{document=**} {
      allow read, write: if false;
    }

    // Allow anyone to CREATE a document in the "mailing_list" collection.
    match /mailing_list/{docId} {
      allow create: if true;
      allow read, update, delete: if false;
    }
  }
}
```

### Publish the Rules

- Click the **Publish** button.

---

## Part 5: Deploy Your Website

The final step to go live.

### Run the Deploy Command

In your terminal (still inside the `arth-labs-site` folder), run:

```sh
firebase deploy --only hosting
```

**Done!**

After the command finishes, it will give you a Hosting URL. This is the link to your live website.

---

## Updating Your Website

To update your website in the future, simply edit the `index.html` file and run:

```sh
firebase deploy --only hosting
```
again.