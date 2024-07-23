1.  **Understanding Pure & Impure Functions**:
    -   Write a pure function that filters a list of integers using LINQ.
    -   Implement an impure function that modifies a global variable.
# 1-1 

```c#
class Program
	{

		static void Main(string[] args)
		{

			List<int> list = new List<int>()  { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

			var evenNumbers = list.Where(num => num % 2==0);

			foreach (var item in evenNumbers)
			{
				Console.WriteLine(item);
			}

			
			Console.ReadLine();
		}
	}
```
# 1-2 
```c#
class Program
	{
		public static List<int> list = new List<int>() { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
		static void Main(string[] args)
		{

			

			var query = list.Select(num => num +=2);

			foreach (var item in query)
			{
				Console.WriteLine(item);
			}

			 
			
			Console.ReadLine();
		}
	}
```	

2.  **Functional Programming in LINQ**:
    -   Rewrite an existing LINQ query using a functional programming approach.
    -   Discuss the benefits and drawbacks of the functional approach.
# 2-1
```c#

class Program
	{

		static void Main(string[] args)
		{

			List<int> list = new List<int>()  { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

			var oddNumbers = from num in list
				             where num%2==1
			     	         select num;

			var oddNums = list.Where(num => num % 2==1);

			foreach (var item in oddNumbers)
			{
				Console.WriteLine(item);
			}
			Console.WriteLine("******************");
			foreach (var item in oddNums)
			{
				Console.WriteLine(item);
			}


			Console.ReadLine();
		}
	}
`````
# 3

