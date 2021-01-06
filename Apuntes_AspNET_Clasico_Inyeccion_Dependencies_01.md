# Inyeccion de dependencias en Asp.net Clasico

## Dynamically loading Assemblies to reduce Runtime Dependencies

https://weblog.west-wind.com/posts/2013/Nov/12/Dynamically-loading-Assemblies-to-reduce-Runtime-Dependencies

## Dynamic Module Loading with Autofac

http://old.devkimchi.com/2014/09/25/dynamic-module-loading-with-autofac/

## Dependency injection on the loose - Load different versions of components at runtime

https://dotnetfalcon.com/versioning/

## Dependency Injection with Autofac

https://www.codeproject.com/Articles/25380/Dependency-Injection-with-Autofac

## How to use Dependency Injection (AutoFac) with Repository Pattern in C#

https://www.iditect.com/how-to/52606332.html

## Get All C# Classes Implementing an Interface

https://garywoodfine.com/get-c-classes-implementing-interface/

## Using AutoFac constructor injection in a console application on different classes

https://stackoverflow.com/questions/47002569/using-autofac-constructor-injection-in-a-console-application-on-different-classe


~~~
interface IUserHandler
{
    void PerformSomeAction();
}

class UserHandler : IUserHandler
{
    private IBackupFactory _backupFactory;
    public UserHandler(IBackupFactory backupFactory)
    {
        _backupFactory = backupFactory;
    }

    public void PerformSomeAction()
    {
        var users = _backupFactory.GetFtpUsers();
    }
}

class AutoFacBootstrapper
{
    public static IContainer Init()
    {
        var builder = new ContainerBuilder();

        builder.RegisterType<UserHandler>().As<IUserHandler>();
        builder.RegisterType<BackupFactory>().As<IBackupFactory>();

        return builder.Build();
    }
}
~~~

~~~
 static void Main(string[] args)
    {
        IContainer container = AutoFacBootstrapper.Init();

        IUserHandler startPoint = container.Resolve<IUserHandler>();
        startPoint.PerformSomeAction();
    }
~~~

														