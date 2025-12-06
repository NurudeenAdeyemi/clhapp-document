# Admission Module - Detailed Documentation

## Table of Contents
1. [Module Overview](#module-overview)
2. [User Roles & Permissions](#user-roles--permissions)
3. [Core Features](#core-features)
4. [User Workflows](#user-workflows)
5. [Course Management](#course-management)
6. [Cohort Management](#cohort-management)
7. [Application Process](#application-process)
8. [Data Models](#data-models)
9. [API Endpoints](#api-endpoints)
10. [UI/UX Specifications](#uiux-specifications)
11. [Business Rules](#business-rules)
12. [Technical Requirements](#technical-requirements)

---

## Module Overview

The Admission Module serves as the entry point for prospective students to explore courses, apply for programs, and complete enrollment. It supports multiple learning delivery modes including cohort-based, virtual, and self-paced learning.

### Key Objectives
- Provide a seamless course discovery experience
- Enable flexible application processes
- Support multiple course delivery modes
- Streamline admin cohort management
- Integrate user registration with application flow
- Automate enrollment confirmation and notifications

---

## User Roles & Permissions

### 1. Public User (Guest)
**Permissions:**
- View course catalog
- View course details
- View public cohort information
- Access signup/login page

**Restrictions:**
- Cannot apply for courses
- Cannot save favorites
- Cannot access application status

### 2. Registered User (Applicant)
**Permissions:**
- All public user permissions
- Apply for courses
- Select delivery mode
- Apply for specific cohorts
- Save favorite courses
- Track application status
- Upload required documents
- Update profile information

### 3. Admin
**Permissions:**
- All registered user permissions
- Create/edit/delete courses
- Create/edit/delete cohorts
- Manage course visibility
- Advertise cohorts
- Review applications
- Approve/reject applications
- Manage applicant data
- Generate admission reports
- Configure application form fields

### 4. Super Admin
**Permissions:**
- All admin permissions
- Manage admin users
- Configure system settings
- Access audit logs
- Manage email templates
- Configure payment settings

---

## Core Features

### Feature 1: Course Catalog
Display all available courses with filtering, sorting, and search capabilities.

**Capabilities:**
- List view with pagination
- Grid/card view option
- Search by course name, category, or keywords
- Filter by:
  - Category/Department
  - Delivery mode (cohort-based, virtual, self-paced)
  - Duration
  - Price range
  - Start date
  - Level (beginner, intermediate, advanced)
- Sort by:
  - Newest first
  - Alphabetical
  - Price (low to high, high to low)
  - Popularity
  - Start date

**Display Information:**
- Course thumbnail image
- Course title
- Short description (excerpt)
- Delivery mode badges
- Duration
- Price
- Next start date (for cohort-based)
- Available seats (for cohort-based)
- Rating/reviews (future enhancement)

### Feature 2: Course Details Page
Comprehensive information about a specific course.

**Sections:**
- Course overview and description
- Learning objectives/outcomes
- Curriculum/syllabus outline
- Instructor information and bio
- Prerequisites and requirements
- Course duration and time commitment
- Available delivery modes:
  - **Cohort-based**: Fixed schedule with live sessions
  - **Virtual**: Online synchronous learning
  - **Self-paced**: Asynchronous learning
- Pricing information
- FAQ section
- Reviews and testimonials
- Available cohorts (if applicable)
- "Apply Now" button (requires login)

### Feature 3: Delivery Mode Selection
Users can choose how they want to take the course.

**Mode Types:**

**A. Cohort-Based**
- Fixed start and end dates
- Live sessions with scheduled meeting times
- Peer interaction and group projects
- Limited seats per cohort
- Application deadline
- Display available cohorts with dates
- Show enrollment count/capacity

**B. Virtual**
- Online synchronous learning
- Live instructor-led sessions
- Flexible scheduling within timeframes
- Interactive virtual classroom
- Recorded session access

**C. Self-Paced**
- Fully asynchronous
- Immediate access upon enrollment
- Complete at your own speed
- Access to recorded content
- No fixed deadlines (or flexible deadlines)
- Lifetime or time-limited access

### Feature 4: Cohort Management (Admin)
Admins can create and manage cohorts for courses.

**Cohort Creation:**
- Select parent course
- Set cohort name/identifier (e.g., "Spring 2025 Batch")
- Define start and end dates
- Set enrollment capacity
- Set application deadline
- Define schedule (days/times for live sessions)
- Assign instructor(s)
- Set cohort-specific pricing (if different)
- Add cohort-specific description/notes

**Cohort Advertising:**
- Publish cohort to public catalog
- Feature cohort on homepage
- Set visibility status (draft, published, closed, archived)
- Add promotional banners/badges
- Send email campaigns to prospects
- Create early bird pricing
- Set registration reminders

**Cohort Monitoring:**
- View applications count
- Track enrollment status
- View applicant list
- Send communications to cohort applicants
- Duplicate cohort for future batches
- Archive completed cohorts

### Feature 5: Application Process
Multi-step application workflow with user registration.

**Application Flow:**

**Step 1: User Authentication Check**
- If not logged in → Redirect to signup/login
- If logged in → Proceed to application

**Step 2: Course/Cohort Selection**
- Confirm selected course
- If cohort-based: select specific cohort
- If multiple modes available: choose delivery mode
- Display pricing and key dates

**Step 3: Personal Information**
- Auto-populate from user profile
- Allow editing if needed
- Required fields:
  - Full name
  - Email address
  - Phone number
  - Date of birth
  - Gender
  - Address (street, city, state/province, country, postal code)
  - Emergency contact information

**Step 4: Educational Background**
- Highest qualification
- Institution name
- Year of completion
- Field of study
- Current occupation
- Years of experience
- LinkedIn profile (optional)

**Step 5: Course-Specific Questions**
- Why are you interested in this course?
- What do you hope to achieve?
- How did you hear about us?
- Previous experience in subject area
- Custom questions per course (configurable by admin)

**Step 6: Document Upload**
- Resume/CV (PDF, DOC, DOCX)
- Educational certificates
- ID proof
- Passport-size photograph
- Other course-specific documents
- File size limits and format validation

**Step 7: Payment Information** (if applicable)
- Application fee payment
- Full course fee payment
- Installment plan selection
- Scholarship/discount code application
- Payment method selection

**Step 8: Review & Submit**
- Summary of all entered information
- Terms and conditions acceptance
- Privacy policy acceptance
- Email/SMS notification preferences
- Final submission button

**Post-Submission:**
- Display confirmation message
- Send confirmation email with application ID
- Show application status page
- Provide payment receipt (if applicable)

### Feature 6: User Registration/Signup
Required before completing application.

**Registration Options:**
- Email and password
- Social login (Google, Facebook, LinkedIn)
- Single Sign-On (SSO) for institutions

**Registration Fields:**
- Email address (unique)
- Password (with strength requirements)
- First name
- Last name
- Phone number (with country code)
- Agree to terms and conditions

**Post-Registration:**
- Email verification required
- Welcome email sent
- Redirect to complete profile or continue application
- Auto-save application in progress

**Login Process:**
- Email and password
- "Remember me" option
- Forgot password flow
- Account lockout after failed attempts
- Two-factor authentication (optional)

---

## User Workflows

### Workflow 1: Public User Browsing Courses
```
1. User visits admission portal
2. Views course catalog (no login required)
3. Applies filters/search
4. Clicks on course card
5. Views detailed course information
6. Sees available cohorts and delivery modes
7. Clicks "Apply Now"
8. → Redirected to signup/login page
```

### Workflow 2: New User Application
```
1. User clicks "Apply Now" for a course
2. System detects no active session
3. Redirects to signup page
4. User completes registration form
5. Email verification sent
6. User verifies email
7. User is logged in automatically
8. Returns to application form with course pre-selected
9. Completes multi-step application
10. Submits application
11. Receives confirmation email
12. Can track application status in dashboard
```

### Workflow 3: Registered User Applying
```
1. User logs in
2. Browses course catalog
3. Selects course and cohort (if applicable)
4. Clicks "Apply Now"
5. System pre-fills known information
6. User completes remaining fields
7. Uploads documents
8. Reviews and submits
9. Makes payment (if required)
10. Application submitted
11. Status visible in user dashboard
```

### Workflow 4: Admin Creating Cohort
```
1. Admin logs into admin panel
2. Navigates to Course Management
3. Selects course to create cohort for
4. Clicks "Create New Cohort"
5. Fills cohort details form:
   - Name (e.g., "January 2025 Batch")
   - Start and end dates
   - Enrollment capacity
   - Application deadline
   - Session schedule
   - Instructor assignment
6. Sets visibility to "Published"
7. Optionally creates promotional campaign
8. Cohort appears in public catalog
9. Users can now apply for this cohort
```

### Workflow 5: Admin Advertising Cohort
```
1. Admin selects existing cohort
2. Clicks "Advertise Cohort"
3. Configures promotion:
   - Feature on homepage (yes/no)
   - Add promotional banner/badge
   - Set early bird deadline
   - Create discount code
   - Write marketing email
4. Selects target audience:
   - All registered users
   - Users who viewed this course
   - Previous applicants
   - Custom segment
5. Schedules or sends immediately
6. Cohort marked as "Featured"
7. Promotional content appears on catalog
```

### Workflow 6: Application Review (Admin)
```
1. Admin receives notification of new application
2. Logs into admin panel
3. Views application list with filters:
   - By course
   - By cohort
   - By status (pending, reviewing, approved, rejected)
   - By date range
4. Opens specific application
5. Reviews all submitted information and documents
6. Adds internal notes
7. Takes action:
   - Approve → Sends acceptance email
   - Reject → Sends rejection email with reason
   - Request more info → Sends email to applicant
8. Application status updated
9. Applicant notified via email/SMS
10. Approved applicants moved to enrollment list
```

---

## Course Management

### Course Entity Structure

**Basic Information:**
- Course ID (auto-generated)
- Course code (e.g., "CS101")
- Course title
- Short description (150 characters)
- Full description (rich text)
- Category/Department
- Tags/keywords
- Thumbnail image
- Banner image
- Video introduction URL

**Academic Details:**
- Course objectives/learning outcomes
- Prerequisites
- Target audience
- Difficulty level (beginner, intermediate, advanced)
- Curriculum/syllabus (modules and topics)
- Assessment methods
- Certification details

**Delivery Options:**
- Available modes (cohort-based, virtual, self-paced)
- Default mode
- Course duration (weeks, months)
- Estimated time commitment (hours/week)
- Language of instruction
- Accreditation information

**Pricing:**
- Base price
- Currency
- Installment options available
- Application fee (if any)
- Refund policy
- Early bird discount settings

**Enrollment Settings:**
- Enrollment capacity (overall)
- Minimum participants (for cohort-based)
- Application requirements
- Custom application questions
- Required documents list
- Auto-approval criteria (optional)

**Instructor Information:**
- Assigned instructor(s)
- Instructor bio and credentials
- Instructor photo

**Status & Visibility:**
- Draft/Published/Archived
- Featured on homepage
- Public/Private
- Created date
- Last updated date

### Admin Course Operations

**Create Course:**
- Multi-step form with all fields above
- Image upload with preview
- Rich text editor for descriptions
- Dynamic form fields for custom questions
- Preview before publishing

**Edit Course:**
- Update any field
- Track change history
- Preview changes
- Publish updates immediately or schedule

**Duplicate Course:**
- Copy all settings
- Rename and modify as needed
- Useful for similar courses

**Delete/Archive Course:**
- Soft delete (archive)
- Check for active cohorts/applications
- Warning before deletion
- Cannot delete if active enrollments exist

---

## Cohort Management

### Cohort Entity Structure

**Basic Information:**
- Cohort ID (auto-generated)
- Parent Course ID (foreign key)
- Cohort name/identifier
- Cohort code (e.g., "CS101-S25")
- Description (cohort-specific notes)

**Schedule:**
- Start date
- End date
- Application open date
- Application deadline
- Session schedule:
  - Days of week
  - Time slots
  - Duration per session
  - Time zone
  - Total sessions count
  - Session format (live, hybrid)

**Enrollment:**
- Maximum capacity
- Minimum participants
- Current enrollment count
- Waitlist capacity
- Waitlist current count

**Pricing:**
- Inherit from course or custom
- Special pricing/discounts
- Early bird pricing (amount and deadline)
- Scholarship availability

**Instructor:**
- Assigned instructor(s)
- Teaching assistants (if any)

**Status & Visibility:**
- Status (draft, published, application_open, application_closed, in_progress, completed, cancelled, archived)
- Featured (yes/no)
- Visibility (public, private, invitation_only)

**Promotional:**
- Banner text/badge (e.g., "Limited Seats", "Early Bird Open")
- Featured on homepage
- Email campaign sent (yes/no, date)
- Notification sent to followers

**Metadata:**
- Created by (admin user ID)
- Created date
- Last updated date
- Last updated by

### Cohort Lifecycle States

1. **Draft** - Created but not visible to public
2. **Published** - Visible but applications not yet open
3. **Application Open** - Accepting applications
4. **Application Closed** - Deadline passed, no new applications
5. **In Progress** - Cohort has started
6. **Completed** - Cohort has ended
7. **Cancelled** - Cohort cancelled before start
8. **Archived** - Removed from active listings

### Cohort Operations

**Create Cohort:**
- Select parent course (required)
- Fill all cohort-specific details
- Set schedule and capacity
- Assign instructor
- Set status and visibility
- Save as draft or publish immediately

**Publish/Advertise Cohort:**
- Change status to "Published"
- Make visible in public catalog
- Send notification email to:
  - Users who expressed interest
  - Users who viewed the course
  - Newsletter subscribers
- Add to featured cohorts section
- Share on social media (optional)

**Edit Cohort:**
- Update dates (with restrictions if enrollments exist)
- Modify capacity
- Change pricing
- Update schedule
- Cannot change parent course

**Close Applications:**
- Manually close before deadline
- Auto-close on deadline date
- No new applications accepted
- Existing applications still processed

**Cancel Cohort:**
- Notify all applicants
- Process refunds if payments made
- Archive cohort record

**Duplicate Cohort:**
- Create new cohort from existing
- Copy all settings
- Update dates for next batch
- Useful for recurring courses

**Archive Cohort:**
- Move to archive after completion
- Maintain records for reporting
- Not visible in active listings

---

## Application Process

### Application Entity Structure

**Application Metadata:**
- Application ID (unique)
- User ID (foreign key)
- Course ID (foreign key)
- Cohort ID (foreign key, nullable for non-cohort courses)
- Delivery mode selected
- Application date/timestamp
- Status (draft, submitted, under_review, approved, rejected, waitlisted, withdrawn)
- Reviewed by (admin user ID, if reviewed)
- Review date
- Review notes (internal, admin only)

**Personal Information:**
- First name
- Middle name
- Last name
- Email
- Phone (with country code)
- Date of birth
- Gender
- Nationality
- Address (street, city, state, country, postal code)
- Emergency contact name
- Emergency contact phone

**Educational Background:**
- Highest qualification
- Institution name
- Year of completion
- Field of study
- GPA/Grade (optional)
- Current occupation
- Company name
- Years of experience
- Industry
- LinkedIn URL

**Course-Specific Responses:**
- JSON field storing:
  - Question ID
  - Question text
  - Answer/Response
  - (Dynamic based on course configuration)

**Documents:**
- Array of uploaded documents:
  - Document type (resume, certificate, ID, etc.)
  - File name
  - File path/URL
  - Upload date
  - File size
  - MIME type

**Payment Information:**
- Application fee paid (boolean)
- Application fee amount
- Payment transaction ID
- Payment date
- Payment method
- Full course fee paid (boolean)
- Course fee amount
- Course fee transaction ID
- Payment plan selected
- Discount code applied
- Final amount

**Preferences:**
- Email notifications (yes/no)
- SMS notifications (yes/no)
- Marketing communications (yes/no)
- Preferred contact method

**Consents:**
- Terms accepted (boolean, required)
- Privacy policy accepted (boolean, required)
- Data processing consent (boolean, required)
- Timestamp of acceptance

### Application Status Flow

```
Draft (saved but not submitted)
    ↓
Submitted (application complete and submitted)
    ↓
Under Review (admin is reviewing)
    ↓ ↓ ↓
    |  |  Rejected (declined with reason)
    |  |
    |  Waitlisted (no seats available, added to waitlist)
    |
Approved (accepted into program)
    ↓
Enrolled (officially enrolled after payment/confirmation)
```

**Status Actions:**
- **Draft**: User can edit and save progress
- **Submitted**: User cannot edit, admin notified
- **Under Review**: Admin opened application
- **Approved**: Acceptance email sent, enrollment instructions provided
- **Rejected**: Rejection email with optional feedback
- **Waitlisted**: Waitlist notification, may convert to approved if seat opens
- **Withdrawn**: User or admin cancelled application
- **Enrolled**: Moved to student management system

---

## Data Models

### 1. User Model
```javascript
{
  id: UUID,
  email: String (unique),
  password: String (hashed),
  first_name: String,
  last_name: String,
  phone: String,
  phone_country_code: String,
  profile_image: String (URL),
  role: Enum ['public', 'applicant', 'student', 'admin', 'super_admin'],
  email_verified: Boolean,
  email_verification_token: String,
  is_active: Boolean,
  last_login: DateTime,
  created_at: DateTime,
  updated_at: DateTime,
  profile: {
    date_of_birth: Date,
    gender: String,
    nationality: String,
    address: Object,
    emergency_contact: Object
  }
}
```

### 2. Course Model
```javascript
{
  id: UUID,
  course_code: String (unique),
  title: String,
  slug: String (unique, URL-friendly),
  short_description: String (150 chars),
  full_description: Text (rich text),
  category: String,
  tags: Array[String],
  thumbnail_image: String (URL),
  banner_image: String (URL),
  video_url: String,

  // Academic
  objectives: Array[String],
  prerequisites: Array[String],
  target_audience: String,
  difficulty_level: Enum ['beginner', 'intermediate', 'advanced'],
  curriculum: Array[Object] // modules with topics
  assessment_methods: Array[String],
  certification: Object,

  // Delivery
  available_modes: Array[Enum] ['cohort', 'virtual', 'self_paced'],
  default_mode: Enum ['cohort', 'virtual', 'self_paced'],
  duration_value: Number,
  duration_unit: Enum ['weeks', 'months'],
  weekly_hours: Number,
  language: String,

  // Pricing
  price: Number,
  currency: String,
  installment_available: Boolean,
  application_fee: Number,

  // Enrollment
  capacity: Number,
  minimum_participants: Number,
  application_questions: Array[Object],
  required_documents: Array[String],
  auto_approval: Boolean,

  // Instructor
  instructors: Array[UUID], // references to User model

  // Status
  status: Enum ['draft', 'published', 'archived'],
  is_featured: Boolean,
  is_public: Boolean,

  created_at: DateTime,
  updated_at: DateTime,
  created_by: UUID
}
```

### 3. Cohort Model
```javascript
{
  id: UUID,
  course_id: UUID (foreign key),
  cohort_name: String,
  cohort_code: String (unique),
  description: Text,

  // Schedule
  start_date: Date,
  end_date: Date,
  application_open_date: Date,
  application_deadline: Date,
  schedule: {
    days_of_week: Array[String], // ['Monday', 'Wednesday']
    time_slots: Array[Object], // [{start: '10:00', end: '12:00'}]
    timezone: String,
    total_sessions: Number,
    session_duration: Number (minutes)
  },

  // Enrollment
  max_capacity: Number,
  min_participants: Number,
  current_enrollment: Number (computed),
  waitlist_capacity: Number,
  current_waitlist: Number (computed),

  // Pricing
  use_course_pricing: Boolean,
  custom_price: Number,
  early_bird_price: Number,
  early_bird_deadline: Date,

  // Instructor
  instructor_ids: Array[UUID],
  teaching_assistant_ids: Array[UUID],

  // Status
  status: Enum ['draft', 'published', 'application_open', 'application_closed', 'in_progress', 'completed', 'cancelled', 'archived'],
  is_featured: Boolean,
  visibility: Enum ['public', 'private', 'invitation_only'],

  // Promotional
  banner_text: String,
  featured_on_homepage: Boolean,
  campaign_sent: Boolean,
  campaign_sent_date: DateTime,

  created_at: DateTime,
  updated_at: DateTime,
  created_by: UUID
}
```

### 4. Application Model
```javascript
{
  id: UUID,
  application_number: String (unique, human-readable),
  user_id: UUID (foreign key),
  course_id: UUID (foreign key),
  cohort_id: UUID (foreign key, nullable),
  delivery_mode: Enum ['cohort', 'virtual', 'self_paced'],

  // Status
  status: Enum ['draft', 'submitted', 'under_review', 'approved', 'rejected', 'waitlisted', 'withdrawn', 'enrolled'],
  submitted_at: DateTime,
  reviewed_by: UUID (admin),
  reviewed_at: DateTime,
  review_notes: Text,
  rejection_reason: Text,

  // Personal Info
  personal_info: {
    first_name: String,
    middle_name: String,
    last_name: String,
    email: String,
    phone: String,
    date_of_birth: Date,
    gender: String,
    nationality: String,
    address: Object,
    emergency_contact: Object
  },

  // Educational Background
  education: {
    highest_qualification: String,
    institution: String,
    year_of_completion: Number,
    field_of_study: String,
    gpa: String,
    current_occupation: String,
    company: String,
    years_of_experience: Number,
    industry: String,
    linkedin_url: String
  },

  // Course-specific responses
  custom_responses: Array[Object], // [{question_id, question, answer}]

  // Documents
  documents: Array[Object], // [{type, filename, url, uploaded_at}]

  // Payment
  payment: {
    application_fee_paid: Boolean,
    application_fee_amount: Number,
    application_fee_transaction_id: String,
    application_fee_date: DateTime,
    payment_method: String,
    course_fee_paid: Boolean,
    course_fee_amount: Number,
    course_fee_transaction_id: String,
    payment_plan: String,
    discount_code: String,
    discount_amount: Number,
    final_amount: Number
  },

  // Preferences & Consents
  preferences: {
    email_notifications: Boolean,
    sms_notifications: Boolean,
    marketing_opt_in: Boolean,
    preferred_contact_method: String
  },
  consents: {
    terms_accepted: Boolean,
    terms_accepted_at: DateTime,
    privacy_accepted: Boolean,
    privacy_accepted_at: DateTime,
    data_processing_consent: Boolean
  },

  created_at: DateTime,
  updated_at: DateTime
}
```

### 5. Document Model (separate table for tracking uploads)
```javascript
{
  id: UUID,
  application_id: UUID (foreign key),
  user_id: UUID (foreign key),
  document_type: Enum ['resume', 'certificate', 'id_proof', 'photo', 'transcript', 'other'],
  original_filename: String,
  stored_filename: String,
  file_path: String,
  file_size: Number (bytes),
  mime_type: String,
  uploaded_at: DateTime,
  verified: Boolean,
  verified_by: UUID (admin),
  verified_at: DateTime
}
```

---

## API Endpoints

### Public Endpoints (No Authentication Required)

#### 1. Get Course Catalog
```
GET /api/courses
Query Parameters:
  - page: Number (default: 1)
  - limit: Number (default: 20)
  - search: String
  - category: String
  - delivery_mode: String
  - level: String
  - price_min: Number
  - price_max: Number
  - sort: String (newest, price_asc, price_desc, name)

Response: {
  data: Array[Course],
  pagination: {
    current_page: Number,
    total_pages: Number,
    total_items: Number,
    per_page: Number
  }
}
```

#### 2. Get Course Details
```
GET /api/courses/:courseId
or
GET /api/courses/slug/:slug

Response: {
  course: Course Object,
  available_cohorts: Array[Cohort],
  instructor_details: Array[User]
}
```

#### 3. Get Course Cohorts
```
GET /api/courses/:courseId/cohorts
Query Parameters:
  - status: String (application_open, upcoming)
  - featured: Boolean

Response: {
  data: Array[Cohort]
}
```

#### 4. Get Featured Courses
```
GET /api/courses/featured

Response: {
  data: Array[Course]
}
```

### Authentication Endpoints

#### 5. User Registration
```
POST /api/auth/register
Body: {
  email: String,
  password: String,
  first_name: String,
  last_name: String,
  phone: String,
  terms_accepted: Boolean
}

Response: {
  user: User Object (without password),
  token: String,
  message: "Registration successful. Please verify your email."
}
```

#### 6. User Login
```
POST /api/auth/login
Body: {
  email: String,
  password: String,
  remember_me: Boolean
}

Response: {
  user: User Object,
  token: String,
  expires_at: DateTime
}
```

#### 7. Verify Email
```
GET /api/auth/verify-email/:token

Response: {
  message: "Email verified successfully"
}
```

#### 8. Forgot Password
```
POST /api/auth/forgot-password
Body: {
  email: String
}

Response: {
  message: "Password reset link sent to your email"
}
```

#### 9. Reset Password
```
POST /api/auth/reset-password
Body: {
  token: String,
  new_password: String
}

Response: {
  message: "Password reset successful"
}
```

### Protected Endpoints (Authentication Required)

#### 10. Create Application (Draft)
```
POST /api/applications
Headers: Authorization: Bearer {token}
Body: {
  course_id: UUID,
  cohort_id: UUID (optional),
  delivery_mode: String
}

Response: {
  application: Application Object,
  message: "Application draft created"
}
```

#### 11. Update Application
```
PATCH /api/applications/:applicationId
Headers: Authorization: Bearer {token}
Body: {
  // Any application fields to update
  personal_info: Object,
  education: Object,
  custom_responses: Array,
  etc.
}

Response: {
  application: Application Object,
  message: "Application updated"
}
```

#### 12. Submit Application
```
POST /api/applications/:applicationId/submit
Headers: Authorization: Bearer {token}

Response: {
  application: Application Object,
  message: "Application submitted successfully",
  application_number: String
}
```

#### 13. Upload Document
```
POST /api/applications/:applicationId/documents
Headers: Authorization: Bearer {token}
Body: FormData {
  document_type: String,
  file: File
}

Response: {
  document: Document Object,
  message: "Document uploaded successfully"
}
```

#### 14. Get My Applications
```
GET /api/applications/my-applications
Headers: Authorization: Bearer {token}
Query Parameters:
  - status: String
  - page: Number

Response: {
  data: Array[Application],
  pagination: Object
}
```

#### 15. Get Application Details
```
GET /api/applications/:applicationId
Headers: Authorization: Bearer {token}

Response: {
  application: Application Object,
  course: Course Object,
  cohort: Cohort Object (if applicable)
}
```

#### 16. Withdraw Application
```
POST /api/applications/:applicationId/withdraw
Headers: Authorization: Bearer {token}

Response: {
  message: "Application withdrawn successfully"
}
```

### Admin Endpoints (Admin/Super Admin Only)

#### 17. Create Course
```
POST /api/admin/courses
Headers: Authorization: Bearer {admin_token}
Body: Course Object

Response: {
  course: Course Object,
  message: "Course created successfully"
}
```

#### 18. Update Course
```
PATCH /api/admin/courses/:courseId
Headers: Authorization: Bearer {admin_token}
Body: Partial Course Object

Response: {
  course: Course Object,
  message: "Course updated successfully"
}
```

#### 19. Delete Course
```
DELETE /api/admin/courses/:courseId
Headers: Authorization: Bearer {admin_token}

Response: {
  message: "Course deleted/archived successfully"
}
```

#### 20. Create Cohort
```
POST /api/admin/cohorts
Headers: Authorization: Bearer {admin_token}
Body: Cohort Object

Response: {
  cohort: Cohort Object,
  message: "Cohort created successfully"
}
```

#### 21. Update Cohort
```
PATCH /api/admin/cohorts/:cohortId
Headers: Authorization: Bearer {admin_token}
Body: Partial Cohort Object

Response: {
  cohort: Cohort Object,
  message: "Cohort updated successfully"
}
```

#### 22. Publish/Advertise Cohort
```
POST /api/admin/cohorts/:cohortId/publish
Headers: Authorization: Bearer {admin_token}
Body: {
  send_notifications: Boolean,
  feature_on_homepage: Boolean,
  banner_text: String
}

Response: {
  cohort: Cohort Object,
  message: "Cohort published and advertised"
}
```

#### 23. Get All Applications (Admin View)
```
GET /api/admin/applications
Headers: Authorization: Bearer {admin_token}
Query Parameters:
  - status: String
  - course_id: UUID
  - cohort_id: UUID
  - search: String
  - date_from: Date
  - date_to: Date
  - page: Number

Response: {
  data: Array[Application],
  pagination: Object,
  statistics: {
    total: Number,
    pending: Number,
    approved: Number,
    rejected: Number
  }
}
```

#### 24. Review Application
```
POST /api/admin/applications/:applicationId/review
Headers: Authorization: Bearer {admin_token}
Body: {
  status: Enum ['approved', 'rejected', 'waitlisted'],
  review_notes: String,
  rejection_reason: String (if rejected),
  send_notification: Boolean
}

Response: {
  application: Application Object,
  message: "Application reviewed successfully"
}
```

#### 25. Get Application Statistics
```
GET /api/admin/applications/statistics
Headers: Authorization: Bearer {admin_token}
Query Parameters:
  - course_id: UUID (optional)
  - cohort_id: UUID (optional)
  - date_from: Date
  - date_to: Date

Response: {
  total_applications: Number,
  by_status: Object,
  by_course: Array[Object],
  by_cohort: Array[Object],
  conversion_rate: Number,
  average_processing_time: Number (days)
}
```

---

## UI/UX Specifications

### 1. Course Catalog Page

**Layout:**
- Header with logo and navigation (Home, Courses, About, Contact)
- Search bar prominent at top
- Sidebar with filters (collapsible on mobile)
- Main content area with course cards
- Grid layout (3-4 columns on desktop, responsive)
- Pagination or infinite scroll

**Filter Sidebar:**
- Category checkboxes
- Delivery mode checkboxes
- Price range slider
- Duration filter
- Level radio buttons
- Clear all filters button

**Course Card Design:**
- Large thumbnail image (16:9 ratio)
- Course title (truncate at 2 lines)
- Short description (truncate at 3 lines)
- Delivery mode badges (colored pills)
- Price displayed prominently
- Duration and level icons
- "View Details" button
- Hover effect: slight elevation, show "Apply Now" option

**Mobile Considerations:**
- Filters in bottom drawer/modal
- Single column layout
- Sticky search bar
- Swipeable course cards

### 2. Course Details Page

**Layout Sections:**

**Hero Section:**
- Full-width banner image
- Overlay with course title
- Breadcrumb navigation
- Call-to-action: "Apply Now" button (sticky on scroll)
- Price tag
- Share buttons

**Tabs/Sections:**
1. Overview
   - Video introduction (if available)
   - Full description
   - Key highlights (bullet points)

2. Curriculum
   - Expandable modules
   - Topics under each module
   - Estimated time per module

3. Delivery Options
   - Cards for each available mode
   - Comparison table
   - "Select Mode" buttons

4. Instructor
   - Photo and bio
   - Credentials
   - Social links

5. Available Cohorts (if cohort-based)
   - Table/cards with dates and availability
   - Apply to specific cohort

6. Prerequisites & Requirements
   - List of prerequisites
   - Technical requirements

7. FAQ
   - Accordion of common questions

8. Reviews (future)
   - Star ratings
   - Student testimonials

**Sidebar (Desktop):**
- Course quick info card
- Price and payment options
- Next start date
- Duration
- Available seats
- "Apply Now" button
- "Save to favorites" button
- Contact admissions link

### 3. Application Form

**Design Principles:**
- Multi-step wizard with progress indicator
- Step numbers and titles visible
- "Save as Draft" option on every step
- Previous/Next navigation
- Validation on each field
- Helpful tooltips and placeholders
- Auto-save functionality (every 30 seconds)

**Progress Indicator:**
```
[1] Authentication → [2] Course Selection → [3] Personal Info →
[4] Education → [5] Questions → [6] Documents → [7] Payment → [8] Review
```

**Step Templates:**

**Step 1: Authentication Check**
- If not logged in:
  - "You need to sign up or log in to apply"
  - Tabs for "Sign Up" and "Login"
  - Social login buttons
  - Traditional form fields
  - "Continue" button

**Step 2: Course Selection Confirmation**
- Course card display
- Selected cohort (if applicable)
- Delivery mode selection (radio buttons with descriptions)
- Key dates displayed
- Pricing information
- "Confirm and Continue" button

**Step 3: Personal Information**
- Form fields in logical groups
- Country selector with flags
- Phone with country code dropdown
- Date picker for DOB
- Address auto-complete
- Real-time validation
- "Next" button

**Step 4: Educational Background**
- Dropdown for qualification levels
- Institution name (text input with suggestions)
- Year selectors
- Occupation and experience fields
- LinkedIn profile validation
- "Next" button

**Step 5: Course-Specific Questions**
- Dynamic questions based on course
- Text areas for essay questions
- Character count for limited responses
- Rich text editor if needed
- "Next" button

**Step 6: Document Upload**
- Drag-and-drop upload zones
- File type and size indicators
- Upload progress bars
- Thumbnail previews
- Delete/replace options
- "Skip for now" option (if not required)
- "Next" button

**Step 7: Payment Information**
- Payment method selection (radio cards)
- Secure payment form
- Apply discount code input
- Order summary sidebar
- Total amount display
- "Proceed to Payment" button
- Or "Pay Later" option if allowed

**Step 8: Review & Submit**
- Accordion sections for each step
- Edit links to go back to specific steps
- Summary of all information
- Terms and conditions checkbox
- Privacy policy checkbox
- Email consent checkbox
- Final "Submit Application" button (prominent, green)
- Confirmation modal before submission

**Post-Submission:**
- Success animation
- Application number display (large)
- Summary of next steps
- Download/email confirmation option
- "Track Application Status" button
- "Apply for Another Course" link

### 4. User Dashboard

**Sections:**
- Welcome message with user name
- Quick stats: Applications (pending, approved, etc.)
- My Applications table/cards
- Saved courses
- Profile completeness indicator
- Notifications panel

**My Applications View:**
- Filterable by status
- Sortable by date
- Each row/card shows:
  - Application number
  - Course name and thumbnail
  - Cohort (if applicable)
  - Submission date
  - Status badge (color-coded)
  - Action buttons (View, Withdraw)

### 5. Admin Panel

**Dashboard:**
- Statistics cards (total applications, pending review, approved, rejected)
- Charts (applications over time, by course, by status)
- Recent applications table
- Quick actions

**Course Management:**
- List view with search and filters
- Actions: Add New, Edit, Delete, Duplicate
- Status indicators
- Enrollment counts

**Cohort Management:**
- List view grouped by course
- Calendar view option
- Actions: Add New, Edit, Publish, Cancel
- Enrollment tracking
- Send notifications button

**Application Management:**
- Advanced filtering
- Bulk actions
- Application review interface:
  - Full application view
  - Document viewer
  - Internal notes section
  - Approve/Reject/Waitlist buttons
  - Email template selection
  - Audit trail

**Reports:**
- Exportable reports (CSV, PDF)
- Custom date ranges
- Filter by course/cohort
- Conversion funnel visualization

### 6. Responsive Design

**Breakpoints:**
- Mobile: 320px - 767px
- Tablet: 768px - 1023px
- Desktop: 1024px+

**Mobile-Specific Features:**
- Bottom navigation bar
- Hamburger menu
- Swipeable content
- Touch-friendly buttons (min 44px)
- Simplified filters
- Collapsible sections

### 7. Accessibility

**Requirements:**
- WCAG 2.1 Level AA compliance
- Keyboard navigation support
- Screen reader friendly
- Alt text for all images
- ARIA labels and roles
- Sufficient color contrast (4.5:1)
- Focus indicators visible
- Error messages clearly announced

---

## Business Rules

### 1. Course Rules

- A course must have at least one delivery mode
- Course price must be non-negative
- Course cannot be deleted if it has active cohorts or applications
- Draft courses are not visible to public users
- Featured courses appear on homepage (max 6)
- Course slug must be unique and URL-safe

### 2. Cohort Rules

- Cohort must be linked to an existing published course
- Start date must be before end date
- Application deadline must be before start date
- Application open date must be before application deadline
- Max capacity must be greater than min participants
- Cannot modify capacity below current enrollment count
- Cannot delete cohort if applications exist
- Cohort status automatically changes to "application_closed" on deadline
- Cohort status automatically changes to "in_progress" on start date
- Cannot enroll more students than max capacity (unless waitlist)
- Early bird deadline must be before application deadline
- Cannot modify dates if cohort is "in_progress" or "completed"

### 3. Application Rules

- User must be registered and logged in to apply
- User cannot apply twice for the same course+cohort combination
- Application status "draft" can be edited by user
- Application status "submitted" cannot be edited by user
- Application must be complete before submission (all required fields)
- Application can only be reviewed by admin
- Approved applications automatically enroll if payment is confirmed
- Rejected applications cannot be resubmitted (must apply again)
- Withdrawn applications cannot be reinstated
- Application deadline is enforced (no submissions after deadline)
- If cohort is full, new applications go to waitlist automatically
- Waitlisted applications convert to approved if seat becomes available

### 4. Document Upload Rules

- Only accepted file types: PDF, DOC, DOCX, JPG, PNG
- Maximum file size: 5MB per file
- Maximum total upload size per application: 20MB
- Documents are virus-scanned before storage
- Document filenames are sanitized
- Uploaded documents cannot be deleted after application submission (only by admin)

### 5. Payment Rules

- Application fee (if any) must be paid before submission
- Course fee must be paid before enrollment
- Refund policy: 100% refund if withdrawn before deadline, 50% if within X days, no refund after course starts
- Discount codes have expiration dates
- Discount codes have usage limits (total uses, per user)
- Cannot combine multiple discount codes
- Early bird pricing automatically applies if before deadline
- Payment confirmation triggers automated enrollment email

### 6. User Registration Rules

- Email must be unique in system
- Password must meet strength requirements:
  - Minimum 8 characters
  - At least one uppercase letter
  - At least one lowercase letter
  - At least one number
  - At least one special character
- Email verification required before full access
- Account auto-locks after 5 failed login attempts (30-minute cooldown)
- Password reset links expire after 1 hour

### 7. Notification Rules

- Application submission triggers confirmation email to user
- Application status change triggers email to user
- Admin receives email on new application submission
- Cohort advertisement sends email to opted-in users only
- Reminders sent X days before application deadline
- Payment confirmation triggers receipt email
- Enrollment confirmation triggers welcome email with course access

### 8. Access Control Rules

- Public users can view published courses and cohorts only
- Registered users can view own applications only
- Admins can view all applications for their assigned courses
- Super admins can view all data
- Applicants cannot see other applicants' information
- Admin review notes are never visible to applicants
- Document access restricted to owner and admins

---

## Technical Requirements

### 1. Technology Stack Recommendations

**Backend:**
- Framework: Node.js (Express) / Python (Django/Flask) / Ruby (Rails)
- Database: PostgreSQL (relational data) + Redis (caching, sessions)
- File Storage: AWS S3 / Google Cloud Storage / Azure Blob Storage
- Search: Elasticsearch or Algolia (for course catalog)
- Queue: Bull/Bee-Queue (Node.js) or Celery (Python) for async tasks
- Email Service: SendGrid / Amazon SES / Mailgun
- SMS Service: Twilio / Vonage
- Payment Gateway: Stripe / PayPal / Razorpay

**Frontend:**
- Framework: React / Vue.js / Next.js
- State Management: Redux / Zustand / Pinia
- UI Library: Material-UI / Ant Design / Tailwind CSS
- Form Management: Formik / React Hook Form
- File Upload: React Dropzone / Uppy
- Rich Text Editor: TinyMCE / Quill / Slate

**Authentication:**
- JWT tokens with refresh token rotation
- OAuth 2.0 for social login
- bcrypt for password hashing (cost factor 12)

**DevOps:**
- Containerization: Docker
- Orchestration: Kubernetes (for scale)
- CI/CD: GitHub Actions / GitLab CI / Jenkins
- Monitoring: Sentry (errors) + DataDog/New Relic (performance)
- Logging: ELK Stack (Elasticsearch, Logstash, Kibana)

### 2. Database Design Considerations

**Indexes:**
- Course: slug, status, is_featured, category
- Cohort: course_id, status, start_date, application_deadline
- Application: user_id, course_id, cohort_id, status, submitted_at
- User: email, role

**Relationships:**
- User 1-to-many Application
- Course 1-to-many Cohort
- Course 1-to-many Application
- Cohort 1-to-many Application
- Application 1-to-many Document
- Course many-to-many Instructor (User)

**Performance:**
- Use database connection pooling
- Implement query result caching (Redis)
- Use pagination for all list endpoints
- Implement database read replicas for heavy read operations
- Use database indexes strategically

### 3. Security Requirements

**Data Protection:**
- All sensitive data encrypted at rest (AES-256)
- All data in transit uses TLS 1.3
- PII data is anonymized in logs
- Regular security audits
- GDPR compliance for EU users
- Data retention policies enforced
- Right to be forgotten implemented

**Input Validation:**
- Server-side validation for all inputs
- XSS prevention (sanitize HTML inputs)
- SQL injection prevention (parameterized queries/ORMs)
- CSRF protection (tokens)
- Rate limiting on all public endpoints
- File upload validation (type, size, content)

**Authentication & Authorization:**
- JWT tokens expire after 1 hour (access) / 7 days (refresh)
- Role-based access control (RBAC) enforced
- API endpoints protected with middleware
- Admin actions require re-authentication for sensitive ops
- Audit logs for all admin actions

### 4. Performance Requirements

**Response Times:**
- API endpoints: < 200ms (p95)
- Page load time: < 2 seconds (p95)
- Search results: < 500ms
- File uploads: Progressive with real-time feedback

**Scalability:**
- Handle 1000+ concurrent users
- Support 10,000+ courses
- Support 100,000+ applications
- Horizontal scaling capability
- Database sharding strategy (if needed)

**Caching Strategy:**
- Cache course catalog (TTL: 5 minutes)
- Cache course details (TTL: 10 minutes)
- Cache user sessions (Redis)
- CDN for static assets
- Browser caching headers configured

### 5. File Storage

**Structure:**
```
/uploads
  /applications
    /{application_id}
      /resume
      /certificates
      /id_proof
      /photos
      /other
  /courses
    /{course_id}
      /thumbnail
      /banner
      /videos
```

**Naming Convention:**
- {timestamp}_{uuid}_{sanitized_original_name}.{ext}
- Example: 1704024000_a1b2c3d4_john_doe_resume.pdf

**Access Control:**
- Pre-signed URLs for temporary access
- Document access requires authentication
- Admin access to all documents
- User access to own documents only

### 6. Email Templates

**Required Templates:**
1. Welcome email (registration)
2. Email verification
3. Password reset
4. Application submission confirmation
5. Application status update (approved)
6. Application status update (rejected)
7. Application status update (waitlisted)
8. Payment confirmation
9. Enrollment confirmation
10. Course reminder (before start)
11. Cohort advertisement
12. Application deadline reminder

**Template Variables:**
- User name
- Application number
- Course name
- Cohort details
- Payment details
- Custom fields

### 7. Testing Requirements

**Unit Tests:**
- Service layer functions
- Utility functions
- Validators
- Target: 80%+ code coverage

**Integration Tests:**
- API endpoint testing
- Database operations
- Third-party integrations (payment, email)

**End-to-End Tests:**
- Critical user journeys:
  - Complete application flow
  - Admin review and approval
  - Payment processing
- Tools: Cypress / Playwright / Selenium

**Load Testing:**
- Simulate 1000 concurrent users
- Test application submission under load
- Test course catalog performance
- Tools: k6 / JMeter / Gatling

### 8. Monitoring & Logging

**Application Monitoring:**
- Track API response times
- Monitor error rates
- Track user journey completion rates
- Alert on critical errors
- Dashboard for real-time metrics

**Business Metrics:**
- Applications submitted per day
- Application approval rate
- Average review time
- Course view to application conversion
- Payment success rate
- User registration rate

**Logging:**
- All API requests logged
- Error logs with stack traces
- Admin action audit logs
- Payment transaction logs
- Log retention: 90 days minimum

### 9. Backup & Disaster Recovery

**Database Backups:**
- Full backup: Daily
- Incremental backup: Every 6 hours
- Point-in-time recovery capability
- Backup retention: 30 days
- Backup testing: Monthly

**File Storage Backups:**
- Replicated across multiple regions
- Versioning enabled
- Soft delete (30-day retention)

**Disaster Recovery:**
- RTO (Recovery Time Objective): 4 hours
- RPO (Recovery Point Objective): 1 hour
- Disaster recovery plan documented
- Annual DR drills

### 10. Compliance & Legal

**Data Privacy:**
- Privacy policy displayed and accepted
- Cookie consent banner (for EU users)
- Data processing agreements with vendors
- Right to access personal data
- Right to delete personal data
- Data breach notification procedures

**Accessibility:**
- WCAG 2.1 Level AA compliance
- Keyboard navigation
- Screen reader support
- Alternative text for images
- Sufficient color contrast

**Legal:**
- Terms and conditions acceptance required
- Clear refund policy stated
- Age verification (minimum 13 years old)
- Parental consent for minors (if applicable)

---

## Research Sources

This documentation is based on industry research and best practices from:

- [Online Enrollment Process: Advantages & Best Practices](https://thinkorion.com/blog/online-enrollment-process)
- [The 2025 Guide to AI-Powered Admission Software](https://www.creatrixcampus.com/blog/admission-management-software-guide)
- [6 Best Cohort Based Learning Platforms [2025]](https://www.educate-me.co/blog/best-cohort-based-learning-platforms)
- [What is Cohort vs. Self-Paced Learning? - Wharton](https://executiveeducation.wharton.upenn.edu/thought-leadership/wharton-online-insights/cohort-vs-self-paced-learning/)
- [Cohort-Based Courses | Disco](https://www.disco.co/features/cohort-based-courses)
- [College Application Form Template | Jotform](https://www.jotform.com/form-templates/college-application-form)
- [Student Application Form Template | Formplus](https://www.formpl.us/templates/student-application-form-template)
- [The Course Catalog - LifterLMS](https://lifterlms.com/docs/course-catalog/)
- [WordPress Course Catalog Plugin for Online Courses | CreativeMinds](https://www.cminds.com/wordpress-plugins-library/course-catalog-lms-plugin-wordpress/)

---

## Next Steps for Development

### Phase 1: Foundation (Weeks 1-2)
- [ ] Set up development environment
- [ ] Choose and configure technology stack
- [ ] Set up database schema
- [ ] Implement authentication system
- [ ] Create basic user registration and login

### Phase 2: Course Management (Weeks 3-4)
- [ ] Develop course CRUD operations (admin)
- [ ] Implement course catalog public view
- [ ] Create course details page
- [ ] Add search and filter functionality
- [ ] Implement course image uploads

### Phase 3: Cohort Management (Weeks 5-6)
- [ ] Develop cohort CRUD operations (admin)
- [ ] Link cohorts to courses
- [ ] Display cohorts on course details
- [ ] Implement cohort advertising features
- [ ] Add cohort status management

### Phase 4: Application System (Weeks 7-10)
- [ ] Create multi-step application form
- [ ] Implement application draft saving
- [ ] Add document upload functionality
- [ ] Create application submission process
- [ ] Build user dashboard for tracking applications
- [ ] Develop admin application review interface
- [ ] Implement application status workflow
- [ ] Create email notification system

### Phase 5: Payment Integration (Weeks 11-12)
- [ ] Integrate payment gateway
- [ ] Implement payment processing
- [ ] Add discount code system
- [ ] Create payment confirmation flow
- [ ] Generate receipts

### Phase 6: Testing & Refinement (Weeks 13-14)
- [ ] Comprehensive testing (unit, integration, e2e)
- [ ] Performance optimization
- [ ] Security audit
- [ ] Bug fixes
- [ ] User acceptance testing (UAT)

### Phase 7: Launch Preparation (Week 15)
- [ ] Documentation finalization
- [ ] Admin training
- [ ] Deployment to production
- [ ] Monitoring setup
- [ ] Go-live

### Future Enhancements (Post-Launch)
- [ ] Mobile app (iOS/Android)
- [ ] Advanced analytics and reporting
- [ ] AI-powered course recommendations
- [ ] Chatbot for applicant support
- [ ] Integration with third-party systems
- [ ] Waitlist automation
- [ ] Scholarship management module
- [ ] Video interview scheduling
- [ ] Alumni testimonials integration