3.  **Projection Operation**:
    -   Create a LINQ query to project specific properties of objects in a collection.
    -   Apply a projection operation to format data for display in a UI.	
	
	```c#
     // Classes
	public class Person
	{
		public string Name { get; set; }
		public int Age { get; set; }
		public string hoppy{ get; set; }
	}

	//Data
	public static class Data
	{
		public static Person[] people = 
		{
			new Person { Name = "Ahmed", Age = 20, hoppy = "fishing" },
			new Person { Name = "mohamed", Age = 22, hoppy = "tennis" },
			new Person { Name = "omar", Age = 28, hoppy = "reading" }
		};
	}

	//Runtime
	class Program
	{

		static void Main(string[] args)
		{

			var query = from person in Data.people
						select new { Name=  person.Name  , Hoppy = person.hoppy };
		

			foreach (var item in query)
			{
				Console.WriteLine(item);
			}
			


			Console.ReadLine();
		}
	}
``
# 4
4.  **Sorting Data**:
    -   Implement sorting of a list of objects based on different properties using LINQ.
    -   Compare the performance of LINQ sorting methods for large datasets.
	
	```c#
	var query = from person in Data.people
						orderby person.Age , person.Name descending
						select person;
		

			foreach (var item in query)
			{
				Console.WriteLine(item.Age);
			}
	```
 # 6
6.  **Quantifiers**:
   -   Use quantifiers to check if all elements in a list satisfy a condition.
-   Apply quantifiers to find if any element in a list meets a specific criteria.

	```c#
    // Classes
	public class Person
	{
		public string Name { get; set; }
		public int Age { get; set; }
		public string hoppy{ get; set; }
	}

	//Data
	public static class Data
	{
		public static Person[] people = 
		{
			new Person { Name = "Ahmed", Age = 20, hoppy = "fishing" },
			new Person { Name = "mohamed", Age = 22, hoppy = "tennis" },
			new Person { Name = "omar", Age = 28, hoppy = "reading" },
			new Person { Name = "mazen", Age = 80, hoppy = "reading" }
		};
	}

	//Runtime
	class Program
	{

		static void Main(string[] args)
		{
			bool Allyoung = Data.people.All(p => p.Age <30);
			if (Allyoung) { Console.WriteLine("All persons are young"); }
			else { Console.WriteLine("not All persons are young"); }

			bool OLDman = Data.people.Any(p => p.Age > 60);
			if (OLDman) { Console.WriteLine("there is an old man on the plane"); }
			else { Console.WriteLine("there is no old Man"); }
			


			Console.ReadLine();
		}	
``
# 7
7.  **Grouping Data**:
    -   Group a collection of objects by a common property using LINQ.
    -   Calculate aggregate functions (e.g., sum, average) on grouped data. 

   	```c#
     // Classes
	public class employee
	{
		public string Name { get; set; }
		public string deptName { get; set; }
		public int salary{ get; set; }
	}

	//Data
	public static class Data
	{
		public static employee[] emp = 
		{
			new employee { Name = "Ahmed", deptName = "SWE" , salary = 50000 },
			new employee { Name = "omar", deptName = "MPE" , salary = 90000 },
			new employee { Name = "mohamed", deptName = "CSE" , salary = 80000 },
			new employee { Name = "mazen", deptName = "MPE" , salary = 70000 },
			new employee { Name = "ebrahim", deptName = "CSE" , salary = 30000 },
			new employee { Name = "fady", deptName = "SWE" , salary = 40000 },
			new employee { Name = "osama", deptName = "IT" , salary = 50000 },
			new employee { Name = "samir", deptName = "IT" , salary = 60000 },
		};
	}

	//Runtime
	class Program
	{

		static void Main(string[] args)
		{
			var query = from emp in Data.emp
						group emp by emp.deptName;


			foreach(var grp in query)
			{
				Console.WriteLine($"dept Name : {grp.Key}");
				int sum = grp.Sum(g => g.salary);
				int count = grp.Count();
				Console.WriteLine($"Total salaries : {sum}");
				Console.WriteLine($"average salary : {sum/count}");
				Console.WriteLine("----------------------------------------");
			}
			
						  

			


			Console.ReadLine();
		}
	}
   ``
# 8
8.  **Join Operations**:
    -   Perform an inner join between two collections of objects using LINQ.
    -   Implement a left join operation and handle null values in the result.

   	```c#
   	// Classes
	public class employee
	{
		public string Name { get; set; }
		public string deptName { get; set; }
		public int salary{ get; set; }
	}
	public class Department
	{
		public string deptName { get; set; }
		public string manager { get; set; }
	}


	//Data
	public static class Data
	{
		public static employee[] emp = 
		{
			new employee { Name = "Ahmed", deptName = "SWE" , salary = 50000 },
			new employee { Name = "omar", deptName = "MPE" , salary = 90000 },
			new employee { Name = "mohamed", deptName = "CSE" , salary = 80000 },
			new employee { Name = "mazen", deptName = "MPE" , salary = 70000 },
			new employee { Name = "ebrahim", deptName = "CSE" , salary = 30000 },
			new employee { Name = "fady", deptName = "SWE" , salary = 40000 },
			new employee { Name = "osama", deptName = "IT" , salary = 50000 },
			new employee { Name = "samir", deptName = "IT" , salary = 60000 },
		};

		public static Department[] dept =
		{
			new Department {  deptName = "SWE" , manager = "ahmed" },
			new Department {  deptName = "CSE" , manager = "hassan" },
			new Department {  deptName = "IT" , manager = "nabil" },
			new Department {  deptName = "MPE" , manager = "sayed" },

		};
	}

 
	//Runtime
	class Program
	{

		static void Main(string[] args)
		{
			var query = from emp in Data.emp
						join dept in Data.dept on emp.deptName equals dept.deptName
						group emp by new { dept.deptName, dept.manager } into g
						select new { manager = g.Key.manager,
								    Department = g.Key.deptName,
						         	Employees = g
						   };

			foreach(var g in query)
			{
				Console.WriteLine($"manager : {g.manager} , Department : {g.Department}");
				foreach(var itr in g.Employees)
				{
					Console.WriteLine($"Emp Name : {itr.Name} ,  Emp Salary : {itr.salary} ");
				}
				Console.WriteLine("-------------------------------------");
			}


			 
						  

			


			Console.ReadLine();
		}
	
