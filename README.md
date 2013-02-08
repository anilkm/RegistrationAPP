RegistrationAPP
//Application using JavaEE by which user can register and login.
........................................LogIn......................................
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.lang.*;
import java.sql.*;
public class LogInServlet extends HttpServlet
{
private Connection conn;
private PreparedStatement ps;
public void init() throws ServletException
{
ServletContext sc=super.getServletContext();
String driverclass=sc.getInitParameter("driverclass");
String connstring=sc.getInitParameter("connstr");
String dbuser=sc.getInitParameter("dbuser");
String dbpass=sc.getInitParameter("dbpass");
try
{Class.forName(driverclass);
}
catch(ClassNotFoundException cnf)
{
System.out.println("cann't find the driver class");
throw new ServletException("Error:"+cnf);
}
try
{
conn=DriverManager.getConnection(connstring,dbuser,dbpass);
ServletConfig cfg=super.getServletConfig();
String qry=cfg.getInitParameter("qry");
ps=conn.prepareStatement(qry);
}
catch(SQLException sq)
{
System.out.println("Sql Error:"+sq);
throw new ServletException("sql error2:"+sq);
}
}
public void doPost(HttpServletRequest req,HttpServletResponse resp) throws ServletException,IOException
{
resp.setContentType("text/html");
PrintWriter pw=resp.getWriter();
String username=req.getParameter("username");
String password=req.getParameter("password");
if(username.equals("")||password.equals(""))
pw.println("<b>Cann't leave username or password blank</b>");
else
{
try
{
ps.setString(1,username);
ps.setString(2,password);
ResultSet rs=ps.executeQuery();
if(rs.next())
{
pw.println("<b><center>Welcome "+username+" To My Page</center></b>");
}
else
{
pw.println("<b>You aren't registered</b>");
pw.println("<br><a href='home2.html'>Try Again</a>");
pw.println("<br><b>OR</b>");
pw.println("<br><a href='register.html'>Register Yourself</a>");
}
}
catch(SQLException sq)
{
System.out.println("Sql Error: from try");
throw new ServletException("sql error:"+sq);
}
}
pw.close();
}
}

...........................................Registration.............................
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;
public class RegistrationServlet extends HttpServlet
{
private Connection conn;
private PreparedStatement ps;
public void init() throws ServletException
{
ServletContext sc=super.getServletContext();
String driverclass=sc.getInitParameter("driverclass");
String connstring=sc.getInitParameter("connstr");
String dbuser=sc.getInitParameter("dbuser");
String dbpass=sc.getInitParameter("dbpass");
try
{Class.forName(driverclass);
}
catch(ClassNotFoundException cnf)
{
System.out.println("cann't find the driver class");
throw new ServletException("Error:"+cnf);
}
try
{
conn=DriverManager.getConnection(connstring,dbuser,dbpass);
ServletConfig cfg=super.getServletConfig();
String qry2=cfg.getInitParameter("qry2");
ps=conn.prepareStatement(qry2);
}
catch(SQLException sq)
{
System.out.println("Sql Error:"+sq);
throw new ServletException("sql error2:"+sq);
}
}
public void doPost(HttpServletRequest req,HttpServletResponse resp)throws ServletException,IOException
{
resp.setContentType("text/html");
PrintWriter pw=resp.getWriter();
String username=req.getParameter("username");
String password=req.getParameter("password");
if(username.equals("")||password.equals(""))
pw.println("<b>Cann't leave username or password blank</b>");
else
{
try
{
ps.setString(1,username);
ps.setString(2,password);
ps.executeUpdate();
pw.println("<b>Thanx For Registration Now <a href='home.html'>LogIn</a></b>");

}
catch(SQLException sq)
{
System.out.println("Sql Error:");
pw.println("<html><body>");
pw.println("<b><center>");
pw.println("Username Not Available");
pw.println("</b></center>");
pw.println("<center><a href='register.html'>BACK</a></center>");
pw.println("</body>");
pw.println("</html>");
//throw new ServletException("Sql error:"+sq);
}
}
pw.close();
}
}


