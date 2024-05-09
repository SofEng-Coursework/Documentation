API Reference
==============
FirebaseProvider
-----------------
**Properties:**

FIREBASE_APP: FirebaseApp
  The entry point of the Firebase SDK.

FIREBASE_AUTH: FirebaseAuth
  Used for all authentication operations.

FIREBASE_FIRESTORE: FirebaseFirestore
  Used for all Firestore database operations.

**Methods:**

initialize(): Future<void>
  Initializes the Firebase app with default options. Sets up instances for FIREBASE_AUTH and FIREBASE_FIRESTORE. Sets up a listener for auth state changes. Delay of 250 milliseconds before completion.

initializeMock(): Future<void>
  Initializes mock instances for FIREBASE_AUTH and FIREBASE_FIRESTORE for testing purposes. Delay of 250 milliseconds before completion.

getLoggedInUser(): User?
  Returns the currently logged in user. Returns null if no user is logged in.

AccountController
-----------------
**Properties:**

firebaseProvider: FirebaseProvider
  Instance of FirebaseProvider for accessing Firebase services.
collectionName: String
  Name of the Firestore collection to be used for storing account data.

**Methods:**

signUp(String email, String password, String name, String phone): Future<ErrorStatus>
  Signs up a new user with provided credentials. Returns an ErrorStatus indicating success or failure.

login(String email, String password): Future<ErrorStatus>
  Logs in an existing user with provided credentials. Returns an ErrorStatus indicating success or failure.

getUserData(): Future<Map<String, dynamic>?>
  Retrieves data of the currently logged-in user. Returns a map containing user data, or null if no user is logged in.

signOut(): Future<ErrorStatus>
  Signs out the current user. Returns an ErrorStatus indicating success or failure.

deleteAccount(): Future<ErrorStatus>
  Deletes the current user account. Returns an ErrorStatus indicating success or failure.

updateAccount({String? name, String? phone}): Future<ErrorStatus>
  Updates the current user account information with provided data. Returns an ErrorStatus indicating success or failure.

AdminQueueController
--------------------
**Properties:**

_firebaseProvider: FirebaseProvider
  Instance of FirebaseProvider for accessing Firebase services.

**Methods:**

addQueue(String name, int? capacity, String owner): Future<ErrorStatus>
  Adds a new queue to the Firestore database with provided details. Returns an ErrorStatus indicating success or failure.

getQueues(): Stream<List<Queue>>
  Returns a Stream of all queues owned by the current admin.

getFeedback(String queueID): Stream<List<FeedbackEntry>>
  Returns a Stream of feedback entries for a specific queue.

toggleQueueOpenStatus(Queue queue): Future<ErrorStatus>
  Toggles the open status of a queue. Returns an ErrorStatus indicating success or failure.

deleteQueue(Queue queue): Future<ErrorStatus>
  Deletes a queue from the Firestore database. Returns an ErrorStatus indicating success or failure.

getQueue(String queueID): Stream<Queue>
  Returns a Stream of a specific queue.

removeUserFromQueue(Queue queue, QueueUserEntry user): Future<ErrorStatus>
  Removes a user from a queue. Returns an ErrorStatus indicating success or failure.

addUserToQueue(Queue queue, String user): Future<ErrorStatus>
  Adds a user to a queue. Returns an ErrorStatus indicating success or failure.

moveUserUp(Queue queue, QueueUserEntry user): Future<ErrorStatus>
  Moves a user up in the queue. Returns an ErrorStatus indicating success or failure.

moveUserDown(Queue queue, QueueUserEntry user): Future<ErrorStatus>
  Moves a user down in the queue. Returns an ErrorStatus indicating success or failure.

UserQueueController
-----------------
**Properties:**

_firebaseProvider: FirebaseProvider
  Instance of FirebaseProvider for accessing Firebase services.

**Methods:**

joinQueue(Queue queue): Future<ErrorStatus>
  Joins a user to the specified queue. Returns an ErrorStatus indicating success or failure.

leaveQueue(Queue queue): Future<ErrorStatus>
  Removes a user from the specified queue. Returns an ErrorStatus indicating success or failure.

