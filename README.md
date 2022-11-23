	# urlshortener
	import java.sql.*;

	Connection con;

	class tinyShortner
	{
		long count = 0;

		void ADD(String url)
		{
			Statement stmt = con.createStatement();
			String shortURL = "tinyurl"+count;
			count++;
			String q1 = "insert into URLSHORTNER values('" +url+ "', '" +shortURL+"')";
		int x = stmt.executeUpdate(q1);
		if (x > 0)           
		    System.out.println("SHORT URL Successfully created");           
		else           
		    System.out.println("creation of SHORT URL failed");
		}

		String get(String url)
		{
			Statement stmt = con.createStatement();
			String q1 = "select * from URLSHORTNER WHERE url = '" + url + "'";
		ResultSet rs = stmt.executeQuery(q1);

		if (rs.next())
		    return rs.getString(2);
		else
		    return "No such short url present for the given url";
		}

		void delete(String url)
		{
			Statement stmt = con.createStatement();
			String q1 = "DELETE from URLSHORTNER WHERE url = '" + url + "'";
		int x = stmt.executeUpdate(q1);

		if (x > 0)           
		    System.out.println("Successfully Deleted");           
		else
		    System.out.println("NOT Deleted"); 
		}
	}

	public class Project
	{
		public static void main(String[] args) 
		{
			Class.forName("org.sqlite.JDBC");
		con = DriverManager.getConnection("jdbc:sqlite:C://sqlite//URLSHORTNER.db");

			while(True)
			{
				System.out.println("1.ADD URL");
				System.out.println("2.DELETE URL");
				System.out.println("3.GET URL");
				System.out.println("3.EXIT");
				System.out.print("Enter your choice :");
				System.out.println();
				int op = sc.nextInt();

				switch(op)
				{
					case 1:
					{
						String url = sc.next();
						ADD(url);
						break;
					}
					case 2:
					{
						String url = sc.next();
						delete(url);
						break;
					}
					case 3:
					{
						String url = sc.next();
						System.out.println(get(url));
						break;
					}
					default
						return;
				}
			}
		}
	}
