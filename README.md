# Virtual-Smart-Campus-Management-System
## Overview
A Java-based console application to manage a virtual smart campus, including Students, Instructors, Staff, Courses, and Grade Records ,InputHelper,Lap,Room,Equipment,CampusResource,ReservationSystem.
### Classes
1. `People`
2. `Student`
3. `Instructor`
4. `Staff`
5. `Course`
6. `GradeRecord`
7. `CampusSystem`
8. `InputHelper`
9. `Lap`
10. `Room`
11. `Equipment`
12. `CampusResource`
13. ` Equipment`
14. `ReservationSystem`

#### 1. Class People
**`Description:`**
 Represents a generic person in the system (parent class for Instructor, Student, and Staff).
Handles basic personal information and input validation.

*`Attributes:`*  

| Attribute    | Type         | Description |
|:------------|:-------------|:------------------|
| id         | int        | Unique academic   ID (positive integer) |
| name       | String     | Full name (must not contain numbers or symbols) |
| e_mail     | String     | Auto-generated university email based on name and ID |
| phoneNumber| int        | Phone number (validated to be digits only) |
| dateOfBirth| LocalDate  | Date of birth, validated using a fixed date format |
| nationalID | String     | National ID number (14 digits only) |
| scanner    | Scanner    | Input object for reading user input |
| DATE_FORMATTER | DateTimeFormatter | Static formatter for standardizing date input |

*Methods with Usage Examples:* 
- **`setPhoneNumber()`**
  - *Purpose:* Asks user for phone number and validates it's an integer.
  -  *`Example:`*
  ```
    Enter your phone number: 0123456789
  ```
   - *`Example interaction:`*
    ```  
    Enter your name (no numbers allowed): Ali Hassan
    Enter your academic ID (positive number): 12345
    Your email has been set to: ali224101523@ksiu.edu.eg
     ```
     
  - **`setDateOfBirth()`**
  - *Purpose:* Collects and validates birth date, ensures it’s not in the future, and calculates age.
  - *`Example:`*
    ```
    Enter your birth date (day/month/year, e.g. 7/7/2006): 15/08/2000
    Age: 23 years, 9 months
    ```

- **`setNationalID()`**
  - *Purpose:* Ensures the National ID is a 14-digit number.
  - *`Example:`*
    ```
    Enter your national ID (14 digits): 30007150123456
    ```

- **`displayUserData()`**
  - *Purpose:* Displays a summary of entered user data.
  - *`Example output:`*
    ```
    User Data Summary:
    Phone Number: 0123456789
    Date of Birth: 7/7/2006
    National ID: 30007150123456
    Current Age: 18 years, 10 months
    ```
   *Special Notes:*  
Uses `LocalDate` and `DateTimeFormatter` for reliable date management.  
Email is generated like:
```java
String firstName = this.name.split("\\s+")[0];
String name = firstName.toLowerCase().replaceAll("[^a-z]", "");
this.e_mail = name + this.id + "@ksiu.edu.eg"; 
```
##### 2. Class Student

**`Description:`**
The Student class represents a student in the virtual campus system. It inherits from the People class, and adds academic attributes and functionality like course registration, grade management, and GPA calculation.
---
*`Attributes:`*

| Attribute        | Type                    | Description                                         |
|------------------|-------------------------|-----------------------------------------------------|
| scanner          | Scanner                 | Input object for reading user input                |
| level            | String                  | Academic level of the student                      |
| enrolledCourses  | ArrayList<Course>       | List of courses the student is enrolled in         |
| gradeRecords     | ArrayList<GradeRecord>  | Records of grades for each enrolled course         |
---
*Methods with Usage Examples:* 

- **`registerCourse(Course course)`**

- Purpose: Registers the student in a course and adds a new empty GradeRecord for it.

 - *`Example interaction:`*
```
- student.registerCourse(programming101);
```
 - *`Console Output:`*
  ```
- Ali registered for Programming 101
```
 - **`getGradeRecordForCourse(Course course)`**

