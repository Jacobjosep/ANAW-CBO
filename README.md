# ANAW - Act of Networking and Welfare

A comprehensive web platform for managing networking and welfare activities supporting communities in Sudan through global collaboration.

## 🌟 Overview

ANAW is a web-based platform that connects members worldwide to support communities in Sudan through networking, welfare programs, and collaborative efforts. The system provides separate interfaces for administrators and members with role-based access control.

## ✨ Features

### Public Website
- **Responsive Design**: Mobile-friendly interface with modern UI
- **Tab-based Navigation**: Home, About, Programs, Meetings, Donate, Contact
- **Interactive Elements**: Smooth animations and transitions
- **Contact Form**: Integrated with FormSubmit for email handling
- **Social Media Integration**: Links to various platforms

### Admin Dashboard
- **Member Management**: Add, view, and delete members
- **Meeting Scheduling**: Create and manage virtual meetings
- **Project Management**: Track active projects and budgets
- **Announcement System**: Post updates to different user groups
- **Statistics Overview**: Dashboard with key metrics

### Member Dashboard
- **Personal Donation Tracking**: View donation history and totals
- **Meeting Access**: Join scheduled virtual meetings
- **Announcement Feed**: Stay updated with organization news
- **Project Information**: View active initiatives
- **Donation Portal**: Make contributions to specific projects

## 🛠️ Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript
- **Backend**: PHP
- **Database**: MySQL
- **Styling**: Custom CSS with CSS Variables
- **Icons**: Font Awesome 6.4.0
- **Forms**: FormSubmit.co for contact form handling

## 📁 Project Structure



# ANAW-CBO
Act of Networking And Networking 

## 🚀 Installation & Setup

### Prerequisites
- Web server (Apache/Nginx)
- PHP 7.4 or higher
- MySQL 5.7 or higher
- Modern web browser

### Database Setup
1. Create a MySQL database named `anaw_db`
2. Import the following table structure:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    country VARCHAR(50),
    role ENUM('admin', 'member') DEFAULT 'member',
    status ENUM('active', 'inactive') DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE meetings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    description TEXT,
    meeting_link VARCHAR(500),
    meeting_date DATETIME,
    duration INT,
    status ENUM('scheduled', 'completed', 'cancelled') DEFAULT 'scheduled',
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);

CREATE TABLE projects (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    description TEXT,
    location VARCHAR(100),
    budget DECIMAL(10,2),
    status ENUM('planning', 'active', 'completed', 'on_hold'),
    start_date DATE,
    end_date DATE,
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);

CREATE TABLE announcements (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    content TEXT NOT NULL,
    type ENUM('general', 'project', 'meeting', 'financial'),
    priority ENUM('low', 'medium', 'high'),
    target_audience ENUM('all', 'members', 'admins'),
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES users(id)
);

CREATE TABLE donations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    member_id INT,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'USD',
    donation_type ENUM('one-time', 'monthly', 'quarterly', 'annual'),
    project_id INT NULL,
    status ENUM('pending', 'confirmed', 'cancelled') DEFAULT 'pending',
    donation_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (member_id) REFERENCES users(id),
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
