That's a great project idea! Building an online MCQ testing system involves several key components. Let's break down the process step-by-step. We'll focus on a web-based application, which is a common and flexible approach.

Here's a general outline of the architecture and technologies you'd need:

**1. Technology Stack Selection:**

*   **Frontend (User Interface):** This is what your users will interact with.
    *   **HTML:** For structuring the content.
    *   **CSS:** For styling and making it look good.
    *   **JavaScript:** For interactivity (e.g., handling answer selections, timers, dynamic content).
    *   **Frameworks/Libraries (Optional but Recommended):** React, Angular, or Vue.js can significantly speed up development and manage complex UIs.
*   **Backend (Server-side Logic):** This handles data storage, user authentication, processing requests, and serving content to the frontend.
    *   **Programming Language:** Python (with Flask/Django), Node.js (with Express), PHP (with Laravel), Ruby (with Rails), or Java (with Spring Boot) are popular choices.
    *   **Database:** Where your questions, options, answers, user data, and test results will be stored.
        *   **Relational Databases:** PostgreSQL, MySQL, SQLite (good for beginners/small projects).
        *   **NoSQL Databases:** MongoDB (if you prefer a document-based approach).
*   **Excel File Processing:** You'll need a library on the backend to read and parse your uploaded Excel files.
    *   **Python:** `pandas` and `openpyxl` are excellent.
    *   **Node.js:** `xlsx`
    *   **PHP:** `PhpSpreadsheet`

**2. Core Features and Components:**

*   **User Management:**
    *   Registration/Login for administrators (you) and potentially students.
    *   Role-based access (admin can upload questions, create tests; students can take tests).
*   **Question Management (Admin Panel):**
    *   **Upload Questions:** This is where your Excel file upload functionality comes in.
    *   View, Edit, Delete existing questions.
    *   Categorize questions (e.g., by subject, topic).
*   **Test Creation (Admin Panel):**
    *   Create new tests/quizzes.
    *   Select questions to include in a test.
    *   Set test parameters (e.g., duration, number of attempts, whether to shuffle questions/options).
*   **Test Taking (Student Interface):**
    *   Display questions and options clearly.
    *   Allow users to select answers.
    *   Implement a timer (optional).
    *   Prevent navigation away from the test or other cheating mechanisms (can be complex).
    *   Submission of answers.
*   **Result Management:**
    *   Automatic scoring of tests.
    *   Display results to students immediately or later.
    *   Admin view of all test results, student performance, question analysis.

**3. Database Schema Design (Example using a relational database):**

Here's a simplified look at how your tables might be structured:

*   **`Users` Table:**
    *   `id` (Primary Key)
    *   `username`
    *   `email`
    *   `password_hash`
    *   `role` (e.g., 'admin', 'student')
*   **`Questions` Table:**
    *   `id` (Primary Key)
    *   `question_text`
    *   `question_type` (e.g., 'MCQ')
    *   `points` (e.g., 1)
    *   `created_at`
*   **`Options` Table:**
    *   `id` (Primary Key)
    *   `question_id` (Foreign Key to `Questions.id`)
    *   `option_text`
    *   `is_correct` (Boolean: true/false)
*   **`Tests` Table:**
    *   `id` (Primary Key)
    *   `test_name`
    *   `duration_minutes`
    *   `created_by` (Foreign Key to `Users.id`)
    *   `created_at`
*   **`Test_Questions` (Junction table for Many-to-Many relationship between Tests and Questions):**
    *   `test_id` (Foreign Key to `Tests.id`)
    *   `question_id` (Foreign Key to `Questions.id`)
*   **`Submissions` Table:**
    *   `id` (Primary Key)
    *   `user_id` (Foreign Key to `Users.id`)
    *   `test_id` (Foreign Key to `Tests.id`)
    *   `submitted_at`
    *   `score`
*   **`Answer_Attempts` Table:**
    *   `id` (Primary Key)
    *   `submission_id` (Foreign Key to `Submissions.id`)
    *   `question_id` (Foreign Key to `Questions.id`)
    *   `selected_option_id` (Foreign Key to `Options.id` - can be null if skipped)
    *   `is_correct` (Boolean: calculated upon submission)

**4. Step-by-Step Development Process:**

**Phase 1: Setup and Basic Functionality**