- Purpose: Returns the GradeRecord linked to a course if the student is enrolled.

 - *`Example:`*
```
- GradeRecord record = student.getGradeRecordForCourse(programming101);
```
- **`calculateOverallGPA()`**

- Purpose: Calculates and returns the average GPA from all enrolled courses.

 - *`Example:`*
```
- double gpa = student.calculateOverallGPA();
- System.out.println("Total GPA: " + gpa);
```

- **`viewGrades()`**
- Purpose: Displays all grades (quizzes, assignments, midterm, final) for each course, and shows individual course GPA and total GPA.

- *`Example output:`*
```
Course: oop101
Quizzes: [10.0, 9.0]
Assignments: [20.0, 18.0]
Midterm: 40.0
Final: 50.0
Course GPA: 3.7
Total GPA: 3.6
```
- **`viewProfile()`**

- Purpose: Displays the student’s academic level and total GPA.

- *`Example:`*
```
Level: Level 2
Total GPA: 3.6
```
---
 *Special Notes:*  
- **enrolledCourses** and **gradeRecords** are *parallel lists* — meaning:  
  The record at index i in gradeRecords directly corresponds to the course at index i in enrolledCourses.

- Inherits all personal data management attributes and methods from the **People** class, including:  
  id, name, email, phoneNumber, dateOfBirth, and nationalID.

- *GPA Calculation:*  
  GPA is computed by iterating over each **GradeRecord** associated with enrolled courses and averaging the results returned by the **calculateGPA()** method.

- *Grade and GPA Display:*  
  Provides organized summaries of each course’s grades, individual GPAs per course, and an overall GPA.

- *Dynamic Course Registration:*  
  When a student registers for a course, a corresponding empty **GradeRecord** is created and added to the **gradeRecords** list, keeping both lists in sync.

###### 3. Class Instructor
*`Description:`*  
The Instructors class extends People and represents a university instructor. It adds instructor-specific data like department, office number, and title. It also manages the courses the instructor teaches and handles grade entry for students.

---

*`Attributes:`*  

| Attribute         | Type                  | Description |
|:------------------|:---------------------|:----------------------------------------------------|
| department       | String              | Instructor’s academic department |
| officenumber     | String              | Office number of the instructor |
| title            | String              | Job title (e.g., Professor, Assistant Lecturer) |
| teachingCourses  | ArrayList<Course>   | List of courses assigned to this instructor |

---

*Methods with Usage Examples:*  
- **addCourse(Course course)**
  - *Purpose:* Adds a course to the instructor’s teaching list if not already assigned.
  - *Example:*
    ```
    java
    instructor.addCourse(newCourse);
    ```

- **removeCourse(Course course)**
  - *Purpose:* Removes a course from the instructor’s teaching list.
  - *Example:*
    ```
    java
    instructor.removeCourse(specificCourse);
    ```

- **viewTeachingCourses()**
  - *Purpose:* Displays a list of all courses this instructor teaches.
  - *Example:*
    ```
    java
    instructor.viewTeachingCourses();
    ```

- **enterStudentGrades(Scanner input, Course course)**
  - *Purpose:* Allows the instructor to input grades for students enrolled in a given course.
  - *How it works:*
    ``` 
    1. Lists enrolled students.  
    2. Prompts to select a student.  
    3. Requests number and grades of quizzes, assignments, midterm, and final exam.  
    4. Validates each input.
    ```
- **enterInstructorData(Scanner input)**
  - *Purpose:* Collects instructor-specific data via console input.
     - *Example:*
    ```
    Enter Department: Computer Science
    Enter Office Number: B201
    Enter Title: Assistant Lecturer
    ```

- **viewProfile()**
  - *Purpose:* Displays the instructor’s personal and professional profile.
  - *Example output:*
    ```
    Instructor Name: Ahmed Ali
    Department: Computer Science
    Office Number: B201
    Email: ahmed12345@ksiu.edu.eg
    Title: Lecturer
    Phone Number: 01123456789
   ``` 

---

