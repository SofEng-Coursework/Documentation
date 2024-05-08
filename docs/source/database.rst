Database
=========
FirebaseProvider
-----------------
Properties
-----------
FIREBASE_APP: FirebaseApp
  The entry point of the Firebase SDK.

FIREBASE_AUTH: FirebaseAuth
  Used for all authentication operations.

FIREBASE_FIRESTORE: FirebaseFirestore
  Used for all Firestore database operations.

Methods
--------
initialize(): Future<void>
  Initializes the Firebase app with default options. Sets up instances for FIREBASE_AUTH and FIREBASE_FIRESTORE. Sets up a listener for auth state changes. Delay of 250 milliseconds before completion.

initializeMock(): Future<void>
  Initializes mock instances for FIREBASE_AUTH and FIREBASE_FIRESTORE for testing purposes. Delay of 250 milliseconds before completion.

getLoggedInUser(): User?
  Returns the currently logged in user. Returns null if no user is logged in.