1.  **Choose your Tech Stack:** Decide on your backend language/framework and database. (e.g., Python Flask + PostgreSQL, or Node.js Express + MongoDB).
2.  **Project Setup:** Create your project directory, set up your development environment, and install necessary dependencies.
3.  **Database Connection:** Configure your application to connect to your chosen database.
4.  **User Authentication (Admin):**
    *   Create `Users` table.
    *   Implement a simple admin registration/login form and backend logic. Use secure password hashing (e.g., bcrypt).
    *   A good place to start would be to create the admin login/registration page: 

**Phase 2: Question Management (Admin)**

1.  **Database Schema for Questions and Options:** Create the `Questions` and `Options` tables.
2.  **Excel Upload Endpoint:**
    *   Create an HTML form with a file input field for uploading Excel files.
    *   On the backend, create an API endpoint (e.g., `/upload_questions`).
    *   When a file is uploaded, use your chosen Excel parsing library (`pandas`/`openpyxl` for Python) to read the data.
    *   **Data Structure in Excel:** Each row could represent a question. Columns might be: `Question Text`, `Option 1`, `Option 2`, `Option 3`, `Option 4`, `Correct Option Number` (e.g., 1, 2, 3, or 4).
    *   **Validation:** Validate the data from the Excel file (e.g., ensure all required fields are present, correct option number is valid).
    *   **Save to Database:** Insert the questions and their options into your `Questions` and `Options` tables.

    *Example of an Admin Panel for Question Upload:*

3.  **View/Edit/Delete Questions:** Create a page where admins can see a list of all questions, search, filter, and individually edit or delete them.

**Phase 3: Test Creation and Taking**

1.  **Database Schema for Tests, Submissions, Answer Attempts:** Create these tables.
2.  **Test Creation (Admin):**
    *   Create a form for admins to define a new test (name, description, duration).
    *   Allow admins to select questions from the question bank to add to the test. This will populate the `Test_Questions` junction table.
3.  **Student Registration/Login:** Implement a similar process for students, potentially with a separate role.
4.  **Test List for Students:** A page where students can see available tests.
5.  **Test Taking Interface:**
    *   When a student starts a test, fetch the questions and options for that test.
    *   Display one question at a time or all questions on one page.
    *   Implement radio buttons for MCQ option selection.
    *   Add a submit button.
    *   **Timer (Optional but recommended):** Use JavaScript for a countdown timer on the client-side.
6.  **Submission Handling:**
    *   When a student submits, record their `submission_id`, `user_id`, `test_id`, and `submitted_at` in the `Submissions` table.
    *   For each question, record their `selected_option_id` in the `Answer_Attempts` table.
    *   **Scoring:** Compare `selected_option_id` with `Options.is_correct` to calculate the score and update `Submissions.score`.

    *A typical student test-taking interface could look like this:* 

**Phase 4: Results and Enhancements**

