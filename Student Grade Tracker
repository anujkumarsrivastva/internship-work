import java.util.*;

class Grade {
    private String subject;
    private double score;
    
    public Grade(String subject, double score) {
        this.subject = subject;
        this.score = score;
    }
    
    public String getSubject() { return subject; }
    public double getScore() { return score; }
    
    @Override
    public String toString() {
        return subject + ": " + score;
    }
}

class Student {
    private String name;
    private int studentId;
    private ArrayList<Grade> grades;
    
    public Student(String name, int studentId) {
        this.name = name;
        this.studentId = studentId;
        this.grades = new ArrayList<>();
    }
    
    public void addGrade(String subject, double score) {
        if (score >= 0 && score <= 100) {
            grades.add(new Grade(subject, score));
        } else {
            System.out.println("Invalid grade! Please enter a grade between 0 and 100.");
        }
    }
    
    public double calculateAverage() {
        if (grades.isEmpty()) return 0.0;
        
        double sum = 0;
        for (Grade grade : grades) {
            sum += grade.getScore();
        }
        return sum / grades.size();
    }
    
    public double getHighestGrade() {
        if (grades.isEmpty()) return 0.0;
        
        double highest = grades.get(0).getScore();
        for (Grade grade : grades) {
            if (grade.getScore() > highest) {
                highest = grade.getScore();
            }
        }
        return highest;
    }
    
    public double getLowestGrade() {
        if (grades.isEmpty()) return 0.0;
        
        double lowest = grades.get(0).getScore();
        for (Grade grade : grades) {
            if (grade.getScore() < lowest) {
                lowest = grade.getScore();
            }
        }
        return lowest;
    }
    
    public Grade getHighestGradeWithSubject() {
        if (grades.isEmpty()) return null;
        
        Grade highest = grades.get(0);
        for (Grade grade : grades) {
            if (grade.getScore() > highest.getScore()) {
                highest = grade;
            }
        }
        return highest;
    }
    
    public Grade getLowestGradeWithSubject() {
        if (grades.isEmpty()) return null;
        
        Grade lowest = grades.get(0);
        for (Grade grade : grades) {
            if (grade.getScore() < lowest.getScore()) {
                lowest = grade;
            }
        }
        return lowest;
    }
    
    public ArrayList<Grade> getGradesBySubject(String subject) {
        ArrayList<Grade> subjectGrades = new ArrayList<>();
        for (Grade grade : grades) {
            if (grade.getSubject().toLowerCase().contains(subject.toLowerCase())) {
                subjectGrades.add(grade);
            }
        }
        return subjectGrades;
    }
    
    public String getLetterGrade() {
        double avg = calculateAverage();
        if (avg >= 90) return "A";
        else if (avg >= 80) return "B";
        else if (avg >= 70) return "C";
        else if (avg >= 60) return "D";
        else return "F";
    }
    
    // Getters
    public String getName() { return name; }
    public int getStudentId() { return studentId; }
    public ArrayList<Grade> getGrades() { return grades; }
    public int getGradeCount() { return grades.size(); }
}

public class StudentGradeTracker {
    private ArrayList<Student> students;
    private Scanner scanner;
    
    public StudentGradeTracker() {
        students = new ArrayList<>();
        scanner = new Scanner(System.in);
    }
    
    public void displayMenu() {
        System.out.println("\n========== STUDENT GRADE TRACKER ==========");
        System.out.println("1. Add New Student");
        System.out.println("2. Add Grade to Student");
        System.out.println("3. View Student Details");
        System.out.println("4. Display All Students Summary");
        System.out.println("5. Search Student by Name");
        System.out.println("6. View Grades by Subject");
        System.out.println("7. Class Statistics");
        System.out.println("8. Remove Student");
        System.out.println("9. Exit");
        System.out.print("Enter your choice (1-9): ");
    }
    
    public void addStudent() {
        System.out.print("Enter student name: ");
        String name = scanner.nextLine();
        
        System.out.print("Enter student ID: ");
        int id = scanner.nextInt();
        scanner.nextLine(); // consume newline
        
        // Check if student ID already exists
        for (Student student : students) {
            if (student.getStudentId() == id) {
                System.out.println("Student ID already exists! Please use a different ID.");
                return;
            }
        }
        
        students.add(new Student(name, id));
        System.out.println("Student added successfully!");
    }
    
    public void addGradeToStudent() {
        if (students.isEmpty()) {
            System.out.println("No students found. Please add students first.");
            return;
        }
        
        System.out.print("Enter student ID: ");
        int id = scanner.nextInt();
        scanner.nextLine();
        
        Student student = findStudentById(id);
        if (student == null) {
            System.out.println("Student not found!");
            return;
        }
        
        System.out.print("Enter subject name: ");
        String subject = scanner.nextLine();
        
        System.out.print("Enter grade for " + subject + " (0-100): ");
        double grade = scanner.nextDouble();
        scanner.nextLine();
        
        student.addGrade(subject, grade);
        System.out.println("Grade added successfully for " + subject + "!");
    }
    
    public void viewStudentDetails() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        System.out.print("Enter student ID: ");
        int id = scanner.nextInt();
        scanner.nextLine();
        
        Student student = findStudentById(id);
        if (student == null) {
            System.out.println("Student not found!");
            return;
        }
        
