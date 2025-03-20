import java.sql.*;
import java.util.Scanner;

// Model
class Product {
    int productID;
    String productName;
    double price;
    int quantity;
}

// Database Connection Utility
class DatabaseConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/your_database";
    private static final String USER = "root";
    private static final String PASSWORD = "password";

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}

// DAO Class
class ProductDAO {
    public void createProduct(Product product) {
        String sql = "INSERT INTO Product (ProductName, Price, Quantity) VALUES (?, ?, ?)";
        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement stmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)) {
            conn.setAutoCommit(false);
            stmt.setString(1, product.productName);
            stmt.setDouble(2, product.price);
            stmt.setInt(3, product.quantity);
            stmt.executeUpdate();
            conn.commit();
            System.out.println("Product added successfully.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public void readProducts() {
        String sql = "SELECT * FROM Product";
        try (Connection conn = DatabaseConnection.getConnection();
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(sql)) {
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("ProductID") + ", Name: " + rs.getString("ProductName") + ", Price: " + rs.getDouble("Price") + ", Quantity: " + rs.getInt("Quantity"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public void updateProduct(int id, double newPrice, int newQuantity) {
        String sql = "UPDATE Product SET Price = ?, Quantity = ? WHERE ProductID = ?";
        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement stmt = conn.prepareStatement(sql)) {
            conn.setAutoCommit(false);
            stmt.setDouble(1, newPrice);
            stmt.setInt(2, newQuantity);
            stmt.setInt(3, id);
            int rows = stmt.executeUpdate();
            conn.commit();
            if (rows > 0) System.out.println("Product updated successfully.");
            else System.out.println("Product not found.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public void deleteProduct(int id) {
        String sql = "DELETE FROM Product WHERE ProductID = ?";
        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement stmt = conn.prepareStatement(sql)) {
            conn.setAutoCommit(false);
            stmt.setInt(1, id);
            int rows = stmt.executeUpdate();
            conn.commit();
            if (rows > 0) System.out.println("Product deleted successfully.");
            else System.out.println("Product not found.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

// Controller
public class ProductApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ProductDAO dao = new ProductDAO();
        while (true) {
            System.out.println("1. Add Product");
            System.out.println("2. View Products");
            System.out.println("3. Update Product");
            System.out.println("4. Delete Product");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    Product product = new Product();
                    System.out.print("Enter Product Name: ");
                    product.productName = scanner.next();
                    System.out.print("Enter Price: ");
                    product.price = scanner.nextDouble();
                    System.out.print("Enter Quantity: ");
                    product.quantity = scanner.nextInt();
                    dao.createProduct(product);
                    break;
                case 2:
                    dao.readProducts();
                    break;
                case 3:
                    System.out.print("Enter Product ID to update: ");
                    int id = scanner.nextInt();
                    System.out.print("Enter new Price: ");
                    double newPrice = scanner.nextDouble();
                    System.out.print("Enter new Quantity: ");
                    int newQuantity = scanner.nextInt();
                    dao.updateProduct(id, newPrice, newQuantity);
                    break;
                case 4:
                    System.out.print("Enter Product ID to delete: ");
                    int deleteId = scanner.nextInt();
                    dao.deleteProduct(deleteId);
                    break;
                case 5:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }
}