*Special Notes:*  

- The class inherits all attributes and validation logic from People.
- It manages a list of teachingCourses using an ArrayList<Course>.
- Grade entry is fully validated (e.g., numbers only, within valid range, no future dates).
- Uses interactive console input for both personal and course management.

####### 4. Class Staff
*Description:*  
The Staff class extends the People class and represents non-academic employees working in the virtual campus system, such as system administrators or clerical staff. It adds staff-specific data like position, department, working hours, and salary.

---

*`Attributes:`*  

| Attribute     | Type        | Description |
|:--------------|:-------------|:------------------|
| position     | String     | The job title or role of the staff member |
| department   | String     | Department where the staff works |
| workingHours | int        | Number of working hours per week |
| salary       | double     | Monthly salary of the staff member |

---

*Methods with Usage Examples:*  

- **getPosition() / setPosition(String position)**  
  - *Purpose:* Retrieve or set the staff member's job title.  
  - *`Example:`*
    ```
    
    staff.setPosition("System Administrator");
    System.out.println(staff.getPosition());
    ```
- **getDepartment() / setDepartment(String department)**  
  - *Purpose:* Retrieve or set the staff member's department.  
  - *`Example:`*
    ```
    staff.setDepartment("IT Services");
    ```

- **getWorkingHours() / setWorkingHours(int hours)**  
  - *Purpose:* Retrieve or set the number of working hours.  
  - *`Example:`*
   ```
    staff.setWorkingHours(40);
    ```

- **getSalary() / setSalary(double salary)**  
  - *Purpose:* Retrieve or set the staff member's salary.  
  - *Example:*
   ```
    staff.setSalary(8000.50);
    ```

- **Staff()**  
  - *Purpose:* Simple method that prints "staff" to indicate the object type.

---

*`Special Notes:`*  

- Inherits personal data and validation behavior from the People class.
- Acts as a simple data holder with standard getter and setter

#### 5. Class Course


*`Description:`* 
The Course class represents an academic course in the virtual campus system. It manages information about the course, its instructor, enrolled students, and grading breakdown.
---
*`Attributes:`* 

| Attribute             | Type                  | Description                                           |
|-----------------------|-----------------------|-------------------------------------------------------|
| courseCode            | String                | Unique code that identifies the course                |
| courseName            | String                | Full name of the course                               |
| instructor            | Instructors           | Instructor assigned to teach the course               |
| students              | ArrayList<Students>   | List of students enrolled in the course               |
| quizPercentage        | double                | Percentage weight for quizzes (0 → 1)                 |
| assignmentPercentage  | double                | Percentage weight for assignments (0 → 1)             |
| midtermPercentage     | double                | Percentage weight for midterm exam (0 → 1)            |
| finalPercentage       | double                | Percentage weight for final exam (0 → 1)              |

---
*Methods with Usage Examples:* 

- **`addStudent(Students student)`**

- Purpose: Adds a student to the list of enrolled students in the course.

- *`Example:`*
```
course.addStudent(student);

```
- **`assignInstructor(Instructors instructor)`**

Purpose: Assigns an instructor to the course and prints a confirmation message.

- *`Example:`*
```
course.assignInstructor(instructor);
```
- *`Example output:`*
```
Ahmed assigned to course Programming Fundamentals
```

- **`viewCourseDetails()`**

- Purpose: Displays the course code, name, instructor, and list of enrolled students.
-  *`Example output:`*
  ```
- Course Code: CS101
- Course Name: Programming Fundamentals
- Instructor: Ahmed
- Enrolled Students:
  - Ali
  - Mariam
```
---

Special Notes:

The total of all percentage attributes (quiz, assignment, midterm, final) should equal 1.0 (or 100%) to fairly distribute grades.

A course can be created without an instructor initially.

The ArrayList<Students> grows dynamically as students register.

---
#### 6.Class GradeRecord
*`Description:`* 
The GradeRecord class is responsible for holding the grades for a student in a particular course. It stores individual quiz and assignment grades, as well as midterm and final exam grades, and can calculate the GPA based on course weightings.


