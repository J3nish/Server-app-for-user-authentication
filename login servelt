package com.mycompany.practical_4;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(name = "login", urlPatterns = {"/login"})
public class login extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");

        try (PrintWriter out = response.getWriter()) {
            // Load MySQL Driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Establish Connection
            Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/jdbc", "root", "");

            // Prepare SQL Statement
            String sql = "SELECT * FROM login WHERE username = ? AND password = ?";
            PreparedStatement pstmt = conn.prepareStatement(sql);

            // Get parameters and set them
            pstmt.setString(1, request.getParameter("username"));
            pstmt.setString(2, request.getParameter("password"));

            // Execute query
            ResultSet rs = pstmt.executeQuery();

            out.println("<html><body>");
            if (rs.next()) {
                out.println("<h3>Login Successful!</h3>");
            } else {
                out.println("<h3>Invalid Credentials, Try Again.</h3>");
            }
            out.println("</body></html>");

            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
