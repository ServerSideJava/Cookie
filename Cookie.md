import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.*;
import java.io.IOException;

@WebServlet("/login-with-cookie")
public class LoginWithCookieServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        response.setContentType("text/html");
        response.getWriter().println("<html><body>");
        response.getWriter().println("<h1>Login Page</h1>");
        response.getWriter().println("<form method='post' action='/login-with-cookie'>");
        response.getWriter().println("Username: <input type='text' name='username'><br>");
        response.getWriter().println("<input type='submit' value='Login'>");
        response.getWriter().println("</form>");
        response.getWriter().println("</body></html>");
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        String username = request.getParameter("username");

        if (username != null && !username.isEmpty()) {
            // Create a new cookie to store the username
            Cookie usernameCookie = new Cookie("username", username);
            usernameCookie.setMaxAge(3600); // Set the cookie's expiration time (1 hour)

            // Add the cookie to the response
            response.addCookie(usernameCookie);

            response.setContentType("text/html");
            response.getWriter().println("<html><body>");
            response.getWriter().println("<h1>Welcome, " + username + "!</h1>");
            response.getWriter().println("<a href='/logout-with-cookie'>Logout</a>");
            response.getWriter().println("</body></html>");
        } else {
            response.setContentType("text/html");
            response.getWriter().println("<html><body>");
            response.getWriter().println("<h1>Login failed. Please enter a username.</h1>");
            response.getWriter().println("<a href='/login-with-cookie'>Back to Login</a>");
            response.getWriter().println("</body></html>");
        }
    }
}
