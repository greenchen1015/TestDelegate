# TestDelegate
Test Delegate

```
using System;

namespace TestDelegate
{
	internal class Program
	{
		private static void Main(string[] args)
		{
			Console.WriteLine("Start ... ");

			var service = new TestService();
			service.MailEvent += new TestService.MailEventHandler(Mail);

			service.Execute();

			Console.WriteLine("End ... ");

			Console.ReadLine();
		}

		/// <summary>
		/// Mail事件 .
		/// </summary>
		/// <param name="message">The message.</param>
		private static void Mail(string user, string message)
		{
			Console.WriteLine(string.Format(" Mail to {0}, {1} ", user, message));
		}
	}
}

using System;

namespace TestDelegate
{
	public class TestService
	{
		/// <summary>
		/// 定義委派方法簽章
		/// </summary>
		/// <param name="user">The user.</param>
		/// <param name="message">The message.</param>
		public delegate void MailEventHandler(string user, string message);

		/// <summary>
		/// 實際上用的Event Handler
		/// </summary>
		public event MailEventHandler MailEvent;

		public void Execute()
		{
			Console.WriteLine("Test Service / do something ...");

			// Raise Mail Event.
			this.MailEvent("test mail user", " the mail message ");
			
			Console.WriteLine(" Test Service / continue to do something ...");
		}
	}
}
```

Result:

```
Start ..
Test Service / do something ..
 Mail to test mail user,  the mail message
Test Service / continue to do something ...
End ..
```
