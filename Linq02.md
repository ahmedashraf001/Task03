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

```

# 1 
1.  **Element Operations**:
    -   Implement a LINQ query to retrieve the first and last element from a collection.
    -   Discuss scenarios where retrieving a single element from a sequence is preferable.
 ```c#
 class Program
	{

		static void Main(string[] args)
		{
			var query01 = Data.emp.FirstOrDefault();
			var query02 = Data.emp.LastOrDefault();

			Console.WriteLine(query01.Name);
			Console.WriteLine(query02.Name);

			Console.ReadLine();
		}
	}
```
# 2
2.  **Equality Operations**:
    -   Write a LINQ query to check if two sequences contain the same elements.
    -   Discuss different approaches to handle equality comparison in LINQ.
 ```c#
 class Program
	{

		static void Main(string[] args)
		{
			List<int> list01 = new  List<int> () { 1, 2, 3, 4, 5, 6, 7 };
			List<int> list02 = new List<int>() { 1, 2, 3, 4, 5, 6, 7 };

			bool equality = list01.SequenceEqual(list02);

			if (equality) { Console.WriteLine("two sequences contain the same elements."); }
			else Console.WriteLine("two sequences don't contain the same elements.");


			Console.ReadLine();
		}
	}
```
# 3
3.  **Concatenation**:
    -   Concatenate two sequences using the LINQ `Concat` method.
    -   Explore scenarios where concatenation is useful, such as combining multiple data sources.
 ```c#
 class Program
	{

		static void Main(string[] args)
		{
			List<int> list01 = new  List<int> () { 1, 2, 3, 4, 5, 6, 7 };
			List<int> list02 = new List<int>() { 1, 2, 3, 4, 5, 6, 7 };

			var contacted = list01.Concat(list02);

			foreach (int item in contacted)
			{
				Console.WriteLine(item);
			}


			Console.ReadLine();
		}
	}
```
# 4
4.  **Aggregate Operations**:
    -   Implement LINQ queries to calculate sum, average, and maximum values from a collection.
    -   Discuss the performance implications of aggregate operations on large datasets.
 ```c#
class Program
	{

		static void Main(string[] args)
		{
			int maxSalary = (from e in Data.emp
							 select e.salary).Max();
			int Count = (from e in Data.emp
						 select e.salary).Count();

			int sum = (from e in Data.emp
					   select e.salary).Sum();



			Console.WriteLine($"Total salaries : {sum} , max salary : {maxSalary} , average salaray : {sum/ Count}");

			Console.ReadLine();
		}
	}
```
# 5
5.  **Sets Operations**:
    -   Perform set operations (union, intersection, difference) on two sequences using LINQ methods.
    -   Discuss scenarios where set operations are beneficial, such as data merging and deduplication.
 ```c#
class Program
	{

		static void Main(string[] args)
		{
			List<int> list01 = new List<int>() { 1, 2, 3, 4 ,5 };
			List<int> list02 = new List<int>() { 4,5,6,7 , 8 };

			var union = list01.Union(list02);
			var intersect = list01.Intersect(list02);
			var difference = list01.Except(list02);

			Console.WriteLine("union:");
			foreach (var item in union)
			{
				Console.WriteLine(item);
			}
			Console.WriteLine("intersect:");
			foreach (var item in intersect)
			{
				Console.WriteLine(item);
			}
			Console.WriteLine("difference:");
			foreach (var item in difference)
			{
				Console.WriteLine(item);
			}





			Console.ReadLine();
		}
	}
```

# 9
9.  **Custom LINQ Extension Methods**:
    -   Create a custom LINQ extension method to filter a collection based on a custom predicate.
    -   Discuss best practices for designing and implementing custom LINQ extension methods.
 ```c#
// Extenstions class:
namespace Linq01
{
	public static class Extensions
	{
        public static IEnumerable<T> Filter<T>(this IEnumerable<T> source, Predicate<T> predicate)
        {
            foreach (var item in source)
            {
                if (predicate(item))
                    yield return item;
            }
        }
    }
}
// Runtime :
namespace Linq01
{
	
	class Program
	{

		static void Main(string[] args)
		{
			List<int> list = new List<int>() { 1, 2, 3, 4, 5, 6, 7,8,9 };

			var query = list.Filter(e => e % 2 == 0);

			foreach(var item in query)
			{
				Console.WriteLine(item);
			}
			 


			Console.ReadLine();
		}
	}
}

```
