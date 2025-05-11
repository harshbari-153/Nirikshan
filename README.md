# NIRIKSHAN

A fun, user-friendly Streamlit web app designed for my Mother to track her daily activities! The app features a colorful pie chart to visualize activity proportions and an interactive form to log activities, proportions, and notes (supporting Indian languages like Gujarati). Data is stored in a CSV file on GitHub, enabling access across multiple devices.

## Features

- **Upper Section: Pie Chart**
  - Displays a bright, colorful pie chart of activity proportions using Matplotlib and Seaborn.
  - Filters data by time range (Last Week, Last Month, Last 2 Months, Last 6 Months, Last Year, All Records; default: All Records).
  - Shows up to 10 activities with percentages ≥1%, with clear labels and no overlap with the title.

- **Lower Section: Activity Form**
  - **Date Picker**: Select past dates only (defaults to yesterday).
  - **Three Activity Inputs**: Each with a dropdown (from a customizable list of 25 activities like Playing, Cooking, etc.) and a slider (0-100%).
  - **Slider Logic**: Sliders sum to 100; the third slider auto-adjusts (not user-controllable). First slider complements with the third, then the second if needed.
  - **Note Textbox**: Supports up to 500 characters in any Indian language (e.g., Gujarati).
  - **Buttons**:
    - **Submit Activity**: Saves to `activity_records.csv` on GitHub, overwriting existing entries for the same date.
    - **Load Activity**: Retrieves data for the selected date, populating the form (shows an error if no entry exists).
    - **Download Records**: Downloads the sorted CSV file locally.

- **GitHub Integration**: Uses `PyGithub` to store and retrieve `activity_records.csv` from the `Nirikshan` repository, ensuring data persistence across devices.
- **Child-Friendly UI**: Comic Sans font, bright colors (pink, orange, lavender), and rounded edges for an engaging experience.
- **Robust Error Handling**: Handles missing CSV files, invalid data, and GitHub API errors gracefully.

## Prerequisites

- **GitHub Repository**: A repository named `Nirikshan` with `activity_records.csv` initialized (headers: `Date,Activity_1,Activity_1_proportion,Activity_2,Activity_2_proportion,Activity_3,Activity_3_proportion,Note`).
- **GitHub Personal Access Token**: With `repo` scope for read/write access.
- **Streamlit Community Cloud**: For deployment (optional for local use).
- **Python**: Version 3.8+ for local development.

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/harshbari-153/Nirikshan.git
cd Nirikshan
```

### 2. Install Dependencies
Create a virtual environment and install the required packages:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

The `requirements.txt` includes:
```
streamlit
pandas
matplotlib
seaborn
PyGithub
```

### 3. Initialize `activity_records.csv`
Ensure `activity_records.csv` exists in the repository root with the following headers:
```csv
Date,Activity_1,Activity_1_proportion,Activity_2,Activity_2_proportion,Activity_3,Activity_3_proportion,Note
```

### 4. Configure GitHub Token
- Generate a Personal Access Token at `https://github.com/settings/tokens` with `repo` scope.
- For **local use**, set the token as an environment variable:
  ```bash
  export GITHUB_TOKEN="your_token_here"  # On Windows: set GITHUB_TOKEN=your_token_here
  ```
- For **Streamlit Cloud**, add the token to the app's secrets:
  ```toml
  [secrets]
  GITHUB_TOKEN = "your_token_here"
  ```

### 5. Run Locally
```bash
streamlit run app.py
```
The app will open in your browser at `http://localhost:8501`.

### 6. Deploy on Streamlit Community Cloud
- Sign in to `https://share.streamlit.io/`.
- Create a new app, linking it to your `Nirikshan` repository.
- Specify `app.py` as the main file.
- Add the GitHub token to the app's secrets (see above).
- Deploy the app and access it via the provided URL.

## File Structure
```
Nirikshan/
├── app.py                   # Main Streamlit app
├── requirements.txt         # Python dependencies
├── activity_records.csv     # Data storage (CSV)
└── README.md               # This file
```

## Usage
1. **View Pie Chart**:
   - Select a time range (e.g., Last Week) to see a pie chart of activity proportions.
   - The chart updates dynamically, showing up to 10 activities with ≥1% proportions.

2. **Log Activities**:
   - Pick a past date (defaults to yesterday).
   - Choose three activities from the dropdowns.
   - Adjust the first two sliders (0-100%); the third slider auto-adjusts to sum to 100.
   - Add a note (up to 500 characters, supports Gujarati).
   - Click **Submit Activity** to save to GitHub.

3. **Load Activities**:
   - Select a date and click **Load Activity** to populate the form with saved data.
   - If no entry exists, an error message appears.

4. **Download Data**:
   - Click **Download Records** to get the sorted `activity_records.csv`.

## Customization
- **Activity List**: Edit the `activity_list` in `app.py` to change the 25 available activities.
- **UI**: Modify the CSS in `app.py` (under `st.markdown`) to adjust colors, fonts, or styling.
- **CSV Structure**: The app expects 8 columns in `activity_records.csv`. Ensure any manual edits maintain this structure.

## Troubleshooting
- **GitHub Errors**: Verify the token has `repo` scope and the repository name is `Nirikshan`.
- **CSV Issues**: If `activity_records.csv` is missing or malformed, the app initializes it with correct headers.
- **Streamlit Errors**: Check Streamlit Cloud logs (`Manage app` > `Logs`) for details. Ensure `requirements.txt` matches the specified versions.
- **Textbox Not Loading**: Ensure notes in the CSV are valid strings (not `NaN`). Test with Gujarati text to confirm Unicode support.

## Contributing
Feel free to fork this repository, make improvements, and submit pull requests. Suggestions for enhancing the UI or adding features are welcome!

## License
This project is licensed under the MIT License.

## Contact
For questions or feedback, reach out via GitHub Issues or LinkedIn.

---

Built with ❤️ for my mother to make tracking her activities fun and colorful!
