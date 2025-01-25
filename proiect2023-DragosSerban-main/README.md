## Smart Streaming Recommendation System

This project aims to develop a smart recommendation system for a streaming platform. The application handles streams of music, podcasts, and audiobooks, leveraging existing user and creator data to provide personalized recommendations. It processes user interaction commands and modifies data accordingly to ensure accurate recommendations.

### Functionality

The application reads input data from CSV files, processes commands from a text file, and outputs results to the console. Commands enable the addition of streams, user listening history updates, and stream recommendations based on user preferences.

### Input Data

#### Streamers
##### File: streamers.csv
##### Each line contains:
##### streamerType: Integer representing the type of streamer (1 - musician, 2 - podcast host, 3 - audiobook author).
##### id: Unique integer ID.
##### name: Name of the streamer.

#### Streams
##### File: streams.csv
##### Each line contains:
##### streamType: Integer representing the type of stream (1 - song, 2 - podcast, 3 - audiobook).
##### id: Unique integer ID.
##### streamGenre: Genre of the stream (varies by stream type).
##### noOfStreams: Long integer for the total number of listens.
##### streamerId: ID of the associated streamer.
##### length: Duration in seconds.
##### dateAdded: Unix timestamp of when the stream was added.
##### name: Name of the stream.

#### Users
##### File: users.csv
##### Each line contains:
##### id: Unique integer ID.
##### name: Name of the user.
##### streams: Space-separated list of stream IDs representing the user's listening history.

### Commands
#### Streamer Commands
##### Add Stream
Format: <streamerId> ADD <streamType> <id> <streamGenre> <length> <name>
Adds a stream for a given streamer. Updates application data but does not produce console output.
##### List Streams
Format: <streamerId> LIST
Displays a JSON-formatted list of a streamer's streams, including fields like id, name, length (formatted as HH:MM:SS or MM:SS), and dateAdded.
##### Delete Stream
Format: <streamerId> DELETE <streamId>
Removes a stream from the application. Updates data but does not produce console output.

#### User Commands
##### List User History
Format: <userId> LIST
Displays a JSON-formatted list of streams the user has listened to.
##### Listen to Stream
Format: <userId> LISTEN <streamId>
Updates the user's history and increments the stream's listen count.
##### Recommend Streams
Format: <userId> RECOMMEND [SONG | PODCAST | AUDIOBOOK]
Displays up to 5 unlistened streams with the highest listen counts for the specified type, from creators the user has already listened to.
##### Surprise Recommendation
Format: <userId> SURPRISE [SONG | PODCAST | AUDIOBOOK]
Displays up to 3 recently added streams from unlistened creators of the specified type.

### Design patterns
The application implements several design patterns:

#### Factory Pattern:
Used to create instances of Streamer, Stream, and commands. Centralizes object creation logic.
#### Singleton Pattern:
Ensures that classes like StreamerFactory, StreamFactory, and Data have only one instance throughout the application's lifecycle.
#### Command Pattern:
Encapsulates commands as objects, allowing for flexible and reusable command execution.
#### Iterator Pattern:
Provides a standardized way to iterate through streams for recommendation algorithms (e.g., top 5 streams by listens or top 3 recently added streams).
#### Observer Pattern:
Updates related entities (e.g., incrementing listen counts when a user listens to a stream) to maintain consistency.
