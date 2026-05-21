# MoneyTransaction

MoneyTransaction is a legacy Android app for tracking small personal money transactions by person. The installed app name is `Ledger`.

The app is built around a simple use case: record who you lent money to or borrowed money from, group transactions by person, and quickly see the current net amount.

## Features

- Track transactions by person
- Add a transaction with:
  - person name
  - amount
  - transaction type
  - reason
  - current time or manually selected date/time
- View the total net amount across all people
- Open a person detail screen to view individual transaction history
- Search people by name
- Sort people by:
  - recent transaction
  - largest amount to repay
  - largest amount to receive
  - name ascending
  - name descending
  - number of transactions
- Delete a person entry or an individual transaction
- Persist data locally as `transactions.json`

## Transaction Model

The app stores transactions in memory through `TransactionEngine`, grouped by `PersonalTransaction`.

`Transaction.GET_BACK` represents money to receive back and is stored as a positive value.

`Transaction.LEND` represents money to pay back and is stored as a negative value.

The current balance for each person is calculated by summing all transaction values for that person. The main screen total is the sum of every person's balance.

## Data Storage

Data is serialized with Gson and saved to the app's internal files directory:

```text
transactions.json
```

The app does not use a remote server, account login, cloud sync, or database.

## Tech Stack

- Java
- Android SDK
- Android Gradle Plugin 3.4.2
- AndroidX AppCompat
- RecyclerView
- CardView
- ConstraintLayout
- Gson

## Project Structure

```text
app/src/main/java/shyunku/project/moneytransaction/
  MainActivity.java              Main list, search, sort, add transaction
  PersonalDetailActivity.java    Per-person transaction detail screen
  TransactionEngine.java         In-memory grouped transaction state
  PersonalTransaction.java       Person-level transaction collection
  Transaction.java               Single transaction model
  FileManager.java               Gson-based local save/load
  PersonalRecyclerAdapter.java   Main list adapter
  DetailListAdapter.java         Detail list adapter
  ComparatorEngine.java          Sort comparator factory
```

## Build

This is an older Android project. The most reliable way to open it is with Android Studio using the included Gradle wrapper.

```bash
./gradlew assembleDebug
```

On Windows:

```powershell
.\gradlew.bat assembleDebug
```

The project currently targets:

- `compileSdkVersion 29`
- `minSdkVersion 24`
- `targetSdkVersion 29`

## Current Limitations

- This is a legacy project and uses older Gradle/Android dependencies.
- `jcenter()` is still present in the Gradle configuration.
- There is no cloud sync or backup flow.
- Unit and instrumentation test files are still the default Android template tests.
- Some menu actions are placeholders or partial implementations, such as settlement/edit flows.
- The app requests external storage permissions, but the current save path uses the app's internal files directory.

## Status

Archived legacy project. Useful as a record of an early Android app that implements local transaction tracking, RecyclerView-based lists, sorting, filtering, and simple file persistence.
