---
Titulo: "ASP.NET Core and the Strategy Pattern"
---

# Inyeccion de dependencias en Asp.net Core

ASP.NET Core and the Strategy Pattern

https://adamstorr.azurewebsites.net/blog/aspnetcore-and-the-strategy-pattern


<pre>
services.AddScoped<IMathOperator, AddOperator>();
</pre>

<pre>
public class MathStrategy : IMathStrategy
{
	private readonly IEnumerable<IMathOperator> _operators;

	public MathStrategy(IEnumerable<IMathOperator> operators)
	{
		_operators = operators;
	}

	public int Calculate(int a, int b, Operator op)
	{
		return _operators.FirstOrDefault(x => x.Operator == op)?.Calculate(a, b) ?? throw new ArgumentNullException(nameof(op));
	}
}
</pre>

<pre>
public void ConfigureServices(IServiceCollection services)
{
	** snip not related registrations **

	services.AddScoped<IMathStrategy, MathStrategy>();
	services.AddScoped<IMathOperator, AddOperator>();
	services.AddScoped<IMathOperator, SubtractOperator>();
	services.AddScoped<IMathOperator, MultipleOperator>();
	services.AddScoped<IMathOperator, DivideOperator>();
}
</pre>

<pre>
public enum Operator
{
	Add,
	Substract
}

public interface IMathOperator
{
	Operator Operator { get; }

	int Calculate(int a, int b);
}

public interface IMathStrategy
{
	int Calculate(int a, int b, Operator op);
}
</pre>

<pre>
public class MathStrategy : IMathStrategy
{
	private readonly IMathOperator[] _operators;

	public MathStrategy(IMathOperator[] operators)
	{
		_operators = operators;
	}

	public int Calculate(int a, int b, Operator op)
	{
		return _operators.FirstOrDefault(x => x.Operator == op)?.Calculate(a, b) ?? throw new ArgumentNullException(nameof(op));
	}
}
</pre>

<pre>
public interface IMathStrategyFactory
{
	IMathOperator[] Create();
}
</pre>

<pre>
public class MathStrategyFactory : IMathStrategyFactory
{
	private readonly AddOperator _addOperator;
	private readonly SubtractOperator _subtractOperator;

	public MathStrategyFactory(
		AddOperator addOperator,
		SubtractOperator subtractOperator)
	{
		_addOperator = addOperator;
		_subtractOperator = subtractOperator;
	}

	public IMathOperator[] Create() => new IMathOperator[] { _addOperator, _subtractOperator };
}
</pre>

<pre>
services.AddScoped<AddOperator>();
</pre>

<pre>
services.AddScoped<IMathStrategyFactory, MathStrategyFactory>();
services.AddScoped<IMathOperator[]>(provider =>
{
	var factory = (IMathStrategyFactory)provider.GetService(typeof(IMathStrategyFactory));
	return factory.Create();
});
</pre>


<pre>
public class HomeController : ControllerBase
{
	private readonly IMathStrategy _mathStrategy;

	public HomeController(IMathStrategy mathStrategy)
	{
		_mathStrategy = mathStrategy;
	}

	public IActionResult Index()
	{
		int a = 10;
		int b = 5;
		int result = _mathStrategy.Calculate(a, b, Operator.Add);
		return Content(result.ToString());
	}
}
</pre>





















