# Company and College Review Platform

A comprehensive web-based platform that allows employees to share role-specific reviews about companies they have worked with, helping job seekers and users make informed career decisions.

## Features
### For Employees
- **Create Reviews**: Write detailed reviews about current and previous companies
- **Role-Specific Reviews**: Categorize reviews by job role (SDE, HR, Manager, Intern, etc.)
- **Multiple Companies**: Add reviews for previous companies with document verification
- **Edit/Delete**: Manage and update your written reviews
- **Dashboard**: View all your submitted reviews in one place

### For Job Seekers
- **Search Companies**: Find and read reviews about companies
- **Filter Reviews**: Filter by company, job role, and rating
- **View Company Profiles**: Get insights about companies through multiple reviews
- **Role-Based Insights**: See ratings and feedback for specific job roles within companies
- **Read-Only Access**: View reviews without the ability to edit or create (exclusive to employees)

## Technology Stack

- **Frontend**: HTML5, CSS3 (Responsive Design)
- **Backend**: Python with Flask
- **Database**: MongoDB
- **Authentication**: Flask Sessions with Password Hashing

## Installation

### Prerequisites
- Python 3.7 or higher
- MongoDB (local or cloud instance)
- pip (Python package manager)

### Setup Steps

1. **Clone or Extract the Project**
   ```bash
   cd "path/to/ABBS Main 1111"
   ```

2. **Create a Virtual Environment**
   ```bash
   python -m venv venv
   source venv/Scripts/activate  # On Windows
   # or
   source venv/bin/activate      # On MacOS/Linux
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure MongoDB**
   - Ensure MongoDB is running locally on `localhost:27017`
   - Or update the database connection string in `database.py`:
     ```python
     self.client = MongoClient('your_mongodb_uri')
     ```

5. **Run the Application**
   ```bash
   python app.py
   ```

6. **Access the Application**
   - Open your browser and navigate to: `http://127.0.0.1:5000`

## Project Structure

```
ABBS Main 1111/
├── app.py                 # Main Flask application
├── database.py            # MongoDB connection and operations
├── requirements.txt       # Python dependencies
├── templates/
│   ├── login.html         # Login page
│   ├── register.html      # Registration page
│   ├── employee_dashboard.html  # Employee dashboard
│   ├── user_dashboard.html      # Job seeker dashboard
│   ├── 404.html           # 404 error page
│   └── 500.html           # 500 error page
├── static/
│   ├── css/
│   │   ├── auth.css       # Authentication pages styling
│   │   └── style.css      # Main dashboard styling
│   ├── js/                # JavaScript files (for future expansion)
│   └── uploads/           # File uploads directory
└── README.md              # This file
```

## Usage Guide

### User Registration

1. **Employee Registration**
   - Click "Register" and select "Employee"
   - Fill in your details
   - **Important**: On signup, you must enter:
     - Current company name
     - Current job role
   - Only employees can create and edit reviews
   - You can only review your current company initially

2. **Job Seeker Registration**
   - Click "Register" and select "Job Seeker"
   - Fill in your details
   - Job seekers can view but not create/edit reviews

### Employee Actions

1. **Write a Review for Current Company**
   - Go to Employee Dashboard
   - Fill in the review form with:
     - Rating (1-5 stars) – interactive hover animation
     - Review title
     - Detailed feedback
     - Pros (optional)
     - Cons (optional)
   - Company and role are prefilled; company list is auto-created if missing
   - Click "Submit Review"

2. **Company Auto-suggest**
   - When entering a previous company name, suggestions appear
   - The dropdown is populated from existing companies in database

3. **Edit Existing Review**
   - On any review card click "Edit" to open a modal
   - Modify your rating, title, feedback, pros or cons and save

4. **Add Previous Company**
   - Use the tab to provide a prior employer and upload proof
   - The request is sent for **admin approval** before you can review it


### Admin Features

Users whose `user_type` is set to `admin` can:

- Visit `/admin` after login to see a list of pending previous-company submissions
- View uploaded proof documents and approve them
- Once approved, the employee can submit reviews for that company

(To create an admin, set `user_type` to `admin` in the MongoDB `users` collection.)


2. **Add Previous Company**
   - Go to Employee Dashboard
   - Click on "Previous Company" tab
   - Enter company name and job role
   - Upload proof document (pay slip, certificate, offer letter)
   - After verification, you can write reviews for that company

3. **Edit/Delete Reviews**
   - View your reviews in "My Reviews" section
   - Click "Edit" to modify any review
   - Click "Delete" to remove a review

### Job Seeker Actions

1. **Search Companies**
   - Use the search bar to find companies
   - Browse the list of companies

2. **Filter Reviews**
   - Filter by job role
   - Filter by minimum rating
   - Combine filters for specific insights

3. **View Company Details**
   - Click on any company card
   - View average rating
   - See ratings by specific job roles
   - Read individual reviews

4. **Read Full Reviews**
   - Click "Read full review" to see complete review details
   - View pros, cons, and detailed feedback

## API Endpoints

### Authentication
- `POST /register` - User registration
- `POST /login` - User login
- `GET /logout` - User logout

### Dashboard
- `GET /employee-dashboard` - Employee dashboard
- `GET /user-dashboard` - Job seeker dashboard

### Companies
- `GET /api/companies` - Get all companies
- `POST /api/add-company` - Add new company (Employee only)
- `GET /api/company/<id>` - Get company details
- `GET /api/company/<id>/reviews` - Get company reviews

### Reviews
- `POST /api/create-review` - Create review (Employee only)
- `PUT /api/update-review/<id>` - Update review (Employee only)
- `DELETE /api/delete-review/<id>` - Delete review (Employee only)
- `GET /api/search-reviews` - Search and filter reviews

### Previous Companies
- `POST /api/add-previous-company` - Add previous company with document (Employee only)

## Security Features

- **Password Hashing**: Passwords are hashed using Werkzeug security
- **Session Management**: Secure session-based authentication
- **Role-Based Access**: Different access levels for employees and job seekers
- **File Upload Validation**: Only specific file types allowed
- **CSRF Protection**: Session-based security tokens

## Responsive Design

The platform is fully responsive and works seamlessly on:
- Desktop computers (1920px and above)
- Tablets (768px to 1024px)
- Mobile phones (320px to 767px)

All elements adapt to screen size for optimal user experience.

## Database Schema

### Users Collection
```json
{
    "_id": ObjectId,
    "email": String,
    "password": String (hashed),
    "name": String,
    "user_type": String (employee/jobseeker),
    "company": String (employees only),
    "job_role": String (employees only),
    "previous_companies": Array,
    "created_at": DateTime,
    "updated_at": DateTime
}
```

### Companies Collection
```json
{
    "_id": ObjectId,
    "name": String,
    "created_at": DateTime
}
```

### Reviews Collection
```json
{
    "_id": ObjectId,
    "user_id": ObjectId,
    "company_id": ObjectId,
    "job_role": String,
    "rating": Integer (1-5),
    "title": String,
    "feedback": String,
    "pros": String,
    "cons": String,
    "is_previous": Boolean,
    "created_at": DateTime,
    "updated_at": DateTime
}
```

## Troubleshooting

### MongoDB Connection Error
- Ensure MongoDB is running
- Check the connection string in `database.py`
- Verify the database name is correct

### Port Already in Use
- Flask runs on port 5000 by default
- Change port in `app.py`: `app.run(port=5001)`

### File Upload Issues
- Check that `/static/uploads` directory exists
- Verify file size is under 16MB
- Ensure file type is allowed

## Future Enhancements

- Email verification for users
- Company admin dashboard
- Review moderation system
- Advanced analytics and statistics
- Mobile app version
- Salary data integration
- Interview experience sharing

## License

This project is for educational purposes.

## Support

For issues or questions, please contact the development team.

---

**Happy reviewing! Help job seekers make better career decisions.** 🚀
