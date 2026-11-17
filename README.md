
# Bite Log

Bite Log is a calorie-tracking web app prototype. Users create an account, enter their body measurements and goal weight, and the app calculates a daily calorie target. They then log meals by photographing food or entering it by hand, and track their day on a calorie ring. The interface is available in 12 languages.

Built for the COS 496 Capstone course by Dontavius Short, with Claude used to help generate and refine code.

**Live prototype:** https://claude.ai/artifact/TqyXChjgQWsGGrdkJgjsr7

## Features

- Username and password login, plus account creation (password of 8+ characters)
- Goal setup before first use: gender, age, height, current weight, goal weight (lose or gain) and activity level, in kg/cm or lb/in
- Daily calorie target and estimated weeks to reach the goal
- Menu screen with a calorie ring showing calories eaten, left or over
- Camera food logging: take a photo, review the food guess, adjust the portion (0.5 to 10 servings) and add it to the log
- Manual food entry and a log where entries can be deleted
- 12 languages: English, Spanish, French, Portuguese, Russian, Chinese, Japanese, German, Italian, Hindi, Arabic (right-to-left) and Korean

## Tech Stack

- **Web app:** HTML, CSS and JavaScript in a single file, with no build step or dependencies
- **Reference logic and tests:** Python (developed on 3.12; requires 3.8 or newer), using only the standard library

## Getting Started

### Prerequisites

- A current web browser (Chrome, Edge, Firefox or Safari)
- To use the camera, open the app on a phone. On a computer, the "Take photo" button opens a file picker so you can choose a saved photo instead.
- Python 3.8+ only if you want to run the unit tests

### Run the app

1. Clone or download this repository.
2. Open `src/bite-log-full-prototype.html` in your browser (double-click it, or right-click and choose "Open with").
3. Log in with the demo account, or create your own.

| Username | Password |
|---|---|
| `demo` | `Passw0rd` |

Accounts, goals and food logs are saved in your browser's local storage. They do not carry over to another browser or device.

## How It Works

1. **Log in or create an account.**
2. **Set your goal (first login).** The app estimates your daily calories from your measurements.
3. **Use the menu.** Scan food, view today's log, edit your goal, change the language or log out.
4. **Log meals.** Photograph food or enter it manually. The calorie ring updates after every entry.

### Calorie calculation

- Base metabolic rate uses the Mifflin-St Jeor equation: 10 × weight (kg) + 6.25 × height (cm) − 5 × age, then + 5 (male), − 161 (female) or − 78 (other).
- That value is multiplied by an activity factor: 1.2, 1.375, 1.55, 1.725 or 1.9.
- To lose or gain weight, the target is adjusted by 550 kcal per day (about 0.5 kg per week). If the goal is within 0.5 kg of the current weight, the target is a maintenance value.
- Targets are never below 1,200 kcal (1,500 for male) and never above 4,000 kcal.
- The app is for adults only, so age must be 18 or older.

## Project Structure

```
bite-log/
├── src/
│   └── bite-log-full-prototype.html   # the web app
├── auth.py                            # reference authentication logic (Python)
├── food_scanner.py                    # reference food-scan and calorie-log logic (Python)
├── tests/
│   ├── test_auth.py
│   └── test_food_scanner.py
├── docs/                              # user manual, test case matrix, UI/UX documentation
├── README.md
└── .gitignore
```

## Running the Tests

The Python unit tests cover login, password rules, password reset, session timeout, food scanning and the calorie log (31 tests). From the repository root:

```
python3 -m unittest discover -s tests -v
```

Manual test cases for the web app (login, calorie calculation, photo scanning, language switching and more) are in the test case matrix in `docs/`.

## Known Limitations

This is a prototype.

- **Food recognition is a demo.** The app guesses the food from the photo's average color and brightness. Very dark photos are rejected. A finished version would call a food-recognition service.
- **Data is stored only in the browser.** There is no server or database.
- **Passwords in the web app use a simple, non-secure hash** that is fine for a demo but not for real use. The Python reference module shows the intended approach (salted PBKDF2).
- **No password reset** in the web app. The Python module includes a reset flow.
- Two small notes (the demo account hint and the "simplified estimate" note) are not yet translated into every language.

## Roadmap

- Replace the photo-color demo with a real food-recognition service
- Add a server, database and secure password handling
- Split the single HTML file into separate HTML, CSS and JavaScript files
- Add progress charts and a weight history

## Author

Dontavius Short, COS 496 Capstone
````