getQueues(): Stream<List<Queue>>
  Returns a Stream of all queues available.

getCurrentQueue(): Stream<Queue?>
  Returns a Stream of the current queue the user is in, if any.

getCurrentQueuePosition(): Stream<int>
  Returns a Stream of the current position of the user in the queue, if any.

removeFeedbackPrompt(String queueId, String userId): Future<ErrorStatus>
  Removes a queue from the user's feedback prompt list. Returns an ErrorStatus indicating success or failure.

submitFeedback(String queueId, FeedbackEntry entry): Future<ErrorStatus>
  Submits feedback for a specific queue. Returns an ErrorStatus indicating success or failure.

AdminAccountController
-----------------
**Properties:**

_firebaseProvider: FirebaseProvider
  Instance of FirebaseProvider for accessing Firebase services.

**Methods:**

signUp(String email, String password, String name, String phone): Future<ErrorStatus>
  Signs up a new admin account with provided credentials. Returns an ErrorStatus indicating success or failure.

login(String email, String password): Future<ErrorStatus>
  Logs in an existing admin account with provided credentials. Returns an ErrorStatus indicating success or failure.

getUserData(): Future<Map<String, dynamic>?>
  Retrieves data of the currently logged-in admin. Returns a map containing admin data, or null if no admin is logged in.

signOut(): Future<ErrorStatus>
  Signs out the current admin. Returns an ErrorStatus indicating success or failure.

deleteAccount(): Future<ErrorStatus>
  Deletes the current admin account. Returns an ErrorStatus indicating success or failure.

updateAccount({String? name, String? phone}): Future<ErrorStatus>
  Updates the current admin account information with provided data. Returns an ErrorStatus indicating success or failure.

DataController
-----------------
**Methods:**

getWaitTimes(Queue queue): List<Duration>
  Returns a list of wait times (in milliseconds) for each user in the queue.

getMedianWaitTime(Queue queue): Duration
  Returns the median wait time (in milliseconds) for users in the queue.

getLogsForHour(List<QueueLog> logsForDay, int hour): List<QueueLog>
  Returns the logs for a specific hour of the day.

getLogsForDate(Queue queue, DateTime date): List<QueueLog>
  Returns the logs for a specific date for the given queue.

getMedianWaitTimeForHour(List<QueueLog> logsForDay, int hour): Duration
  Returns the median wait time (in milliseconds) for a specific hour of the day.

getMedianWaitTimeForDate(Queue queue, DateTime date): Duration
  Returns the median wait time (in milliseconds) for a specific date for the given queue.

getMinMaxQueueLengthForHour(List<QueueLog> logsForDay, int hour): (int, int)
  Returns a tuple containing the minimum and maximum queue lengths for a specific hour of the day.

getMinMaxQueueLengthForDate(Queue queue, DateTime date): (int, int)
  Returns a tuple containing the minimum and maximum queue lengths for a specific date for the given queue.

formatTime(int milliseconds): String
  Formats the given milliseconds into a human-readable time format (hours, minutes, or seconds).

checkValidHour(int hour): bool
  Checks if the given hour is valid (between 0 and 24). Returns true if valid, false otherwise.

UserAccountController
---------------------
**Methods:**

signUp(String email, String password, String name, String phone): Future<ErrorStatus>
  Signs up a new user account with provided credentials. Returns an ErrorStatus indicating success or failure.

login(String email, String password): Future<ErrorStatus>
  Logs in an existing user account with provided credentials. Returns an ErrorStatus indicating success or failure.

getUserData(): Future<Map<String, dynamic>?>
  Retrieves data of the currently logged-in user. Returns a map containing user data, or null if no user is logged in.

signOut(): Future<ErrorStatus>
  Signs out the current user. Returns an ErrorStatus indicating success or failure.

deleteAccount(): Future<ErrorStatus>
  Deletes the current user account. Returns an ErrorStatus indicating success or failure.

updateAccount({String? name, String? phone}): Future<ErrorStatus>
  Updates the current user account information with provided data. Returns an ErrorStatus indicating success or failure.

