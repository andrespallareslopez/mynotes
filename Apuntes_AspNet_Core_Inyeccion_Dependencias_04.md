---
Titulo: "Automatic CQRS handler registration in ASP.NET Core with reflection"
---

# Inyeccion de dependencias en Asp.net Core

Automatic CQRS handler registration in ASP.NET Core with reflection

https://dejanstojanovic.net/aspnet/2019/may/automatic-cqrs-handler-registration-in-aspnet-core-with-reflection/


<pre>
public interface ICommand
{
}
public interface IQuery<TResult>
{
}
public interface ICommandHandler<TCommand> TCommand:ICommand
{
Task HandleAsync(TModel model);
}
public interface IQueryHandler<TQuery,TResult> where TQuery:IQuery<TResult>
    {
        Task<TResult> HandleAsync(TQuery query);
    }
    

</pre>


<pre>

</pre>

<pre>
    public class CreateProductCommand:ICommand
    {
        public Guid Id { get; }
        public String Name { get;  }
        public String Description { get; set; }

        [JsonConstructor]
        public CreateProductCommand(Guid id, String name, String description)
        {
            this.Id = id;
            this.Name = name;
            this.Description = description;
        }
    }
    
</pre>


<pre>
    public class CreateProductHandler : ICommandHandler<CreateProductCommand>
    {
        public async Task HandleAsync(CreateProductCommand command)
        {
			//TODO: Implement command handling logic
            throw new NotImplementedException();
        }
    }
    
</pre>

<pre>
    public class DeleteProductCommand:ICommand
    {
        public Guid Id { get; }

        [JsonConstructor]
        public DeleteProductCommand(Guid id)
        {
            this.Id = id;
        }
    }
	
	public class DeleteProductHandler : ICommandHandler<DeleteProductCommand>
    {
        public Task HandleAsync(DeleteProductCommand model)
        {
            throw new NotImplementedException();
        }
    }

</pre>


<pre>
    public class ProductView
    {
        public Guid Id { get; set; }
        public String Name { get; set; }
        public String Description { get; set; }
    }
</pre>

<pre>
    public class ProductBrowseQuery:IQuery<IEnumerable<ProductView>>
    {
        public Guid Id { get; set; }
        public String Name { get; set; }
        public int PageIndex { get; set; }
        public int PageSize { get; set; }
    }
    
</pre>

<pre>
   public class BrowseProductHandler : IQueryHandler<ProductBrowseQuery, IEnumerable<ProductView>>
    {
        public async Task<IEnumerable<ProductView>> HandleAsync(ProductBrowseQuery query)
        {
			//TODO: Hanlde query and return result
			throw new NotImplementedException();
        }
    }
    
</pre>

<pre>
    public class ProductGetQuery:IQuery<ProductView>
    {
        public Guid Id { get; set; }
    }

    public class GetProductHandler : IQueryHandler<ProductGetQuery, ProductView>
    {
        public async Task<ProductView> HandleAsync(ProductGetQuery query)
        {
			//TODO: Handle query and return result
			throw new NotImplementedException();
        }
    }
    
</pre>

**Dependency injection**

<pre>
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddScoped<ICommandHandler<CreateProductCommand>, CreateProductHandler>();
            services.AddScoped<ICommandHandler<DeleteProductCommand>, DeleteProductHandler>();
            services.AddScoped<IQueryHandler<ProductBrowseQuery, IEnumerable<ProductView>>, BrowseProductHandler>();
            services.AddScoped<IQueryHandler<ProductGetQuery, ProductView>, GetProductHandler>();
		}
    
</pre>

<pre>
        public void ConfigureServices(IServiceCollection services)
        {
			var commandHandlers = typeof(Startup).Assembly.GetTypes()
                .Where(t => t.GetInterfaces().Any(i a=> i.IsGenericType && i.GetGenericTypeDefinition() == typeof(ICommandHandler<>))
            );

            foreach (var handler in commandHandlers)
            {
                services.AddScoped(handler.GetInterfaces().First(i => i.IsGenericType && i.GetGenericTypeDefinition() == typeof(ICommandHandler<>)), handler);
            }
		}
</pre>

<pre>
        public void ConfigureServices(IServiceCollection services)
        {
			var queryHandlers = typeof(Startup).Assembly.GetTypes()
                .Where(t => t.GetInterfaces().Any(i => i.IsGenericType && i.GetGenericTypeDefinition() == typeof(IQueryHandler<,>))
            );

            foreach (var handler in queryHandlers)
            {
                services.AddScoped(handler.GetInterfaces().First(i => i.IsGenericType && i.GetGenericTypeDefinition() == typeof(IQueryHandler<,>)), handler);
            }
		}
    
</pre>

<pre>
        private static void AddCommandQueryHandlers(this IServiceCollection services, Type handlerInterface)
        {
            var handlers = typeof(ServiceExtensions).Assembly.GetTypes()
                .Where(t => t.GetInterfaces().Any(i => i.IsGenericType && i.GetGenericTypeDefinition() == handlerInterface)
            );

            foreach (var handler in handlers)
            {
                services.AddScoped(handler.GetInterfaces().First(i => i.IsGenericType && i.GetGenericTypeDefinition() == handlerInterface), handler);
            }
        }
    
</pre>

<pre>
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddCommandQueryHandlers(typeof(ICommandHandler<>));
            services.AddCommandQueryHandlers(typeof(IQueryHandler<,>));
		}
    
</pre>
