---
*`Attributes:`* 

| Attribute     | Type              | Description                                        |
|---------------|-------------------|----------------------------------------------------|
| quizzes       | ArrayList<Double> | List of quiz grades                                |
| assignments   | ArrayList<Double> | List of assignment grades                          |
| midterm       | double            | Grade for the midterm exam                         |
| finalExam     | double            | Grade for the final exam                           |

---
*Methods with Usage Examples:* 

-**`addQuiz(double grade)`**

Purpose: Adds a quiz grade to the list.

- *`Example:`*
```
- record.addQuiz(18.5);
```

- **`addAssignment(double grade)`**

- Purpose: Adds an assignment grade to the list.

- *`Example:`*
```
- record.addAssignment(19.0);
```

- **`setMidterm(double grade)`**

- Purpose: Sets the midterm exam grade.

- *`Example:`*

record.setMidterm(30);


- **`setFinalExam(double grade)`**

Purpose: Sets the final exam grade.

- *`Example:`*
```
record.setFinalExam(45);
```

- **`calculateGPA(Course course)

Purpose: Calculates the overall GPA for the course based on the weighted average of all components (quizzes, assignments, midterm, final).

- *`Example:`*
```
double gpa = record.calculateGPA(course);
System.out.println("GPA: " + gpa);
```



---

Special Notes:

Uses defensive copying when returning quiz and assignment lists via getQuizzes() and getAssignments() to protect internal data.

GPA is calculated on a 4.0 scale, where a total score out of 100 is converted to a GPA out of 4.

Internal helper method calculateAverage() safely computes averages even if the grade list is empty.

---
#### 7. Class CampusSystem
*`Description:`* 
The CampusSystem class acts as the main management system for handling Students, Instructors, Staff, and Courses. It provides menus for different roles, adding entities, course registration, grade entry, and viewing details.

---
*`Attributes:`* 

| Attribute Name   | Data Type                  | Description                                                              |
|------------------|----------------------------|--------------------------------------------------------------------------|
| students         | ArrayList<Students>        | A list that holds all student objects in the system.                     |
| instructors      | ArrayList<Instructors>     | A list that holds all instructor objects in the system.                  |
| staffMembers     | ArrayList<Staff>           | A list containing administrative or teaching staff members.              |
| courses          | ArrayList<Course>          | A list of all courses available in the campus system.                    |
| input            | Scanner                    | A scanner object used to read user input from the console.               |

---
*Methods with Usage Examples:* 

- **`addStudent(Students student)`**
- Adds a student to the course enrollment list.
- *`Example:`*
```
Course c = new Course("CS101", "Java Basics", 0.2, 0.2, 0.3, 0.3);
Students s = new Students("Level 1");
c.addStudent(s);
```
- assignInstructor(Instructors instructor)
- Assigns an instructor to the course.
- *`Example:`*
```
Instructors i = new Instructors("CS", "B203", "Dr.");
c.assignInstructor(i);
```
-**`getStudents()`**
- Returns a list of enrolled students.

`**`viewCourseDetails()`**
- Displays course code, name, assigned instructor, and enrolled students.
-  *`Example output:`*
```
Course Code: CS101
Course Name: Java Basics
Instructor: Dr. Sameh
Enrolled Students:
- Ali Ahmed
- Sara Ibrahim
- getQuizPercentage() / getAssignmentPercentage() / getMidtermPercentage() / getFinalPercentage()
Return the respective grading percentage for course components.

```
Special Notes:

- The class uses an ArrayList<Students> for dynamic student registration.
- Assigning an instructor automatically displays a confirmation message.
- The grading weight percentages must be set upon course creation and should total 1.0 (100%).
---
#### 1. Class InputHelper
*`Description:`* 
The InputHelper class is a utility class that assists with taking role and gender selections from the console. It defines two enums — one for system roles and one for genders — and provides selection methods with input validation.

