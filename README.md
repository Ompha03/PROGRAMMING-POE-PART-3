# PROGRAMMING-POE-PART-3
This is part 3 ( final part ) of the Programming POE
# ChatApp / QuickChat: Part 3 (Store Data and Display Task Report)

**Module:** PROG5121 Programming 1A
**Author:** Ompha Maluma (St105398986)

A console-based chat application written in Java. Part 1 added registration and login, Part 2 added sending messages, and **Part 3** adds arrays to hold every message and a **Stored Messages** menu for searching, deleting and reporting.

## Features in Part 3

The application fills these arrays while it runs (nothing is hard-coded):

| Array | Contents |
|-------|----------|
| Sent messages | Every message the user sent |
| Disregarded messages | Every message the user discarded |
| Stored messages | Messages stored to `messages.json`, including those loaded from the file when the app starts |
| Message hashes | The hash of every message |
| Message IDs | The ID of every message |

Recipient, message text and flag are kept in parallel arrays, so index *i* in each list describes the same message.

### Main menu

```
1. Send Messages
2. Show recent sent Messages     (Coming soon)
3. Quit
4. Stored Messages
```

### Stored Messages menu (option 4)

| Option | What it does |
|--------|--------------|
| 1 | Displays the sender and recipient of all stored messages |
| 2 | Displays the longest stored message |
| 3 | Searches for a message ID and shows the recipient and message |
| 4 | Lists all sent or stored messages for a recipient |
| 5 | Deletes a message using its message hash |
| 6 | Displays a report with the full details of all stored messages |
| 7 | Returns to the main menu |

## Project structure

| File | Purpose |
|------|---------|
| `ChatApp.java` | Main class: registration, login, main menu, sending messages |
| `LogIn.java` | Username, password and cell phone checks, plus login messaging |
| `Message.java` | Message ID, hash, validation, JSON storing and reading |
| `MessageManager.java` | Part 3 arrays, searches, delete, report and the Stored Messages menu |
| `MessageManagerTest.java` | JUnit tests for the Part 3 features |

All classes are in the package `com.mycompany.chatapp`.

## How message hashes work

A hash is made of the first two digits of the message ID, a colon, the message number, a colon, then the first and last words of the message, in capitals with punctuation removed. For example, `Hi Mike, can you join us for dinner tonight?` with ID `00...` and message number 0 gives `00:0:HITONIGHT`.

## Requirements

- Java (JDK) and Maven
- Gson (used to store and read `messages.json`)
- JUnit 5 (for the unit tests)

## Running the application

1. Clone the repository and open it in NetBeans (or any Maven-aware IDE).
2. Run `ChatApp.java`.
3. Register with a username, password and South African cell number, then log in.
4. Use the main menu. Messages stored with option 3 are written to `messages.json` in the project folder and are loaded again the next time the app starts.

## Running the unit tests

In the IDE, right-click `MessageManagerTest.java` and choose **Test File**, or from the command line run:

```
mvn test
```

The tests use the Part 3 test data:

| # | Recipient | Message | Flag |
|---|-----------|---------|------|
| 1 | +27834557896 | Did you get the cake? | Sent |
| 2 | +27838884567 | Where are you? You are late! I have asked you to be on time. | Stored |
| 3 | +27834484567 | Yohoooo, I am at your gate. | Disregard |
| 4 | 0838884567 | It is dinner time! | Sent |
| 5 | +27838884567 | Ok, I am leaving without you. | Stored |

They check that the arrays are populated correctly, the longest message, the message ID search (message 4, ID `0838884567`), the recipient search (`+27838884567`), delete by hash (message 2), the hash format, and the sent messages report.

## Continuous integration

A GitHub Actions workflow runs `mvn test` on every push so the tests run with every change. Check the **Actions** tab on GitHub for the latest results.

## Known limitations

- Deleting a stored message by hash removes it from the arrays but not from `messages.json`, so it is loaded again the next time the app starts.
- The message number in a hash comes from the loop counter, which restarts for each batch of messages. Two messages from different batches can therefore share a hash, and delete removes the first match.