1.  **Student Results Page:** Display the student's score, correct/incorrect answers, and possibly explanations.
2.  **Admin Results Dashboard:** Allow admins to view all test submissions, filter by student, test, etc.
3.  **Security:**
    *   Protect against SQL injection, XSS attacks.
    *   Ensure proper authorization (e.g., students can only see their own results, not others').
4.  **Error Handling:** Implement robust error handling for file uploads, database operations, etc.
5.  **User Interface/User Experience (UI/UX):** Make sure the application is easy to use and visually appealing.

**Example Excel File Structure:**

| Question Text                                   | Option 1      | Option 2        | Option 3     | Option 4     | Correct Option No. | Points |
| :---------------------------------------------- | :------------ | :-------------- | :----------- | :----------- | :----------------- | :----- |
| What is the capital of France?                  | London        | Berlin          | Paris        | Rome         | 3                  | 1      |
| Which planet is known as the Red Planet?        | Earth         | Mars            | Jupiter      | Venus        | 2                  | 1      |
| What is the largest ocean on Earth?             | Atlantic      | Indian          | Arctic       | Pacific      | 4                  | 1      |


---
---
**Getting Started:**
Okay, that's an interesting combination! Typically, you'd choose one primary backend language, but using Python for specific tasks (like heavy data processing or machine learning) alongside a Node.js web server is a valid architectural pattern (often called a microservices approach or using Python for specific APIs).

For this MCQ system, we can design it as follows:

*   **Node.js (with Express.js):** Will serve as the main web server, handling user authentication, routing, serving the frontend, and managing most API requests.
*   **Python (with Flask or a script):** Will be specifically used for the Excel file processing, as Python's `pandas` library is exceptionally powerful for this. Node.js can then call this Python script or a small Flask service when an Excel file is uploaded.
*   **Frontend:** We can use plain HTML, CSS, and JavaScript for simplicity, or a lightweight library like Vue.js (which integrates well with Node.js backends).
*   **Database:** PostgreSQL or MySQL are great choices, as both Node.js and Python have excellent libraries for interacting with them. Let's assume **PostgreSQL** for this guide.

---

Let's break down the setup and the first few steps using this hybrid approach.

**Project Structure:**

```
mcq-system/
├── backend-nodejs/
│   ├── src/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── server.js          # Main Node.js app
│   │   └── db.js              # Database connection
│   ├── package.json
│   └── .env
├── python-excel-processor/
│   ├── excel_processor.py     # Python script to handle Excel
│   ├── requirements.txt
│   └── data/                  # Temp storage for uploaded files
├── frontend/
│   ├── public/
│   │   ├── index.html
│   │   ├── css/
│   │   └── js/
│   └── package.json           # If using a frontend framework
└── README.md
```

---

**Step 1: Database Setup (PostgreSQL)**

First, ensure you have PostgreSQL installed and running.

1.  **Create a database:**
    ```sql
    CREATE DATABASE mcq_quiz_db;
    ```
2.  **Create User Tables:** Connect to `mcq_quiz_db` and run these commands.

    ```sql
    -- Users Table
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        username VARCHAR(50) UNIQUE NOT NULL,
        email VARCHAR(100) UNIQUE NOT NULL,
        password_hash VARCHAR(255) NOT NULL,
        role VARCHAR(20) DEFAULT 'student' NOT NULL, -- 'admin' or 'student'
        created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
    );

    -- Questions Table
    CREATE TABLE questions (
        id SERIAL PRIMARY KEY,
        question_text TEXT NOT NULL,
        question_type VARCHAR(50) DEFAULT 'MCQ' NOT NULL,
        points INTEGER DEFAULT 1 NOT NULL,
        created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
    );

    -- Options Table
    CREATE TABLE options (
        id SERIAL PRIMARY KEY,
        question_id INTEGER NOT NULL REFERENCES questions(id) ON DELETE CASCADE,
        option_text VARCHAR(255) NOT NULL,
        is_correct BOOLEAN DEFAULT FALSE NOT NULL
    );

    -- Tests Table
    CREATE TABLE tests (
        id SERIAL PRIMARY KEY,
        test_name VARCHAR(255) NOT NULL,
        description TEXT,
        duration_minutes INTEGER,
        created_by INTEGER REFERENCES users(id) ON DELETE SET NULL, -- Admin who created it
        created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
    );

    -- Junction table for Tests and Questions (Many-to-Many)
    CREATE TABLE test_questions (
        test_id INTEGER NOT NULL REFERENCES tests(id) ON DELETE CASCADE,
        question_id INTEGER NOT NULL REFERENCES questions(id) ON DELETE CASCADE,
        PRIMARY KEY (test_id, question_id)
    );

    -- Submissions Table
    CREATE TABLE submissions (
        id SERIAL PRIMARY KEY,
        user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
        test_id INTEGER NOT NULL REFERENCES tests(id) ON DELETE CASCADE,
        submitted_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
        score INTEGER,
        total_points INTEGER
    );

    -- Answer Attempts Table
    CREATE TABLE answer_attempts (
        id SERIAL PRIMARY KEY,
        submission_id INTEGER NOT NULL REFERENCES submissions(id) ON DELETE CASCADE,
        question_id INTEGER NOT NULL REFERENCES questions(id) ON DELETE CASCADE,
        selected_option_id INTEGER REFERENCES options(id) ON DELETE SET NULL, -- Can be null if skipped
        is_correct BOOLEAN -- Calculated
    );

    ```

---

**Step 2: Node.js Backend Setup**

Navigate to the `backend-nodejs` directory.

1.  **Initialize Node.js Project:**
    ```bash
    cd backend-nodejs
    npm init -y
    ```
2.  **Install Dependencies:**
    ```bash
    npm install express pg bcryptjs jsonwebtoken dotenv multer cors
    ```
    *   `express`: Web framework.
    *   `pg`: PostgreSQL client.
    *   `bcryptjs`: For password hashing.
    *   `jsonwebtoken`: For authentication tokens.
    *   `dotenv`: To load environment variables.
    *   `multer`: For handling file uploads (specifically for the Excel file).
    *   `cors`: For enabling Cross-Origin Resource Sharing.

3.  **`backend-nodejs/.env` file:** Create this file and add your database credentials and a secret key.

    ```
    PORT=5000
    DATABASE_URL="postgresql://your_user:your_password@localhost:5432/mcq_quiz_db"
    JWT_SECRET="supersecretjwtkey" # Change this to a strong, random string in production
    ```

4.  **`backend-nodejs/src/db.js` (Database Connection):**

    ```javascript
    const { Pool } = require('pg');
    require('dotenv').config();

    const pool = new Pool({
        connectionString: process.env.DATABASE_URL,
    });

    pool.on('error', (err) => {
        console.error('Unexpected error on idle client', err);
        process.exit(-1);
    });

    module.exports = {
        query: (text, params) => pool.query(text, params),
        getClient: () => pool.connect(),
    };
    ```

5.  **`backend-nodejs/src/server.js` (Main Application File):**

    ```javascript
    const express = require('express');
    const cors = require('cors');
    require('dotenv').config();
    const path = require('path'); // For serving static files

    const app = express();
    const PORT = process.env.PORT || 5000;

    // Middleware
    app.use(cors());
    app.use(express.json()); // For parsing application/json
    app.use(express.urlencoded({ extended: true })); // For parsing application/x-www-form-urlencoded

    // Serve static files from the frontend build directory (once you have it)
    // For now, let's assume your frontend is in frontend/public
    app.use(express.static(path.join(__dirname, '../../frontend/public')));


    // --- Import Routes ---
    const authRoutes = require('./routes/authRoutes');
    const questionRoutes = require('./routes/questionRoutes');
    // ... more routes will go here

    // --- Use Routes ---
    app.use('/api/auth', authRoutes);
    app.use('/api/questions', questionRoutes);
    // ...

    // Root route to serve your index.html
    app.get('/', (req, res) => {
        res.sendFile(path.join(__dirname, '../../frontend/public', 'index.html'));
    });


    // Start the server
    app.listen(PORT, () => {
        console.log(`Node.js Backend listening on port ${PORT}`);
    });
    ```

6.  **`backend-nodejs/src/routes/authRoutes.js` (Authentication Routes - Admin Login/Register):**

    ```javascript
    const express = require('express');
    const router = express.Router();
    const bcrypt = require('bcryptjs');
    const jwt = require('jsonwebtoken');
    const db = require('../db'); // Our database connection
    require('dotenv').config();

    // Register an Admin (can be done once manually or via a setup script)
    router.post('/register-admin', async (req, res) => {
        const { username, email, password } = req.body;
        try {
            const hashedPassword = await bcrypt.hash(password, 10);
            const result = await db.query(
                'INSERT INTO users (username, email, password_hash, role) VALUES ($1, $2, $3, $4) RETURNING id, username, email, role',
                [username, email, hashedPassword, 'admin']
            );
            const user = result.rows[0];
            const token = jwt.sign({ id: user.id, role: user.role }, process.env.JWT_SECRET, { expiresIn: '1h' });
            res.status(201).json({ message: 'Admin registered successfully', token, user: { id: user.id, username: user.username, role: user.role } });
        } catch (err) {
            console.error(err);
            if (err.code === '23505') { // Unique violation
                return res.status(400).json({ message: 'Username or email already exists.' });
            }
            res.status(500).json({ message: 'Server error during admin registration.' });
        }
    });

    // Login route
    router.post('/login', async (req, res) => {
        const { email, password } = req.body;
        try {
            const result = await db.query('SELECT * FROM users WHERE email = $1', [email]);
            const user = result.rows[0];

            if (!user) {
                return res.status(400).json({ message: 'Invalid credentials.' });
            }

            const isMatch = await bcrypt.compare(password, user.password_hash);
            if (!isMatch) {
                return res.status(400).json({ message: 'Invalid credentials.' });
            }

            const token = jwt.sign({ id: user.id, role: user.role }, process.env.JWT_SECRET, { expiresIn: '1h' });
            res.json({ message: 'Logged in successfully', token, user: { id: user.id, username: user.username, role: user.role } });

        } catch (err) {
            console.error(err);
            res.status(500).json({ message: 'Server error during login.' });
        }
    });

    module.exports = router;
    ```

7.  **`backend-nodejs/src/middleware/authMiddleware.js` (Middleware for protecting routes):**

    ```javascript
    const jwt = require('jsonwebtoken');
    require('dotenv').config();

    const authenticateToken = (req, res, next) => {
        const authHeader = req.headers['authorization'];
        const token = authHeader && authHeader.split(' ')[1]; // Bearer TOKEN

        if (token == null) {
            return res.status(401).json({ message: 'Authentication token required.' });
        }

        jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
            if (err) {
                return res.status(403).json({ message: 'Invalid or expired token.' });
            }
            req.user = user; // Attach user payload to the request
            next();
        });
    };

    const authorizeRole = (roles) => {
        return (req, res, next) => {
            if (!req.user || !roles.includes(req.user.role)) {
                return res.status(403).json({ message: 'Forbidden: You do not have the required permissions.' });
            }
            next();
        };
    };

    module.exports = {
        authenticateToken,
        authorizeRole,
    };
    ```

---

**Step 3: Python Excel Processor Setup**

Navigate to the `python-excel-processor` directory.

1.  **Create Python Virtual Environment (Recommended):**
    ```bash
    cd python-excel-processor
    python3 -m venv venv
    source venv/bin/activate # On Windows: .\venv\Scripts\activate
    ```
2.  **`python-excel-processor/requirements.txt`:**

    ```
    pandas
    openpyxl # Required for reading .xlsx files
    psycopg2-binary # For PostgreSQL connection (if Python directly inserts)
    ```
3.  **Install Python Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **`python-excel-processor/excel_processor.py` (Python Script):**

    This script will:
    *   Take the path to an Excel file as an argument.
    *   Read the Excel data using `pandas`.
    *   Perform basic validation.
    *   Insert questions and options into the PostgreSQL database.

    ```python
    import pandas as pd
    import argparse
    import json
    import os
    import psycopg2
    from psycopg2 import extras

    # --- Database Configuration (Ideally from environment variables or config file) ---
    DB_HOST = os.getenv('DB_HOST', 'localhost')
    DB_NAME = os.getenv('DB_NAME', 'mcq_quiz_db')
    DB_USER = os.getenv('DB_USER', 'your_user') # Replace with your PG user
    DB_PASSWORD = os.getenv('DB_PASSWORD', 'your_password') # Replace with your PG password

    def get_db_connection():
        conn = psycopg2.connect(
            host=DB_HOST,
            database=DB_NAME,
            user=DB_USER,
            password=DB_PASSWORD
        )
        return conn

    def process_excel_file(file_path):
        try:
            df = pd.read_excel(file_path)

            # Expected columns (adjust as per your Excel structure)
            expected_columns = [
                'Question Text', 'Option 1', 'Option 2', 'Option 3', 'Option 4', 'Correct Option No.', 'Points'
            ]
            if not all(col in df.columns for col in expected_columns):
                return {'status': 'error', 'message': f'Missing one or more expected columns. Expected: {expected_columns}'}

            questions_added = 0
            conn = get_db_connection()
            cur = conn.cursor()

            for index, row in df.iterrows():
                try:
                    question_text = str(row['Question Text']).strip()
                    points = int(row['Points'])
                    correct_option_num = int(row['Correct Option No.'])

                    if not question_text:
                        print(f"Skipping row {index + 2}: Question Text is empty.")
                        continue
                    if not (1 <= correct_option_num <= 4):
                        print(f"Skipping row {index + 2}: Invalid 'Correct Option No.' Must be between 1 and 4.")
                        continue

                    # Insert Question
                    cur.execute(
                        "INSERT INTO questions (question_text, points) VALUES (%s, %s) RETURNING id",
                        (question_text, points)
                    )
                    question_id = cur.fetchone()[0]

                    # Insert Options
                    options_data = []
                    for i in range(1, 5): # Assuming 4 options
                        option_text = str(row[f'Option {i}']).strip()
                        is_correct = (i == correct_option_num)
                        options_data.append((question_id, option_text, is_correct))

                    # Use executemany for efficiency
                    extras.execute_values(
                        cur,
                        "INSERT INTO options (question_id, option_text, is_correct) VALUES %s",
                        options_data,
                        page_size=100
                    )
                    questions_added += 1

                except ValueError as ve:
                    print(f"Data conversion error in row {index + 2}: {ve}")
                    conn.rollback() # Rollback current transaction to keep database consistent
                except KeyError as ke:
                    print(f"Missing column in row {index + 2}: {ke}")
                    conn.rollback()
                except Exception as e:
                    print(f"Error processing row {index + 2}: {e}")
                    conn.rollback()

            conn.commit()
            cur.close()
            conn.close()
            return {'status': 'success', 'message': f'{questions_added} questions processed and added to the database.'}

        except FileNotFoundError:
            return {'status': 'error', 'message': 'File not found.'}
        except Exception as e:
            return {'status': 'error', 'message': f'An unexpected error occurred: {e}'}

    if __name__ == '__main__':
        parser = argparse.ArgumentParser(description='Process an Excel file to upload MCQ questions.')
        parser.add_argument('file_path', type=str, help='The path to the Excel file.')
        args = parser.parse_args()

        result = process_excel_file(args.file_path)
        print(json.dumps(result)) # Output JSON for Node.js to read
    ```
    **Important:** Remember to replace `'your_user'` and `'your_password'` in `DB_USER` and `DB_PASSWORD` in `excel_processor.py` with your actual PostgreSQL credentials.

---

**Step 4: Integrating Python with Node.js (Excel Upload API)**

Now, we need to create an API endpoint in Node.js that:
1.  Receives the uploaded Excel file.
2.  Saves it temporarily.
3.  Calls the Python script, passing the file path.
4.  Returns the Python script's output to the client.

1.  **`backend-nodejs/src/routes/questionRoutes.js` (New file):**

    ```javascript
    const express = require('express');
    const router = express.Router();
    const multer = require('multer');
    const path = require('path');
    const { spawn } = require('child_process'); // To run Python script
    const fs = require('fs'); // For file system operations (deleting temp files)

    const { authenticateToken, authorizeRole } = require('../middleware/authMiddleware');

    // Configure Multer for file uploads
    const upload = multer({
        dest: 'temp_uploads/', // Temporary directory to store uploaded files
        fileFilter: (req, file, cb) => {
            const allowedMimes = [
                'application/vnd.ms-excel',
                'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
            ];
            if (allowedMimes.includes(file.mimetype)) {
                cb(null, true);
            } else {
                cb(new Error('Invalid file type. Only Excel files (.xls, .xlsx) are allowed.'), false);
            }
        },
        limits: { fileSize: 5 * 1024 * 1024 } // 5MB file size limit
    });

    // API to upload and process Excel questions
    router.post('/upload-excel',
        authenticateToken,
        authorizeRole(['admin']),
        upload.single('excelFile'), // 'excelFile' is the name of the input field in the form
        async (req, res) => {
            if (!req.file) {
                return res.status(400).json({ message: 'No Excel file uploaded.' });
            }

            const filePath = req.file.path; // Path to the temporarily stored file

            try {
                // Determine the path to the Python script
                const pythonScriptPath = path.join(__dirname, '../../../python-excel-processor/excel_processor.py');
                const pythonEnvPath = path.join(__dirname, '../../../python-excel-processor/venv/bin/python'); // Path to venv python executable

                const pythonProcess = spawn(pythonEnvPath, [pythonScriptPath, filePath]);

                let pythonOutput = '';
                let pythonError = '';

                pythonProcess.stdout.on('data', (data) => {
                    pythonOutput += data.toString();
                });

                pythonProcess.stderr.on('data', (data) => {
                    pythonError += data.toString();
                });

                pythonProcess.on('close', async (code) => {
                    // Clean up the temporary uploaded file
                    fs.unlink(filePath, (err) => {
                        if (err) console.error('Error deleting temp file:', err);
                    });

                    if (code !== 0) {
                        console.error(`Python script exited with code ${code}`);
                        console.error('Python Stderr:', pythonError);
                        // Try to parse error if Python provided it in JSON, otherwise general error
                        try {
                            const errorResult = JSON.parse(pythonOutput);
                            return res.status(500).json({ message: errorResult.message || 'Error processing Excel file (Python).' });
                        } catch (e) {
                            return res.status(500).json({ message: `Error processing Excel file: ${pythonError || 'Unknown Python error.'}` });
                        }
                    }

                    // Python script successful, parse its JSON output
                    try {
                        const result = JSON.parse(pythonOutput);
                        if (result.status === 'success') {
                            res.status(200).json(result);
                        } else {
                            res.status(400).json(result); // Python script returned an error status
                        }
                    } catch (parseErr) {
                        console.error('Error parsing Python output:', parseErr);
                        console.error('Raw Python output:', pythonOutput);
                        res.status(500).json({ message: 'Failed to parse Python script output.' });
                    }
                });

            } catch (error) {
                console.error('Server error during Excel upload:', error);
                // Ensure temp file is deleted even if spawn fails
                fs.unlink(filePath, (err) => {
                    if (err) console.error('Error deleting temp file on server error:', err);
                });
                res.status(500).json({ message: 'Server error processing file.' });
            }
        }
    );


    // Example route to get questions (for admin to view, for now)
    router.get('/', authenticateToken, authorizeRole(['admin']), async (req, res) => {
        try {
            const result = await db.query(`
                SELECT q.id, q.question_text, q.points,
                       json_agg(json_build_object('id', o.id, 'option_text', o.option_text, 'is_correct', o.is_correct)) as options
                FROM questions q
                JOIN options o ON q.id = o.question_id
                GROUP BY q.id
                ORDER BY q.id;
            `);
            res.json(result.rows);
        } catch (err) {
            console.error(err);
            res.status(500).json({ message: 'Error fetching questions.' });
        }
    });


    module.exports = router;
    ```
    **Note:** The `pythonEnvPath` might need adjustment depending on your exact OS and Python virtual environment setup. On macOS/Linux, it's usually `venv/bin/python`. On Windows, it might be `venv\Scripts\python.exe`.

---

**Step 5: Frontend (Admin Panel - Upload Page)**

Navigate to the `frontend/public` directory.

1.  **`frontend/public/index.html` (Basic Admin Login & Excel Upload Form):**

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>QuizMaster Admin</title>
        <link rel="stylesheet" href="css/style.css">
    </head>
    <body>
        <header>
            <h1>QuizMaster Admin Panel</h1>
            <nav id="adminNav" style="display: none;">
                <a href="#" id="logoutBtn">Logout</a>
            </nav>
        </header>

        <main>
            <section id="authSection">
                <h2>Admin Login</h2>
                <form id="loginForm">
                    <label for="email">Email:</label>
                    <input type="email" id="email" required>
                    <label for="password">Password:</label>
                    <input type="password" id="password" required>
                    <button type="submit">Login</button>
                </form>
                <p style="margin-top: 15px;">
                    Don't have an admin account? Register one (for first-time setup):
                    <button id="showRegisterFormBtn">Register Admin</button>
                </p>

                <form id="registerForm" style="display: none; margin-top: 20px;">
                    <h2>Register New Admin</h2>
                    <label for="regUsername">Username:</label>
                    <input type="text" id="regUsername" required>
                    <label for="regEmail">Email:</label>
                    <input type="email" id="regEmail" required>
                    <label for="regPassword">Password:</label>
                    <input type="password" id="regPassword" required>
                    <button type="submit">Register</button>
                    <button type="button" id="hideRegisterFormBtn">Back to Login</button>
                </form>

                <p id="authMessage" style="color: red;"></p>
            </section>

            <section id="adminDashboard" style="display: none;">
                <h2>Welcome, Admin!</h2>

                <div class="card">
                    <h3>Upload Questions from Excel</h3>
                    <form id="uploadExcelForm">
                        <label for="excelFile">Select Excel File:</label>
                        <input type="file" id="excelFile" name="excelFile" accept=".xls,.xlsx" required>
                        <button type="submit">Upload Questions</button>
                    </form>
                    <p id="uploadMessage"></p>
                    <p>
                        <small>
                            Excel file should have columns: 'Question Text', 'Option 1', 'Option 2', 'Option 3', 'Option 4', 'Correct Option No.', 'Points'.
                            'Correct Option No.' should be 1, 2, 3, or 4.
                        </small>
                    </p>
                </div>

                <div class="card" style="margin-top: 20px;">
                    <h3>Questions in Database</h3>
                    <button id="fetchQuestionsBtn">Refresh Questions</button>
                    <div id="questionsList">
                        <!-- Questions will be loaded here -->
                        <p>No questions loaded yet.</p>
                    </div>
                </div>
            </section>
        </main>

        <script src="js/script.js"></script>
    </body>
    </html>
    ```

2.  **`frontend/public/css/style.css` (Basic Styling):**

    ```css
    body {
        font-family: sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f4f4f4;
        color: #333;
    }

    header {
        background-color: #333;
        color: #fff;
        padding: 1rem 2rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    header h1 {
        margin: 0;
    }

    nav a {
        color: #fff;
        text-decoration: none;
        margin-left: 15px;
    }

    main {
        padding: 2rem;
        max-width: 900px;
        margin: 20px auto;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    section {
        margin-bottom: 30px;
    }

    form {
        display: flex;
        flex-direction: column;
        gap: 10px;
        max-width: 400px;
        margin-top: 15px;
    }

    form input[type="email"],
    form input[type="password"],
    form input[type="text"],
    form input[type="file"] {
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 1rem;
    }

    form button {
        background-color: #007bff;
        color: white;
        padding: 10px 15px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 1rem;
    }

    form button:hover {
        background-color: #0056b3;
    }

    .card {
        border: 1px solid #eee;
        padding: 20px;
        border-radius: 8px;
        background-color: #f9f9f9;
    }

    #questionsList {
        margin-top: 15px;
        border-top: 1px solid #eee;
        padding-top: 15px;
    }

    .question-item {
        background-color: #fff;
        border: 1px solid #ddd;
        padding: 10px 15px;
        margin-bottom: 10px;
        border-radius: 5px;
    }

    .question-item ul {
        list-style-type: none;
        padding: 0;
    }

    .question-item ul li {
        margin-bottom: 5px;
    }

    .question-item ul li.correct-option {
        font-weight: bold;
        color: green;
    }
    ```

3.  **`frontend/public/js/script.js` (Frontend Logic):**

    ```javascript
    document.addEventListener('DOMContentLoaded', () => {
        const API_BASE_URL = 'http://localhost:5000/api'; // Your Node.js backend URL

        const authSection = document.getElementById('authSection');
        const adminDashboard = document.getElementById('adminDashboard');
        const loginForm = document.getElementById('loginForm');
        const registerForm = document.getElementById('registerForm');
        const showRegisterFormBtn = document.getElementById('showRegisterFormBtn');
        const hideRegisterFormBtn = document.getElementById('hideRegisterFormBtn');
        const authMessage = document.getElementById('authMessage');
        const adminNav = document.getElementById('adminNav');
        const logoutBtn = document.getElementById('logoutBtn');

        const uploadExcelForm = document.getElementById('uploadExcelForm');
        const uploadMessage = document.getElementById('uploadMessage');
        const fetchQuestionsBtn = document.getElementById('fetchQuestionsBtn');
        const questionsList = document.getElementById('questionsList');

        let authToken = localStorage.getItem('authToken');
        let userRole = localStorage.getItem('userRole');

        function updateUI() {
            if (authToken && userRole === 'admin') {
                authSection.style.display = 'none';
                adminDashboard.style.display = 'block';
                adminNav.style.display = 'flex';
                fetchQuestions(); // Load questions when admin logs in
            } else {
                authSection.style.display = 'block';
                adminDashboard.style.display = 'none';
                adminNav.style.display = 'none';
            }
            authMessage.textContent = ''; // Clear auth message on UI update
            uploadMessage.textContent = ''; // Clear upload message
        }

        // --- Authentication ---
        loginForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;

            try {
                const response = await fetch(`${API_BASE_URL}/auth/login`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ email, password })
                });
                const data = await response.json();
                if (response.ok) {
                    authToken = data.token;
                    userRole = data.user.role;
                    localStorage.setItem('authToken', authToken);
                    localStorage.setItem('userRole', userRole);
                    updateUI();
                } else {
                    authMessage.textContent = data.message || 'Login failed.';
                }
            } catch (error) {
                console.error('Login error:', error);
                authMessage.textContent = 'Network error during login.';
            }
        });

        registerForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const username = document.getElementById('regUsername').value;
            const email = document.getElementById('regEmail').value;
            const password = document.getElementById('regPassword').value;

            try {
                const response = await fetch(`${API_BASE_URL}/auth/register-admin`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ username, email, password })
                });
                const data = await response.json();
                if (response.ok) {
                    authMessage.textContent = 'Admin registered successfully! Please log in.';
                    registerForm.style.display = 'none'; // Hide register form
                    loginForm.style.display = 'flex';    // Show login form
                    document.getElementById('email').value = email; // Pre-fill login email
                } else {
                    authMessage.textContent = data.message || 'Registration failed.';
                }
            } catch (error) {
                console.error('Register error:', error);
                authMessage.textContent = 'Network error during registration.';
            }
        });

        showRegisterFormBtn.addEventListener('click', () => {
            loginForm.style.display = 'none';
            registerForm.style.display = 'flex';
            authMessage.textContent = '';
        });

        hideRegisterFormBtn.addEventListener('click', () => {
            loginForm.style.display = 'flex';
            registerForm.style.display = 'none';
            authMessage.textContent = '';
        });

        logoutBtn.addEventListener('click', () => {
            authToken =
I recommend picking a technology stack you're comfortable with or one that has good documentation and community support for beginners. Python with Flask or Node.js with Express are often good starting points due to their relative simplicity.

Do you have any preferences for a programming language or framework, or would you like me to suggest one to dive deeper into specific code examples for a particular phase?