---

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
| Gender	         | enum private       | Enum for gender selection (Male, Female) |
|Role	             | enum public        |Enum for role selection (Instructor, Staff, Student)|

---
*Methods with Usage Examples:* 

- **`selectRole()`**
- Displays available roles and prompts the user to select one with validation.

Example interaction:
```
1. Instructor
2. Staff
3. Student
Please select a role (1-3): 2
You selected: Staff
```
- **`selectGender()`**
- Displays available genders and prompts for selection with validation.

-**`Example interaction:`**
```
1. Male
2. Female
Please select a gender (1-2): 1
```


---

Special Notes:

Uses Scanner for console input.

Implements robust input validation to handle:

Empty inputs

Non-numeric inputs

Numbers outside valid selection ranges

---
Both methods loop until a valid input is provided.


Example Enum Declaration:

public enum Role {
    Instructor,
    Staff,
    Student;
}


---
#### 9. Class Lap

Description:
The Lab class extends CampusResource and represents a specialized lab facility inside the campus system. It could be a computer lab, chemistry lab, or any other type — specified by the labType attribute. It also keeps track of available equipment.


---

Attributes:

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
|equipment  	| List<String>	|List of equipment items in the lab
|labType	    |String       	|Type of lab (e.g., "Computer", "Physics")




---

Methods:

Constructor

- Usage:
- Creates a new lab instance.
- Lab chemistryLab = new Lab("LAB101", "Building B - Floor 2", 30, "Chemistry");


getResourceType()

Purpose:
Returns a string indicating the type of resource — for example "Chemistry Lab".


addEquipment(String item)

Purpose:
Adds a new equipment item to the lab's equipment list.

Example:
```
chemistryLab.addEquipment("Beaker Set");
```



---

Special Notes:

The equipment list should be initialized (e.g., via constructor or directly at declaration — currently missing in your code; consider adding equipment = new ArrayList<>(); inside the constructor).

Inherits core attributes like id, location, and capacity from the CampusResource class.
---
#### 10. Class Room
Description:
The Room class extends CampusResource and represents a lecture or study room within the campus. It can optionally be equipped with a projector.


---

Attributes:

Attribute	Type	Description

| Attribute Name   | Data Type                  | Description                             |
|------------------|----------------------------|-----------------------------------------|
|hasProjector  	| boolean	|Indicates whether the room has a projector

- Inherited Attributes (from CampusResource):

| Attribute Name   | Data Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
| id               | String                     |Unique identifier for the resource                  |
| location         | String                     | Physical location of the resource                  |
| capacity         | int	                      | Maximum capacity of the resource                   |

---

Methods:

Constructor

Usage:
Creates a new room instance.

Room lectureRoom = new Room("R101", "Main Building - Floor 1", 50, true);


getResourceType()

Purpose:
Returns a string indicating the type of room.
If the room has a projector, it appends (Projector) to the type.

Example Output:

Lecture Room (Projector)


hasProjector()

Purpose:
Returns a boolean value indicating whether the room has a projector.

Example:

if (lectureRoom.hasProjector()) {
    System.out.println("Projector is available.");
}




---

Special Notes:

This class is a specialized resource derived from the abstract/base CampusResource.

The getResourceType() method is overridden to customize the description based on room features.
---
#### 11. Class Equipment

Description:
The Equipment class represents a single piece of equipment in the campus system, like a printer, microscope, or projector. It extends the CampusResource class and defines equipment-specific attributes.


---

Attributes:

Attribute	Data Type	Description
| Attribute Name   | Data Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|equipmentType              | String            |Type of the equipment (e.g. "Projector", "Microscope")    |
| location         | String                     | The manufacturer brand of the equipment                  |

---

Constructor:
```
public Equipment(String id, String location, String type, String manufacturer)

Initializes the equipment with a unique ID, location, type, and manufacturer.

Note: Capacity is always set to 1 since it represents a single item.
```


---

Methods:

Method	Return Type	Description
| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|getResourceType()              | String            |TReturns a string combining equipment type and manufacturer (e.g. "Printer (HP)")    |

