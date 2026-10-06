import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import static sun.security.x509.PolicyInformation.ID;

public class Doctors {
    private Connection connection;

    public Doctors(Connection connection) throws SQLException {
        this.connection = connection;
    }


     void addDoctor() {
        System.out.print("Enter Doctor name: ");
        scanner.nextLine(); // Consume the newline left-over from previous input
        String name = scanner.nextLine(); // Read the entire line for the name

    }
        

        System.out.print("Enter Doctor Name: ");
    String gender = scanner.next(); // This could also be nextLine() if gender can have spaces

        try {
        String query = "INSERT INTO Doctor ( ID, name, Specialization) VALUES (?, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(query);
        preparedStatement.setString(1, ID);
        preparedStatement.setString(2, Doctor Name);
        preparedStatement.setString(2, Specialization);

        int affectedRows = preparedStatement.executeUpdate();
        if (affectedRows > 0) {
            System.out.println("Doctor added successfully!");
        } else {
            System.out.println("Failed to add Doctor!");
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
}





public void viewDoctors() {
        String query = "SELECT * FROM doctors";
        try {
            PreparedStatement preparedStatement = connection.prepareStatement(query);
            
            ResultSet resultSet = preparedStatement.executeQuery();
            System.out.println("Doctors:");
            System.out.println("+--------+----------------------+--------------------+");
            System.out.println("|   ID   |      Doctor Name     |   Specialization   |");
            System.out.println("+--------+----------------------+--------------------+");
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                String specialization = resultSet.getString("specialization");
                System.out.printf("|%-8s|%-22s|%-20s|\n", id, name, specialization);                
                System.out.println("+--------+----------------------+--------------------+");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public boolean getDoctorById (int id) {
        String query = "SELECT * FROM doctors WHERE id = ?";
        
        try {
            PreparedStatement preparedStatement = connection.prepareStatement(query);
            preparedStatement.setInt(1, id);

            ResultSet resultSet = preparedStatement.executeQuery();
            if (resultSet.next()) {
                return true;
            } else {
                return false;
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }
}