.........................Registration Form in html....................................
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <meta http-equiv="content-type" content="text/html;
      charset=ISO-8859-1">
    <title></title>
  </head>
  <body style=" background-color: White;">
    &nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <br>
    <table style=" text-align: left; width: 1300px; height: 34px;
      background-color: rgb(255, 255, 204);" border="0" cellpadding="2"
      cellspacing="2">
      <tbody>
        <tr>
          <td style=" vertical-align: top;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;


            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; <span
              style="COLOR:RED;FONT-SIZE:20PT;">
              STUDENT&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
              REGISTRATION&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FORM</span><br>
          </td>
        </tr>
      </tbody>
    </table>
    <br>
    <br>
    <table style="width: 1342px; height: 391px;" bgcolor="#002e63">
      <tbody>
          
  	  <tr><td><span style="color:white; font-size:16pt;">USERNAME:&nbsp;</span><input type="text" id="tname"size="43"></td><td><span style="color:white;font-size:16pt;">PASSWORD:&nbsp;</span><input type="text" id="tname"size="43"></td></tr>
		  <tr><td><span style="color:white; font-size:16pt;">FIRST NAME:&nbsp;</span><input type="text" id="tname"size="43"></td><td><span style="color:white;font-size:16pt;">FATHER'S NAME:&nbsp;</span><input type="text" id="tname"size="43"></td></tr>
		  <td><span style="color:white; font-size:16pt;">LAST NAME:&nbsp;</span><input type="text" id="tname"size="43"></td><td><span style="color:white;font-size:16pt;">&nbsp;SCHOLAR NO:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><input type="text" id="tname"size="43"></td></tr>
		  <tr><td><span style="color:white;font-size:16pt;">BRANCH:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><select><option>Computer Science Engineering</option><option>Civil Engineering</option><option>Electrical Engineering</option><option>Electronics and Communication Engineering</option></td><td><span style="color:white;font-size:16pt;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SEM:&nbsp;</span><select><option>I</option><option>II</option><option>III</option><option>IV</option><option>V</option><option>VI</option><option>VII</option><option>VIII</option></td></tr>
		  <tr><td><span style="color:white;font-size:16pt;">GENDER:&nbsp;</span><select><option>Male</option><option>Female</option><td><span style="color:white;font-size:16pt;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;COURSE:&nbsp;</span><select><option>B.Tech</option><option>M.Tech</option><option>Phd</option><option>MCA</option></td></td></tr>
		  
      </tbody>
    </table></br></br>
	<table style=" text-align: left; width: 1300px; height: 34px;
      background-color: rgb(255, 255, 204);" border="0" cellpadding="2"
      cellspacing="2">
      <tbody>
        <tr>
          <td style=" vertical-align: top;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;


            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
            &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; <span
              style="COLOR:RED;FONT-SIZE:20PT;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<input type="submit" value="SUBMIT">
              </span><br>
          </td>
        </tr>
      </tbody>
    </table>
  </body>
</html>


...................................................Login Page.........................................
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>

    <meta http-equiv="content-type" content="text/html; charset=ISO-8859-1">
    <title>home</title>
  </head>
  <body align="center" bgcolor="#FF999">
    <form action="LogInServlet" method="post">
      <table align="center">
        <tbody>
          <tr>
            <td style="vertical-align: top;"><br>
              <br>
              <br>
              <br>
              <br>
              <br>
              <br>
              <br>
              <br>
              <br>
              &nbsp; <br>
            </td>
            <td style="vertical-align: top;"><br>
            </td>
          </tr>
          <tr>
            <th>
              <table align="center">
                <tbody>
                  <tr>
                    <th>Uername<br>
                    </th>
                  </tr>
                </tbody>
              </table>
            </th>
            <td>
              <input maxlength="20" name="username">
            </td>
          </tr>
          <tr>
            <th>
              <table align="center">
                <tbody>
                  <tr>
                    <th>password</th>
                  </tr>
                </tbody>
              </table>
            </th>
            <td>
              <input maxlength="20" name="password" type="password">
            </td>
          </tr>
          <tr>
            <td>
              <table align="center">
                <tbody>
                  <tr>
                    <th><br>
                    </th>
                    <th><br>
                    </th>
                  </tr>
                </tbody>
              </table>
            </td>
            <td>
              <br>
            </td>
            <td>
              <input value="Login" type="submit">
              <input value="Reset" type="reset">
            </td>
          </tr>
        </tbody>
      </table>
    </form>
  </body>
</html>