getHistory(): Future<List<Map<String, dynamic>>>
  Gathers all past instances of the user accessing queues to be displayed on the history page. Returns a list of maps containing queue history data.

ErrorStatus
------------

**Properties:**

success: bool
  Indicates whether the operation was successful. Returns true for success and false for failure.

message: String?
  An optional message providing additional details about the error status. Returns null if no message is provided.

**Constructor:**

ErrorStatus({required bool success, String? message})
  Initializes an ErrorStatus instance. The success parameter is required to specify the outcome of the operation. 
  The message parameter is optional and used to provide more details about the error if available.
  
FeedbackEntry
---------------

**Properties:**

userId: String
  Unique identifier for the user providing feedback.

name: String
  The name of the user providing feedback.

comments: String
  Textual comments provided by the user.

rating: int
  Numerical rating provided by the user, typically on a predefined scale (e.g., 1 to 5).

timestamp: int
  Timestamp in milliseconds since the epoch when the feedback entry was created. 
  This is set automatically to the current time when the entry is created.

**Constructor:**

FeedbackEntry({required String userId, required String name, required String comments, required int rating})
  Initializes a new instance of FeedbackEntry with the specified user ID, name, comments, and rating. 
  The timestamp is automatically set to the current time.

**Factory Constructor:**

FeedbackEntry.fromJson(Map<String, dynamic> json)
  Factory constructor that creates an instance of FeedbackEntry from a JSON object. 
  The JSON object must contain keys for 'userId', 'name', 'comments', and 'rating', each with appropriate values.

**Methods:**

toJson(): Map<String, dynamic>
  Converts a FeedbackEntry instance into a JSON map. The resulting map includes keys for 'userId', 'name', 'comments', 'rating', and 'timestamp', 
  corresponding to the properties of the FeedbackEntry.

QueueUserEntry
---------------

**Properties:**

userId: String
  The unique identifier for the user in the queue.

name: String?
  The optional name of the user.

timestamp: int
  Timestamp marking when the user was added to the queue.

**Constructor:**

QueueUserEntry({required String userId, String? name, required int timestamp})
  Initializes a new instance of QueueUserEntry with the specified user ID, optional name, and timestamp.

**Factory Constructor:**

QueueUserEntry.fromJson(Map<String, dynamic> json)
  Creates an instance of QueueUserEntry from a JSON object that includes 'userId', 'name', and 'timestamp'.

**Methods:**

toJson(): Map<String, dynamic>
  Converts the instance into a JSON map.

QueueLog
--------

**Properties:**

userId: String
  The unique identifier for the user associated with this log entry.

start: int
  Start timestamp for the user's queue entry.

end: int
  End timestamp for the user's queue exit.

**Constructor:**

QueueLog({required String userId, required int start, required int end})
  Initializes a new instance of QueueLog with the user ID, start, and end times.

**Factory Constructor:**

QueueLog.fromJson(Map<String, dynamic> json)
  Creates an instance of QueueLog from a JSON object that includes 'userId', 'start', and 'end'.

**Methods:**

toJson(): Map<String, dynamic>
  Converts the instance into a JSON map.
 
Queue
------

**Properties:**

id: String
  Unique identifier for the queue.

name: String
  Name of the queue.

open: bool
  Indicates whether the queue is open.

capacity: int?
  Optional maximum number of users that can be in the queue.

users: List<QueueUserEntry>
  List of users currently in the queue.

logs: List<QueueLog>
  List of logs associated with the queue activities.

**Constructor:**

Queue({required String id, required String name, required bool open, List<QueueUserEntry> users, List<QueueLog> logs, int? capacity})
  Initializes a new instance of Queue with the specified details.

**Methods:**

isFull(): bool
  Returns true if the queue is at full capacity, otherwise false.

**Factory Constructor:**

Queue.fromJson(Map<String, dynamic> json)
  Creates an instance of Queue from a JSON object that includes 'id', 'name', 'open', 'users', 'logs', and optionally 'capacity'.

**Methods:**

toJson(): Map<String, dynamic>
Converts the instance into a JSON map, including details about users and logs.

