---

Example:
```
Equipment printer = new Equipment("EQ123", "Building A", "Printer", "HP");
System.out.println(printer.getResourceType()); // Output: Printer (HP)
```

---
###### 13. Class CampusResource

Description:
CampusResource is an abstract class representing any reservable resource within the campus (like rooms, labs, or equipment). It defines common properties and behaviors that all campus resources share.


---

Attributes:

Attribute	Data Type	Description

resourceId	String	Unique identifier for the resource
location	String	Physical location of the resource
capacity	int	Maximum capacity (number of people it can hold, or 1 for equipment)
isAvailable	boolean	Indicates whether the resource is currently available
reservedUntil	LocalDateTime	Time until which the resource is reserved (if any)



---

Constructor:

public CampusResource(String resourceId, String location, int capacity)

Initializes resource ID, location, and capacity.



---

Abstract Method:

Method	Return Type	Description
| Attribute Name   | Data Type                  | Description                                                              |
|------------------|----------------------------|--------------------------------------------------------------------------|
| getResourceType()    | String           |Must be implemented by subclasses to return the resource type (e.g. "Lecture Room", "Computer Lab")    |



---

Concrete Methods:

Method	Return Type	Description
| Attribute Name   | Data Type                  | Description                                                              |
|------------------|----------------------------|--------------------------------------------------------------------------|
| reserve(LocalDateTime until)    | boolean           | Reserves the resource until a given time if available       |
| release()	                      |	boolean           | Releases the resource and marks it available again          |
| getResourceId()                 |String             |Returns the unique ID of the resource                        |
|getLocation()                    |String             | Returns the location of the resource                        |
|getCapacity()                    |	int               |	Returns the capacity of the resource                        |
|isAvailable()	                  |boolean            | Checks if the resource is available                         |
         


---

Example:
```
Room room1 = new Room("R101", "Building A", 50, true);
System.out.println(room1.getResourceType()); // Lecture Room (Projector)

room1.reserve(LocalDateTime.now().plusHours(2));
System.out.println(room1.isAvailable()); // false
room1.release();
System.out.println(room1.isAvailable()); // true
```
---
###### 14. Class ReservationSystem

Description:
The ReservationSystem class manages campus resources (like rooms, labs, and equipment) and handles their reservations by people. It ensures no double-booking and allows querying available resources.


---

Attributes:

Attribute	Data Type	Description
| Attribute Name   | Data Type                  | Description                                                              |
|------------------|----------------------------|--------------------------------------------------------------------------|
| resources        |Map<String, CampusResource>>           | CampusResource>	A collection of all resources on campus, mapped by their unique ID     |
| release()	       |	Map<String, People>                  | 	Keeps track of which person reserved which resource         |

---

Methods:

Method	Return Type	Description
| Attribute Name   | Data Type                  | Description                                                              |
|addResource(CampusResource resource )                                                    |	         void	Adds a new campus resource to the system|
|makeReservation(String resourceId, People person, LocalDateTime start, LocalDateTime end)|	boolean	Reserves a resource for a person if it’s available|
|isResourceAvailable(String resourceId)                                                   |	boolean	Checks if a specific resource is currently available|
|getResources()	Map<String, CampusResource>                                               |Returns a list of all managed resources|
|getUserReservations(int id)	Map<String, LocalDateTime>	                                |(Currently placeholder) — would ideally return all reservations by user ID|



---

Example Usage:
```
ReservationSystem system = new ReservationSystem();

Room room1 = new Room("R101", "Building A", 50, true);
system.addResource(room1);

People person = new People();
person.setDetails();

boolean reserved = system.makeReservation("R101", person, LocalDateTime.now(), LocalDateTime.now().plusHours(2));

System.out.println("Reservation successful: " + reserved);

```
---

Special Notes:

Uses HashMap for quick lookup of resources by ID.

makeReservation internally updates both the resource status and tracks which person reserved it.

The getUserReservations is currently a placeholder method returning an empty map — could be expanded to show personal reservations.