        displayStudentInfo(student);
    }
    
    public void displayStudentInfo(Student student) {
        System.out.println("\n========== STUDENT DETAILS ==========");
        System.out.println("Name: " + student.getName());
        System.out.println("ID: " + student.getStudentId());
        System.out.println("Number of Grades: " + student.getGradeCount());
        
        if (student.getGradeCount() > 0) {
            System.out.println("\nGrades by Subject:");
            for (Grade grade : student.getGrades()) {
                System.out.println("  " + grade.toString());
            }
            
            System.out.printf("\nOverall Average: %.2f\n", student.calculateAverage());
            
            Grade highest = student.getHighestGradeWithSubject();
            Grade lowest = student.getLowestGradeWithSubject();
            
            System.out.printf("Highest Grade: %.2f (%s)\n", highest.getScore(), highest.getSubject());
            System.out.printf("Lowest Grade: %.2f (%s)\n", lowest.getScore(), lowest.getSubject());
            System.out.println("Letter Grade: " + student.getLetterGrade());
        } else {
            System.out.println("No grades recorded yet.");
        }
        System.out.println("=====================================");
    }
    
    public void displayAllStudents() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        System.out.println("\n========== ALL STUDENTS SUMMARY ==========");
        System.out.printf("%-5s %-20s %-10s %-10s %-15s %-15s %-5s\n", 
                         "ID", "Name", "Subjects", "Average", "Highest", "Lowest", "Letter");
        System.out.println("=".repeat(90));
        
        for (Student student : students) {
            if (student.getGradeCount() > 0) {
                Grade highest = student.getHighestGradeWithSubject();
                Grade lowest = student.getLowestGradeWithSubject();
                
                System.out.printf("%-5d %-20s %-10d %-10.2f %-15s %-15s %-5s\n",
                                student.getStudentId(),
                                student.getName(),
                                student.getGradeCount(),
                                student.calculateAverage(),
                                highest.getScore() + " (" + highest.getSubject() + ")",
                                lowest.getScore() + " (" + lowest.getSubject() + ")",
                                student.getLetterGrade());
            } else {
                System.out.printf("%-5d %-20s %-10s %-10s %-15s %-15s %-5s\n",
                                student.getStudentId(),
                                student.getName(),
                                "0", "N/A", "N/A", "N/A", "N/A");
            }
        }
        System.out.println("=".repeat(90));
    }
    
    public void searchStudentByName() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        System.out.print("Enter student name to search: ");
        String searchName = scanner.nextLine().toLowerCase();
        
        boolean found = false;
        for (Student student : students) {
            if (student.getName().toLowerCase().contains(searchName)) {
                displayStudentInfo(student);
                found = true;
            }
        }
        
        if (!found) {
            System.out.println("No student found with that name.");
        }
    }
    
    public void viewGradesBySubject() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        System.out.print("Enter subject name to search: ");
        String subject = scanner.nextLine();
        
        System.out.println("\n========== GRADES FOR " + subject.toUpperCase() + " ==========");
        boolean found = false;
        
        for (Student student : students) {
            ArrayList<Grade> subjectGrades = student.getGradesBySubject(subject);
            if (!subjectGrades.isEmpty()) {
                System.out.println("Student: " + student.getName() + " (ID: " + student.getStudentId() + ")");
                for (Grade grade : subjectGrades) {
                    System.out.println("  " + grade.toString());
                }
                System.out.println();
                found = true;
            }
        }
        
        if (!found) {
            System.out.println("No grades found for subject: " + subject);
        }
    }
    
    public void displayClassStatistics() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        int totalStudents = students.size();
        int studentsWithGrades = 0;
        double classTotal = 0;
        double classHighest = 0;
        double classLowest = 100;
        
        for (Student student : students) {
            if (student.getGradeCount() > 0) {
                studentsWithGrades++;
                double avg = student.calculateAverage();
                classTotal += avg;
                
                if (avg > classHighest) classHighest = avg;
                if (avg < classLowest) classLowest = avg;
            }
        }
        
        System.out.println("\n========== CLASS STATISTICS ==========");
        System.out.println("Total Students: " + totalStudents);
        System.out.println("Students with Grades: " + studentsWithGrades);
        
        if (studentsWithGrades > 0) {
            System.out.printf("Class Average: %.2f\n", classTotal / studentsWithGrades);
            System.out.printf("Highest Student Average: %.2f\n", classHighest);
            System.out.printf("Lowest Student Average: %.2f\n", classLowest);
        } else {
            System.out.println("No grades recorded yet.");
        }
        System.out.println("=====================================");
    }
    
    public void removeStudent() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        
        System.out.print("Enter student ID to remove: ");
        int id = scanner.nextInt();
        scanner.nextLine();
        
        Student student = findStudentById(id);
        if (student == null) {
            System.out.println("Student not found!");
            return;
        }
        
        System.out.print("Are you sure you want to remove " + student.getName() + "? (y/n): ");
        String confirm = scanner.nextLine();
        
        if (confirm.toLowerCase().equals("y") || confirm.toLowerCase().equals("yes")) {
            students.remove(student);
            System.out.println("Student removed successfully!");
        } else {
            System.out.println("Operation cancelled.");
        }
    }
    
    public Student findStudentById(int id) {
        for (Student student : students) {
            if (student.getStudentId() == id) {
                return student;
            }
        }
        return null;
    }
    
    public void run() {
        System.out.println("Welcome to Student Grade Tracker!");
        
        while (true) {
            displayMenu();
            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline
            
            switch (choice) {
                case 1:
                    addStudent();
                    break;
                case 2:
                    addGradeToStudent();
                    break;
                case 3:
                    viewStudentDetails();
                    break;
                case 4:
                    displayAllStudents();
                    break;
                case 5:
                    searchStudentByName();
                    break;
                case 6:
                    viewGradesBySubject();
                    break;
                case 7:
                    displayClassStatistics();
                    break;
                case 8:
                    removeStudent();
                    break;
                case 9:
                    System.out.println("Thanks for using Student Grade Tracker!");
                    return;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }
    
    public static void main(String[] args) {
        StudentGradeTracker tracker = new StudentGradeTracker();
        tracker.run();
    }
}
