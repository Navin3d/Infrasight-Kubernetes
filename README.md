# Infrasight-Kubernetes
This is an Kubernetes version of Infrasight.

kubectl proxy:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

```bash
kubectl -n kubernetes-dashboard create token admin-user
```
archetype:generate -DgroupId=com.example -DartifactId=my-maven-plugin -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

```
package com.training;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class DepartmentDao {

	public List<Department> getAllDepartment() {
		List<Department> departments = new ArrayList<>();
		Statement st = null;
		Connection con = null;
		try {
			Class.forName("com.mysql.jdbc.Driver");
		    con = DriverManager.getConnection("jdbc:mysql://localhost:3306/training", "root", "root");
			st = con.createStatement();
			ResultSet rs = st.executeQuery("SELECT * from DEPARTMENTS");

			while (rs.next()) {
				Department obj = new Department();
				obj.setDepartmentId(rs.getInt(1));
				obj.setDepartmentName(rs.getString(2));
				obj.setCreatedBy(rs.getString(3));
				departments.add(obj);
			}

		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				st.close();
				con.close();
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

		return departments;
	}

	public void addDepartment(Department department) {

		try {
			Class.forName("com.mysql.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/training", "root", "root");
			PreparedStatement ps = con
					.prepareStatement("INSERT INTO DEPARTMENTS(DEPARTMENT_NAME,CREATED_BY) VALUES (?,?)");
			ps.setString(1, department.getDepartmentName());
			ps.setString(2, department.getCreatedBy());
			int rows = ps.executeUpdate();
			System.out.println(rows + " rows inserted");

		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}

	public void updateDepartment(String createdBy, int departmentId) {

		PreparedStatement st = null;
		int count = 0;
		Connection con = null;
		String query = "UPDATE DEPARTMENTS SET CREATED_BY = ? WHERE DEPARTMENT_ID = ? ";

		try {
			Class.forName("com.mysql.jdbc.Driver");
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/training", "root", "root");
			st = con.prepareStatement(query);
			st.setString(1, createdBy);
			st.setInt(2, departmentId);
			count = st.executeUpdate();
			System.out.println(count + " record is updated successfully");

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				st.close();
				con.close();
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}

		}

	}

	public void deleteDepartment(int departmentId) {

		PreparedStatement st = null;
		int count = 0;
		Connection con = null;
		String query = "DELETE FROM DEPARTMENTS  WHERE DEPARTMENT_ID = ? ";

		try {
			Class.forName("com.mysql.jdbc.Driver");
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/training", "root", "root");
			st = con.prepareStatement(query);
			st.setInt(1, departmentId);
			count = st.executeUpdate();
			System.out.println(count + " record is deleted successfully");

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				st.close();
				con.close();
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}

		}

	}

}

try (Connection connection = DriverManager.getConnection(JDBC_URL, USERNAME, PASSWORD)) {
            // Perform database operations here
            String sql = "SELECT * FROM your_table";
            try (PreparedStatement statement = connection.prepareStatement(sql);
                 ResultSet resultSet = statement.executeQuery()) {
                while (resultSet.next()) {
                    // Process the ResultSet as needed
                    // Example: String value = resultSet.getString("column_name");
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }


private static void readSqlFiles(String folderPath) {
        File folder = new File(folderPath);

        // Check if the path is a directory
        if (folder.isDirectory()) {
            File[] files = folder.listFiles();

            // Iterate over files and subdirectories
            if (files != null) {
                for (File file : files) {
                    if (file.isDirectory()) {
                        // Recursively call the method for nested folders
                        readSqlFiles(file.getAbsolutePath());
                    } else if (file.getName().toLowerCase().endsWith(".sql")) {
                        // Read and print the content of SQL files
                        try {
                            String content = new String(Files.readAllBytes(Paths.get(file.getAbsolutePath())));
                            System.out.println("File: " + file.getAbsolutePath());
                            System.out.println("Content:\n" + content);
                            System.out.println("---------------------------------------------");
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        } else {
            System.out.println("Invalid folder path: " + folderPath);
        }
    }

public static boolean containsWordInList(String inputString, List<String> wordList) {
        for (String word : wordList) {
            if (inputString.contains(word)) {
                return true;
            }
        }
        return false;
    }
```
