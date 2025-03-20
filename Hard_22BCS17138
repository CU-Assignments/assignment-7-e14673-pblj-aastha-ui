import java.sql.*;
import java.util.Scanner;

// Model class for Student
class Student {
    int studentID;
    String name;
    String department;
    double marks;
    
    public Student(int studentID, String name, String department, double marks) {
        this.studentID = studentID;
        this.name = name;
        this.department = department;
        this.marks = marks;
    }
}

// Controller class for database operations
class StudentController {
    private Connection conn;
    
    public StudentController() {
        try {
            String url = "jdbc:mysql://localhost:3306/your_database";
            String user = "your_username";
            String password = "your_password";
            conn = DriverManager.getConnection(url, user, password);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public void addStudent(Student student) {
        String sql = "INSERT INTO Student (StudentID, Name, Department, Marks) VALUES (?, ?, ?, ?)";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setInt(1, student.studentID);
            pstmt.setString(2, student.name);
            pstmt.setString(3, student.department);
            pstmt.setDouble(4, student.marks);
            pstmt.executeUpdate();
            System.out.println("Student added successfully.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public void viewStudents() {
        String sql = "SELECT * FROM Student";
        try (Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(sql)) {
            
            System.out.println("StudentID | Name | Department | Marks");
            while (rs.next()) {
                System.out.println(rs.getInt("StudentID") + " | " + rs.getString("Name") + " | " + rs.getString("Department") + " | " + rs.getDouble("Marks"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public void updateStudent(int studentID, double newMarks) {
        String sql = "UPDATE Student SET Marks = ? WHERE StudentID = ?";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setDouble(1, newMarks);
            pstmt.setInt(2, studentID);
            pstmt.executeUpdate();
            System.out.println("Student marks updated successfully.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public void deleteStudent(int studentID) {
        String sql = "DELETE FROM Student WHERE StudentID = ?";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setInt(1, studentID);
            pstmt.executeUpdate();
            System.out.println("Student deleted successfully.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

// View class for user interaction
public class StudentManagementApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        StudentController controller = new StudentController();
        
        while (true) {
            System.out.println("\nStudent Management System");
            System.out.println("1. Add Student");
            System.out.println("2. View Students");
            System.out.println("3. Update Student Marks");
            System.out.println("4. Delete Student");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    System.out.print("Enter StudentID: ");
                    int id = scanner.nextInt();
                    scanner.nextLine(); 
                    System.out.print("Enter Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter Department: ");
                    String dept = scanner.nextLine();
                    System.out.print("Enter Marks: ");
                    double marks = scanner.nextDouble();
                    controller.addStudent(new Student(id, name, dept, marks));
                    break;
                case 2:
                    controller.viewStudents();
                    break;
                case 3:
                    System.out.print("Enter StudentID: ");
                    int updateId = scanner.nextInt();
                    System.out.print("Enter New Marks: ");
                    double newMarks = scanner.nextDouble();
                    controller.updateStudent(updateId, newMarks);
                    break;
                case 4:
                    System.out.print("Enter StudentID: ");
                    int deleteId = scanner.nextInt();
                    controller.deleteStudent(deleteId);
                    break;
                case 5:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
