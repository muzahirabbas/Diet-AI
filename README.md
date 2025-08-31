# **AI Diet 🥗 \- Your Personal AI-Powered Calorie Tracker**

AI Diet is a modern, single-page web application that helps you track your daily calorie intake and expenditure. Leveraging the power of Google's Gemini AI, you can log meals and exercises using text, voice, or even by taking a picture of your food. All your data is securely stored in your own Firebase project.

## **✨ Features**

* **AI-Powered Logging**: Describe your meal or workout, and the Gemini AI will analyze it and estimate the calories.  
* **Multi-Modal Input**: Log your entries via:  
  * **Text**: Type "I ate a plate of biryani."  
  * **Voice**: Use the microphone to speak your log.  
  * **Image Upload**: Upload a picture of your meal from your gallery.  
  * **Camera Capture**: Take a photo of your food directly within the app.  
* **Secure Authentication**: Sign in securely with your Google account using Firebase Authentication.  
* **Personalized Dashboard**: See your net calories, consumed vs. burnt totals, and your daily target at a glance.  
* **Data Persistence**: Your settings and daily progress are saved to your personal Firebase Firestore database.  
* **Calorie Calculator**: An integrated calculator helps you determine your maintenance and target daily calories based on your age, weight, height, and gender.  
* **Manual Control**: Easily reset or adjust your daily consumed/burnt totals.  
* **Light & Dark Mode**: Automatically adapts to your system preference and includes a manual toggle.  
* **Fully Self-Hosted**: The entire application runs from a single index.html file and connects to *your own* Firebase and Google AI backends.

## **🛠️ Tech Stack**

* **Frontend**: HTML, Tailwind CSS, Vanilla JavaScript (ES Modules)  
* **Backend**:  
  * **Firebase Authentication**: For Google Sign-In.  
  * **Firebase Firestore**: As the NoSQL database to store user data and settings.  
* **AI**: Google Gemini API for natural language and vision-based calorie estimation.  
* **Web APIs**:  
  * Web Speech API for voice recognition.  
  * getUserMedia for camera access.

## **🚀 Getting Started: Setting Up Your Own Version**

Follow these steps to get your own copy of AI Diet up and running.

### **Prerequisites**

* A [Google Account](https://www.google.com/search?q=https://accounts.google.com/signup) to use Firebase and Google AI Studio.  
* Knowledge of how to copy/paste code into a file.  
* A code editor like [VS Code](https://code.visualstudio.com/).

### **Step 1: Clone the Repository**

First, get the code onto your local machine.
 ```
git clone \[https://github.com/YOUR\_USERNAME/YOUR\_REPOSITORY\_NAME.git\](https://github.com/YOUR\_USERNAME/YOUR\_REPOSITORY\_NAME.git)  
cd YOUR\_REPOSITORY\_NAME
 ```
### **Step 2: Set Up Your Firebase Project**

This project uses Firebase for user authentication and data storage.

1. **Create a Firebase Project**:  
   * Go to the [Firebase Console](https://console.firebase.google.com/).  
   * Click on **"Add project"** and give it a name (e.g., "My-AI-Diet-App").  
   * Continue through the setup steps.  
2. **Enable Authentication**:  
   * In your new project's dashboard, go to **Build \> Authentication**.  
   * Click **"Get started"**.  
   * Under the "Sign-in method" tab, select **Google** from the list of providers.  
   * **Enable** the Google provider and set a project-facing email, then click **Save**.  
3. **Add Authorized Domains**:  
   * Still in the **Authentication \> Settings** tab, scroll down to the **"Authorized domains"** section.  
   * Click **"Add domain"**.  
   * If you are testing locally, you might need to add localhost. If you have deployed your site (e.g., to GitHub Pages or Netlify), you must add your live URL (e.g., your-username.github.io).  
4. **Set up Firestore Database**:  
   * Go to **Build \> Firestore Database**.  
   * Click **"Create database"**.  
   * Start in **production mode**. This ensures your data is secure.  
   * Choose a location for your database (e.g., us-central).  
   * Click **Enable**.  
5. **Update Firestore Security Rules**:  
   * In the Firestore Database section, click on the **"Rules"** tab.  
   * Delete the existing rules and replace them with the following code. This ensures that users can only read and write their own data.  
   * Click **Publish**.

   ```
      rules\_version \= '2';  
      service cloud.firestore {  
        match /databases/{database}/documents {  
          // Users can only read and write their own document.  
          match /users/{userId} {  
            allow read, write: if request.auth \!= null && request.auth.uid \== userId;  
          }  
        }  
      }
   ```

6. **Get Your Firebase Configuration**:  
   * Go to your **Project Settings** (click the gear icon ⚙️ next to "Project Overview").  
   * In the **General** tab, scroll down to "Your apps".  
   * Click the web icon (\</\>) to create a new web app.  
   * Give it a nickname (e.g., "AI Diet Web") and click **"Register app"**.  
   * Firebase will provide you with a firebaseConfig object. **Copy this entire object**.

### **Step 3: Update the Code with Your Firebase Config**

1. Open the index.html file in your code editor.  
2. Find the \<script type="module"\> tag near the bottom of the file.  
3. Locate the firebaseConfig constant. It will look like a placeholder similar to this:

   ``` 
   const firebaseConfig \= {  
       apiKey: "YOUR\_API\_KEY",  
       authDomain: "YOUR\_PROJECT\_ID.firebaseapp.com",  
       projectId: "YOUR\_PROJECT\_ID",  
       storageBucket: "YOUR\_PROJECT\_ID.appspot.com",  
       messagingSenderId: "YOUR\_MESSAGING\_SENDER\_ID",  
       appId: "YOUR\_APP\_ID",  
       measurementId: "YOUR\_MEASUREMENT\_ID"  
   };
   ```
5. **Replace this entire placeholder object** with the firebaseConfig object you copied from your Firebase project dashboard in the previous step. The values (like apiKey, projectId, etc.) will be unique to your project.

### **Step 4: Get Your Google Gemini API Key**

The app requires a Gemini API key for its AI features. This key is stored securely in each user's Firestore document, not in the code itself. You need to generate a key to use the app for the first time.

1. Go to [Google AI Studio](https://aistudio.google.com/).  
2. Sign in with your Google account.  
3. On the left menu, click **"Get API key"**.  
4. Click **"Create API key"**.  
5. **Copy the generated API key** and save it somewhere safe. You will need it the first time you use the app.

### **Step 5: Deploy or Run Locally**

You can now open the index.html file directly in your browser to run it locally. For a better experience, you can deploy it to a hosting service like Netlify, Vercel, or GitHub Pages.

## **🧑‍💻 How to Use the App**

1. **Sign In**: Open the app and sign in with your Google account.  
2. **Open Settings**: The first time you sign in, the Settings modal will likely appear. If not, click the gear icon ⚙️ in the top right.  
3. **Enter Your API Key**: Paste your **Gemini API Key** into the designated field.  
4. **Set Your Calorie Target**:  
   * Use the **Calorie Needs Calculator** to estimate your daily target.  
   * Or, manually enter a **Daily Calorie Target**.  
5. **Save Settings**: Click **Save**. Your settings are now securely stored in your Firebase account.  
6. **Start Logging\!**: Use the chat interface to log your food and exercise. Enjoy your personalized AI diet tracker\!
