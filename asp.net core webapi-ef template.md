---
Titulo: "Comandos dotnet CLI"
---

# Template Asp.net Core with WebApi and EntityFramework

**Comandos dotnet CLI**


Agregar referencias de proyecto:

<pre>
dotnet add app/app.csproj reference lib/lib.csproj

dotnet add reference lib1/lib1.csproj lib2/lib2.csproj

Agrega variass referencias de proyecto  usando el patron global en linux:
dotnet add app/app.csproj reference **/*.csproj
</pre>

Para ado.net en .net 3.0:

<pre>
dotnet add package Microsoft.Data.SqlClient --version 1.0.19221.1-Preview
</pre>

**Pasos para crear nuesstro proyecto**

<pre>
dotnet new sln -n Empresarios

dotnet new webapi -n Empresarios.Api

dotnet sln list

dotnet sln add Empresarios.Api\Empresarios.Api

dotnet sln add Empresarios.EF\Empresarios.EF

</pre>

Tendriamos que crear una libreria con dotnet:

<pre>
dotnet new classlib -n Empresarios.EF
</pre>

Y luego añadimos los paquetes para usar entity framework en esta libreria de <code>Empresarios.EF</code>

<pre>
dotnet add package Microsoft.EntityFrameworkCore.SqlServer

dotnet add package Microsoft.EntityFrameworkCore.Tools.DotNet



</pre>
Añadimos el tag <code>DotNetCliToolReference</code> en el fichero de solucion que aparece abajo y ya estamos listos para utilizar el comando <code>dotnet ef</code>

<textarea cols=70 rows=15>
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="2.0.0" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="2.0.0" />
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0" />
  </ItemGroup>
</Project>

</textarea>

En *dotnet CLI* podemos utilizar el comando siguiente:
<pre>
dotnet ef dbcontext scaffold "Server=.\SQLEXPRESS;Database=SchoolDB;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Models 
</pre>
Y nos generaria un scaffolding de los modelos en una carpeta Models, todo este codigo es importado y creado desde una base de datos, veriamos tambien una clase DBContext tambien.


Luego necesitamos utilizar una clase dbcontext como la siguiente:

<pre>
public class EmpresariosContext : DbContext
{
    public SchoolContext()
    {
  
    }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
         optionsBuilder.UseSqlServer(@"Server=.\SQLEXPRESS;Database=SchoolDB;Trusted_Connection=True;");
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
    }
    //entities
    public DbSet<Student> Students { get; set; }
    public DbSet<Course> Courses { get; set; }
} 
</pre>

Podemos añadir migraciones como sigue a partir de un modelo de clases (Code First).

<pre>
 dotnet ef migrations add EmpresariosDB

 dotnet ef database update
</pre>

Luego podemos escribir y leer dedatos de la siguiente manera:

<pre>
namespace EFCoreTutorials
{
    class Program
    {
        static void Main(string[] args)
        {
            using (var context = new EmpresariosContext()) {

                var std = new Student()
                {
                     Name = "Bill"
                };

                context.Students.Add(std);
                context.SaveChanges();
            }
        }
    }
}
</pre>
Podemos hacer consultas como las siguientes:

<pre>
private static void Main(string[] args)
{
    var context = new SchoolContext();
    var studentsWithSameName = context.Students
                                      .Where(s => s.FirstName == GetName())
                                      .ToList();
}

public static string GetName() {
    return "Bill";
}
</pre>
Tenemos tambien Eager Loading con <code>Include()</code> :

<pre>
var context = new SchoolContext();

var studentWithGrade = context.Students
                           .Where(s => s.FirstName == "Bill")
                           .Include(s => s.Grade)
                           .FirstOrDefault();
</pre>

El metodo include tambien se puede hacer desde FromSql

<pre>
var context = new SchoolContext();

var studentWithGrade = context.Students
                        .FromSql("Select * from Students where FirstName ='Bill'")
                        .Include(s => s.Grade)
                        .FirstOrDefault();        
</pre>

Se pueden hacer multiple include:

<pre>
var context = new SchoolContext();

var studentWithGrade = context.Students.Where(s => s.FirstName == "Bill")
                        .Include(s => s.Grade)
                        .Include(s => s.StudentCourses)
                        .FirstOrDefault();
</pre>

ThenInclude()

<pre>
var context = new SchoolContext();

var student = context.Students.Where(s => s.FirstName == "Bill")
                        .Include(s => s.Grade)
                            .ThenInclude(g => g.Teachers)
                        .FirstOrDefault();
</pre>

Projection Query

<pre>
var context = new SchoolContext();

var stud = context.Students.Where(s => s.FirstName == "Bill")
                        .Select(s => new
                        {
                            Student = s,
                            Grade = s.Grade,
                            GradeTeachers = s.Grade.Teachers
                        })
                        .FirstOrDefault();
</pre>


Lazy loading is not supported in Entity Framework Core 2.0

Entity Framework tiene dos escenarios a la hora de guardar los datos: Conectado y Desconectado.

Insert Data

<pre>
using (var context = new SchoolContext())
{
    var std = new Student()
    {
        FirstName = "Bill",
        LastName = "Gates"
    };
    context.Students.Add(std);

    // or
    // context.Add<Student>(std);

    context.SaveChanges();
}
</pre>

Updating data

<pre>
using (var context = new SchoolContext())
{
    var std = context.Students.First<Student>(); 
    std.FirstName = "Steve";
    context.SaveChanges();
}
</pre>
Deleting Data

<pre>
using (var context = new SchoolContext())
{
    var std = context.Students.First<Student>();
    context.Students.Remove(std);

    // or
    // context.Remove<Student>(std);

    context.SaveChanges();
}
</pre>

