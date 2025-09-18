# Lab1

**Course:** Bachelor of Informatics Management and Engineering

## Description

This hands-on lab serves as students introduction to Flutter's widget system by building a static personal profile app. 
Students will explore layout widgets, display components, and scrolling views while applying theming and styling principles. 
By the end of this lab, students will have built a polished mobile app profile showcasing various Flutter widgets and layout techniques.

## Learning Objectives

By completing this lab, you will be able to:

- Implement and customize fundamental Flutter widgets for layout and display
- Build responsive user interfaces using Row, Column, Stack, and Container widgets
- Create visually appealing static content using Text, Image, Icon, and Card widgets
- Design scrollable layouts using SingleChildScrollView, ListView, and GridView widgets
- Apply consistent theming, styling, and Material Design principles
- Understand widget composition and the Flutter widget tree structure

## Setup Instructions

### 1. Create a New Flutter Project

Option 1: Open your terminal/command prompt (in the directory you desire) and run:

```bash
flutter create lab1
cd lab1
```

Option 2: Open Android Studio and go to  File > New Project > New Flutter Project. Name it lab1. (Skip Step 2)

### 2. Open the Project

Open the project folder in your preferred IDE.

### 3. Run the App

Connect a device/emulator and run:

```bash
flutter run
```

You should see the default Flutter counter app. We'll replace this with our static profile app.

---

## Lab Tasks

### Task 1: Project Setup and Custom Theming 

**Objective:** Set up the app structure and apply a custom theme with deep purple colors (or any other color you find fancy 😄).

**Your Challenge:**
1. Replace the contents of `lib/main.dart` to create a new app called "Static Profile App"
2. Create a custom theme with deep purple colors and custom styling for AppBar, Cards, and text
3. Create a `ProfilePage` as a `StatelessWidget` with an AppBar and placeholder body content

**Example of Code:**
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Static Profile App',
      theme: ThemeData(
        primarySwatch: Colors.deepPurple,
        // TODO: Add appBarTheme with backgroundColor and foregroundColor
        // TODO: Add cardTheme with elevation, margin, and rounded corners
        // TODO: Add custom textTheme for different heading sizes
      ),
      home: ProfilePage(),
    );
  }
}

class ProfilePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Alex Johnson'),
        centerTitle: true,
        // TODO: Add actions with more_vert icon
      ),
      body: Container(
        child: Text('Profile content will go here'),
      ),
    );
  }
}
```

**Hints:**
- `CardTheme` shape needs `RoundedRectangleBorder.circular(12)`
- Text themes use properties like `headlineLarge`, `headlineMedium`, `bodyLarge`

### Task 2: Profile Header with Complex Layouts 

**Objective:** Create a profile header using Stack, Container, Row, and Column widgets with a cover photo and overlaid profile picture.

**Your Challenge:**
1. Replace the body with a `SingleChildScrollView` containing a Column
2. Create a cover photo section with gradient background and overlaid profile picture
3. Add profile information below the cover photo

**Starter Code Structure:**
```dart
body: SingleChildScrollView(
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      // TODO: Cover Photo Container with Stack
      Container(
        height: 200,
        width: double.infinity,
        decoration: BoxDecoration(
          gradient: LinearGradient(
            // TODO: Add gradient from deepPurple[300] to deepPurple[600]
          ),
        ),
        child: Stack(
          children: [
            // TODO: Background image with opacity
            // TODO: Positioned profile picture at bottom-left
          ],
        ),
      ),
      
      // TODO: Profile Information Container
      Container(
        padding: EdgeInsets.fromLTRB(24, 60, 24, 20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                // TODO: Name, title, and location column
                // TODO: Available status badge
              ],
            ),
          ],
        ),
      ),
      
      SizedBox(height: 8),
    ],
  ),
),
```

**Sample Image URLs:**
- Cover: `'https://images.unsplash.com/photo-1579952363873-27d3bfad9c0d?w=800'`
- Profile: `'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400'`

**Key Widgets to Use:**
- `Positioned(bottom: -50, left: 24, child: ...)` for profile picture
- `CircleAvatar` with `backgroundImage: NetworkImage(...)`
- `Container` with white border and shadow for profile picture frame

### Task 3: Statistics Cards Row 

**Objective:** Create three statistics cards displayed in a horizontal row.

**Your Challenge:**
Create three equal-width cards showing statistics: "127 Projects", "5.2K Followers", and "4.8 Rating"

**Code Template:**
```dart
// Statistics Row
Container(
  padding: EdgeInsets.symmetric(horizontal: 16),
  child: Row(
    children: [
      Expanded(
        child: Card(
          child: Padding(
            padding: EdgeInsets.all(16),
            child: Column(
              children: [
                Text(
                  '127',
                  style: TextStyle(
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                    color: Colors.deepPurple[600],
                  ),
                ),
                // TODO: Add spacing and label text
              ],
            ),
          ),
        ),
      ),
      // TODO: Add two more Expanded cards for Followers and Rating
    ],
  ),
),

SizedBox(height: 16),
```

**Hints:**
- Use `SizedBox(height: 4)` between number and label
- Labels should use `Theme.of(context).textTheme.bodyMedium`
- All three cards should follow the same structure

### Task 4: About Section with Rich Content 

**Objective:** Create an about section with icons, text, and info chips.

**Your Challenge:**
1. Create a Card with an "About" section that includes:
   - Header with person icon and "About" title
   - A divider line
   - Paragraph of text about the person (justified alignment)
   - Three info chips in a Wrap widget showing experience, apps built, and rating

**Hints:**
- Use `Row` with `Icon` and `Text` for the header
- `Divider` widget creates horizontal lines
- `textAlign: TextAlign.justify` for paragraph text
- `Wrap` widget handles chips that might overflow to next line
- Create a helper method `_buildInfoChip()` that returns a styled Container
- Info chips should have background color, border, and small text

**Suggested info chips:**
- "5+ Years Experience" 
- "50+ Apps Built"
- "Top Rated Developer"

### Task 5: Skills Grid

**Objective:** Display skills using GridView in a fixed-height scrollable container.

**Your Challenge:**
1. Create a Card with "Skills & Technologies" section
2. Use `GridView.count` with:
   - 3 columns (`crossAxisCount: 3`)
   - Fixed height container (200px)
   - Display 9 different skills with icons

**Hints:**
- `Container` with fixed `height` containing `GridView.count`
- Create `_buildSkillChip()` method that takes skill name and IconData
- Each skill chip should have:
  - Gradient background (light to darker purple)
  - Rounded corners and shadow
  - Icon above text
  - Small, bold text
- Adjust `childAspectRatio` to make chips look good (try 2.5)

**Skills to include:**
Flutter, Dart, Firebase, JavaScript, Python, Git, UI/UX, REST APIs, GraphQL

**Matching Icons:**
`Icons.flutter_dash`, `Icons.code`, `Icons.local_fire_department`, etc.

### Task 6: Projects ListView 

**Objective:** Create a scrollable list of projects using ListView.builder.

**Your Challenge:**
1. Create a "Recent Projects" Card section
2. Add a fixed-height Container (280px) with ListView.builder
3. Display 4 projects, each showing:
   - Colored icon container on the left
   - Project name, description, and tech stack
   - Arrow icon on the right

**Hints:**
- Create a List of Maps at the top of your class with project data
- Each project Map should contain: name, description, tech, color, icon
- `ListView.builder` with

## Deliverables

You are required to .zip file this project and deliver it in Moodle before the next class. 
