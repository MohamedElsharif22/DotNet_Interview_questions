# Backend .NET Interview Questions

## دليل الأسئلة والأجوبة - Dot NET Development

---

## 📊 أولاً: Databases و SQL

### ما الفرق بين Stored Procedure و Function ومتى تستخدم كل منهما؟

**Stored Procedure:**

- يمكن أن يحتوي على DML operations (INSERT, UPDATE, DELETE)
- يمكن أن يرجع أكثر من قيمة أو لا يرجع شيء
- يمكن استخدام OUTPUT parameters
- لا يمكن استخدامه في SELECT statement
- يستخدم لتنفيذ العمليات المعقدة والمنطق التجاري

**Function:**

- يجب أن يرجع قيمة واحدة
- لا يمكن أن يحتوي على DML operations
- يمكن استخدامه في SELECT statement
- يستخدم للحسابات والتحويلات

### ما الفرق بين View و Stored Procedure و Function؟

**View:**

- جدول افتراضي يحتوي على نتيجة SELECT statement
- يتم تحديثه تلقائياً عند تغيير البيانات الأساسية
- يستخدم لتبسيط الاستعلامات المعقدة وإخفاء التعقيد

**Stored Procedure:**

- مجموعة من الأوامر المحفوظة في قاعدة البيانات
- يمكن أن يحتوي على parameters ومنطق معقد
- يتم تجميعه مرة واحدة ويحسن الأداء

**Function:**

- يرجع قيمة واحدة ويمكن استخدامه في الاستعلامات
- نوعان: Scalar Functions و Table-valued Functions

### هل التعديل في الـ View يؤثر على البيانات الحقيقية؟

نعم، في بعض الحالات يمكن أن يؤثر التعديل في View على البيانات الأساسية، ولكن هناك شروط:

- View يجب أن يكون مبني على جدول واحد
- لا يحتوي على GROUP BY, HAVING, DISTINCT, TOP
- لا يحتوي على calculated columns أو functions
- يجب أن تتضمن جميع الـ NOT NULL columns في INSERT

### ما هو الـ Trigger وما أنواعه؟

**Trigger:** هو stored procedure خاص يتم تنفيذه تلقائياً عند حدوث event معين على الجدول.

**الأنواع حسب التوقيت:**

- **AFTER Trigger:** يتم تنفيذه بعد العملية (الأكثر شيوعاً)
- **INSTEAD OF Trigger:** يحل محل العملية (يستخدم مع Views)

**الأنواع حسب العملية:**

- INSERT Trigger
- UPDATE Trigger
- DELETE Trigger

### ما هو الـ Index وما أنواعه؟

**Index:** هيكل بيانات يحسن سرعة البحث والاستعلام في الجداول عن طريق إنشاء مؤشرات للصفوف.

**الأنواع:**

- **Clustered Index:** يرتب البيانات فيزيائياً حسب مفتاح الفهرس، جدول واحد يحتوي على clustered index واحد فقط
- **Non-Clustered Index:** لا يؤثر على ترتيب البيانات الفيزيائي، يمكن وجود 999 منه في الجدول الواحد

### ما الفرق بين Clustered و Non-Clustered Index؟

| Clustered                   | Non-Clustered              |
| --------------------------- | -------------------------- |
| يرتب البيانات فيزيائياً     | لا يرتب البيانات فيزيائياً |
| واحد فقط لكل جدول           | عدة (حتى 999) لكل جدول     |
| أسرع في البحث بالمدى        | أسرع في البحث المحدد       |
| لا يحتاج مساحة إضافية كبيرة | يحتاج مساحة إضافية         |
| أبطأ في الـ INSERT/UPDATE   | أسرع في الـ INSERT/UPDATE  |

### ما الفرق بين SQL و NoSQL Databases؟

**SQL Databases (علاقية):**

- هيكل محدد مسبقاً (Schema)
- ACID properties (Atomicity, Consistency, Isolation, Durability)
- استخدام SQL language
- علاقات بين الجداول (Relations)
- مثال: SQL Server, MySQL, PostgreSQL, Oracle

**NoSQL Databases (غير علاقية):**

- مرونة في الهيكل (Schema-less)
- قابلية توسع أفقي عالية
- أداء أفضل للبيانات الكبيرة
- أنواع مختلفة: Document, Key-Value, Column-family, Graph
- مثال: MongoDB, Redis, Cassandra, Neo4j

### ما هو Temp Table ومتى يستخدم؟

**Temp Table:** جدول مؤقت يُنشأ لتخزين البيانات المؤقتة أثناء session معين.

**الأنواع:**

- **Local Temp Table (#TableName):** متاح للـ session الحالي فقط
- **Global Temp Table (##TableName):** متاح لجميع الـ sessions

**الاستخدام:**

- تخزين النتائج المؤقتة للعمليات المعقدة
- تحسين الأداء في الاستعلامات المعقدة
- معالجة البيانات على مراحل متعددة
- تجنب تكرار الاستعلامات المعقدة

### ما هو الفرق بين Union و Union All؟

**UNION:**

- يجمع النتائج من استعلامين أو أكثر ويزيل المكررات
- أبطأ لأنه يتحقق من المكررات ويرتب النتائج
- يتطلب أعمدة متطابقة في النوع والعدد

**UNION ALL:**

- يجمع جميع النتائج بما في ذلك المكررات
- أسرع لأنه لا يتحقق من المكررات
- يحافظ على ترتيب النتائج كما هي

### ما هو الفرق بين Join بأنواعه المختلفة من حيث الأداء؟

**INNER JOIN:**

- الأسرع لأنه يرجع فقط الصفوف المتطابقة
- يستخدم عندما نريد البيانات الموجودة في كلا الجدولين

**LEFT JOIN:**

- أبطأ من INNER JOIN لأنه يرجع جميع صفوف الجدول الأيسر
- يستخدم عندما نريد جميع البيانات من الجدول الأيسر مع البيانات المتطابقة من الأيمن

**RIGHT JOIN:**

- مشابه لـ LEFT JOIN لكن العكس
- أقل استخداماً من LEFT JOIN

**FULL OUTER JOIN:**

- الأبطأ لأنه يرجع جميع الصفوف من كلا الجدولين
- يستخدم عندما نريد جميع البيانات من كلا الجدولين

**Nested Query:**

- عادة أبطأ من الـ JOINs
- يتم تنفيذ الاستعلام الداخلي لكل صف في الخارجي

### ما هو Alias في SQL؟

**Alias:** اسم مؤقت يُعطى للجداول أو الأعمدة لتسهيل القراءة والكتابة.

```sql
-- للأعمدة
SELECT FirstName AS Name, LastName AS Surname FROM Users

-- للجداول
SELECT u.Name, o.OrderDate
FROM Users u
JOIN Orders o ON u.ID = o.UserID
```

### ما هو الفرق بين Primary Key و Unique Key و Composite Key؟

**Primary Key:**

- يحدد كل صف بشكل فريد
- لا يقبل NULL values
- جدول واحد يحتوي على primary key واحد فقط
- ينشئ Clustered Index تلقائياً

**Unique Key:**

- يضمن عدم تكرار القيم
- يقبل NULL value واحد فقط
- يمكن وجود عدة unique keys في الجدول
- ينشئ Non-Clustered Index تلقائياً

**Composite Key:**

- مفتاح يتكون من عمودين أو أكثر
- مجموع الأعمدة يجب أن يكون فريد
- يستخدم عندما عمود واحد لا يكفي للتفرد

### ما هو Normalization ولماذا يستخدم؟

**Normalization:** عملية تنظيم البيانات في قاعدة البيانات لتقليل التكرار وتحسين النزاهة.

**الأشكال الطبيعية:**

- **1NF:** كل خلية تحتوي على قيمة واحدة فقط
- **2NF:** 1NF + إزالة الاعتماد الجزئي
- **3NF:** 2NF + إزالة الاعتماد التعدي

**الفوائد:**

- تقليل تكرار البيانات
- توفير مساحة التخزين
- تحسين نزاهة البيانات
- تسهيل التحديث والصيانة

### كيف أعرف أن أداء Query معين جيد؟

**طرق قياس الأداء:**

- **Execution Time:** وقت التنفيذ
- **CPU Usage:** استخدام المعالج
- **Memory Usage:** استخدام الذاكرة
- **I/O Operations:** عمليات القراءة والكتابة

**أدوات القياس:**

- SQL Server Management Studio (Execution Plan)
- SET STATISTICS IO ON
- SET STATISTICS TIME ON
- SQL Server Profiler

**مؤشرات الأداء الجيد:**

- وقت تنفيذ قصير
- استخدام مناسب للـ Indexes
- قلة عمليات Table Scan
- استخدام فعال للذاكرة

### كيف أستخدم Ranking Functions في SQL؟

**الدوال المتاحة:**

```sql
-- ROW_NUMBER(): يعطي رقم تسلسلي فريد
SELECT ROW_NUMBER() OVER (ORDER BY Salary DESC) as RowNum, Name, Salary
FROM Employees

-- RANK(): يعطي رتبة مع تكرار وفجوات
SELECT RANK() OVER (ORDER BY Salary DESC) as Rank, Name, Salary
FROM Employees

-- DENSE_RANK(): يعطي رتبة مع تكرار بدون فجوات
SELECT DENSE_RANK() OVER (ORDER BY Salary DESC) as DenseRank, Name, Salary
FROM Employees

-- NTILE(): يقسم النتائج إلى مجموعات
SELECT NTILE(4) OVER (ORDER BY Salary DESC) as Quartile, Name, Salary
FROM Employees
```

### كيف أعمل Loop على Rows في قاعدة البيانات؟

**استخدام CURSOR:**

```sql
DECLARE @Name VARCHAR(50)
DECLARE employee_cursor CURSOR FOR
SELECT Name FROM Employees

OPEN employee_cursor
FETCH NEXT FROM employee_cursor INTO @Name

WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT @Name
    FETCH NEXT FROM employee_cursor INTO @Name
END

CLOSE employee_cursor
DEALLOCATE employee_cursor
```

**استخدام WHILE مع CTE:**

```sql
WITH EmployeeCTE AS (
    SELECT ROW_NUMBER() OVER (ORDER BY ID) as RowNum, Name,
           COUNT(*) OVER() as TotalRows
    FROM Employees
)
DECLARE @Counter INT = 1, @Total INT
SELECT @Total = MAX(TotalRows) FROM EmployeeCTE

WHILE @Counter <= @Total
BEGIN
    SELECT Name FROM EmployeeCTE WHERE RowNum = @Counter
    SET @Counter = @Counter + 1
END
```

### ما هو الـ Execution Plan؟

**Execution Plan:** خطة توضح كيف سيقوم SQL Server بتنفيذ الاستعلام خطوة بخطوة.

**أنواعه:**

- **Estimated Execution Plan:** خطة متوقعة بدون تنفيذ فعلي
- **Actual Execution Plan:** خطة حقيقية بعد التنفيذ

**فوائده:**

- تحديد الاختناقات في الأداء
- معرفة استخدام الـ Indexes
- تحسين الاستعلامات
- فهم تكلفة كل عملية

**كيفية قراءته:**

- يقرأ من اليمين إلى اليسار
- النسب المئوية تشير إلى تكلفة كل عملية
- الأسهم السميكة تشير إلى نقل بيانات كثيرة

### ما الفرق بين Delete و Truncate و Drop؟

**DELETE:**

- يحذف صفوف محددة أو جميعها
- يمكن استخدام WHERE clause
- يحتفظ بهيكل الجدول
- يمكن التراجع عنه (مع Transaction)
- أبطأ لأنه يسجل كل عملية حذف

```sql
DELETE FROM Users WHERE Age < 18
```

**TRUNCATE:**

- يحذف جميع الصفوف فقط
- لا يمكن استخدام WHERE clause
- يحتفظ بهيكل الجدول
- أسرع من DELETE
- لا يمكن التراجع عنه في بعض الحالات

```sql
TRUNCATE TABLE Users
```

**DROP:**

- يحذف الجدول بالكامل (الهيكل والبيانات)
- يحذف الجدول من قاعدة البيانات نهائياً
- لا يمكن التراجع عنه

```sql
DROP TABLE Users
```

### كيف أتعامل مع الـ Transaction في SQL؟

**Transaction:** مجموعة من العمليات التي تُنفذ كوحدة واحدة (إما جميعها أو لا شيء).

```sql
BEGIN TRANSACTION

TRY
    INSERT INTO Orders (CustomerID, OrderDate) VALUES (1, GETDATE())
    UPDATE Products SET Stock = Stock - 1 WHERE ID = 1

    COMMIT TRANSACTION
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION
    PRINT 'Error occurred: ' + ERROR_MESSAGE()
END CATCH
```

**خصائص ACID:**

- **Atomicity:** كل أو لا شيء
- **Consistency:** البيانات متسقة
- **Isolation:** المعاملات معزولة
- **Durability:** النتائج دائمة

### ما هو SQL Profiler؟

**SQL Profiler:** أداة لمراقبة وتسجيل النشاطات في SQL Server.

**الاستخدامات:**

- مراقبة الاستعلامات البطيئة
- تتبع الأخطاء والمشاكل
- مراقبة الأمان والوصول
- تحليل الأداء العام

**البدائل الحديثة:**

- **Extended Events:** أكثر كفاءة وأقل تأثيراً على الأداء
- **SQL Server Management Studio Activity Monitor**
- **Azure SQL Analytics**

---

## 🛠️ ثانياً: Entity Framework / EF Core

### ما الفرق بين EF و EF Core؟

**Entity Framework (.NET Framework):**

- يعمل فقط مع .NET Framework
- أكثر نضجاً وله مميزات أكثر
- يدعم EDMX files
- أداء أبطأ نسبياً

**Entity Framework Core (.NET Core/.NET 5+):**

- يعمل مع .NET Core و .NET 5+ و .NET Framework
- خفيف وسريع الأداء
- مفتوح المصدر ومتعدد المنصات
- لا يدعم جميع مميزات EF التقليدي لكن يتطور بسرعة

### ما الفرق بين Code First و Database First؟

**Code First:**

- تكتب الـ Classes أولاً ثم تنشئ قاعدة البيانات
- مرونة أكبر في التحكم
- أسهل في إدارة الإصدارات (Migrations)
- مناسب للمشاريع الجديدة

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

**Database First:**

- قاعدة البيانات موجودة أولاً ثم تنشئ الـ Classes
- مناسب للمشاريع الموجودة
- أقل مرونة في التعديل
- يتطلب إعادة إنشاء الـ Models عند تغيير قاعدة البيانات

### ما هو الـ Seed وكيف يستخدم؟

**Seed:** عملية إدخال بيانات أولية في قاعدة البيانات عند إنشائها.

```csharp
// في OnModelCreating
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<User>().HasData(
        new User { Id = 1, Name = "Admin", Email = "admin@example.com" },
        new User { Id = 2, Name = "User", Email = "user@example.com" }
    );
}

// أو في OnConfiguring
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    optionsBuilder.UseSqlServer(connectionString);
}
```

### ما هي أهم Commands التي تُستخدم مع EF؟

**Package Manager Console:**

```powershell
# إنشاء Migration جديد
Add-Migration InitialCreate

# تطبيق Migrations على قاعدة البيانات
Update-Database

# إزالة Migration الأخير
Remove-Migration

# عرض جميع Migrations
Get-Migration

# إنشاء Script لـ Migration
Script-Migration

# إنشاء قاعدة البيانات
Scaffold-DbContext "connectionString" Microsoft.EntityFrameworkCore.SqlServer
```

**CLI Commands:**

```bash
# إنشاء Migration
dotnet ef migrations add InitialCreate

# تطبيق Migration
dotnet ef database update

# إزالة Migration
dotnet ef migrations remove
```

### ما الفرق بين IQueryable و IEnumerable؟

**IQueryable:**

- يبني Expression Tree
- التنفيذ مؤجل (Deferred Execution)
- يترجم إلى SQL ويتم التنفيذ في قاعدة البيانات
- أفضل للأداء مع قواعد البيانات

```csharp
IQueryable<User> query = context.Users.Where(u => u.Age > 18);
// لم يتم تنفيذ الاستعلام بعد

var result = query.ToList(); // الآن يتم التنفيذ
```

**IEnumerable:**

- يعمل مع الكائنات في الذاكرة
- التنفيذ مؤجل أيضاً لكن في الذاكرة
- جميع البيانات يتم جلبها إلى الذاكرة أولاً

```csharp
IEnumerable<User> users = context.Users.ToList().Where(u => u.Age > 18);
// جميع المستخدمين في الذاكرة ثم الفلترة
```

### كيف أعمل Pagination يعرض 10 عناصر في كل مرة؟

```csharp
public async Task<List<User>> GetUsersAsync(int page, int pageSize = 10)
{
    return await context.Users
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .ToListAsync();
}

// مع معلومات إضافية
public class PagedResult<T>
{
    public List<T> Items { get; set; }
    public int TotalCount { get; set; }
    public int Page { get; set; }
    public int PageSize { get; set; }
    public int TotalPages => (int)Math.Ceiling((double)TotalCount / PageSize);
}

public async Task<PagedResult<User>> GetUsersPagedAsync(int page, int pageSize = 10)
{
    var totalCount = await context.Users.CountAsync();
    var users = await context.Users
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .ToListAsync();

    return new PagedResult<User>
    {
        Items = users,
        TotalCount = totalCount,
        Page = page,
        PageSize = pageSize
    };
}
```

### ما الفرق بين Eager Loading و Lazy Loading؟

**Eager Loading:**

- يجلب البيانات المرتبطة مع الاستعلام الأساسي
- استخدام Include()
- أداء أفضل عند الحاجة للبيانات المرتبطة
- استعلام واحد كبير

```csharp
var users = context.Users
    .Include(u => u.Orders)
    .ThenInclude(o => o.OrderItems)
    .ToList();
```

**Lazy Loading:**

- يأجل جلب البيانات المرتبطة حتى الوصول إليها
- يتطلب virtual properties
- عدة استعلامات صغيرة
- خطر N+1 Query Problem

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public virtual List<Order> Orders { get; set; } // virtual للـ Lazy Loading
}

// الاستخدام
var user = context.Users.First();
var orders = user.Orders; // هنا يتم جلب Orders
```

**Explicit Loading:**

```csharp
var user = context.Users.First();
context.Entry(user)
    .Collection(u => u.Orders)
    .Load();
```

### ما هو Tracking في EF Core؟

**Tracking:** آلية تتبع التغييرات على الكائنات المجلبة من قاعدة البيانات.

**مع Tracking (افتراضي):**

```csharp
var user = context.Users.First(); // مُتتبع
user.Name = "New Name";
context.SaveChanges(); // يحفظ التغيير تلقائياً
```

**بدون Tracking:**

```csharp
var users = context.Users.AsNoTracking().ToList(); // غير مُتتبع
// أسرع للقراءة فقط، لا يمكن حفظ التغييرات
```

**فوائد No Tracking:**

- أداء أفضل للقراءة فقط
- استهلاك ذاكرة أقل
- مناسب للتقارير والاستعلامات الكبيرة

**حالات الـ Entity States:**

- **Added:** كائن جديد سيتم إدراجه
- **Modified:** كائن معدل سيتم تحديثه
- **Deleted:** كائن محذوف سيتم حذفه
- **Unchanged:** كائن غير معدل
- **Detached:** كائن غير مُتتبع

---

## 🌐 ثالثاً: ASP.NET Core / MVC

### ما الفرق بين ASP.NET MVC و ASP.NET Core؟

**ASP.NET MVC (.NET Framework):**

- يعمل فقط على Windows
- مبني على .NET Framework
- أبطأ في الأداء
- IIS dependency
- System.Web dependency

**ASP.NET Core:**

- متعدد المنصات (Windows, Linux, macOS)
- مبني على .NET Core/.NET 5+
- أداء عالي وسريع
- مستقل عن IIS
- مفتوح المصدر
- Built-in Dependency Injection
- Unified MVC and Web API

### ما هو الـ Middleware وكيف أكتبه؟

**Middleware:** مكونات تتعامل مع HTTP requests و responses في pipeline معين.

**كتابة Middleware بسيط:**

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        // عمل شيء قبل المرور للـ middleware التالي
        Console.WriteLine("Before next middleware");

        await _next(context); // استدعاء الـ middleware التالي

        // عمل شيء بعد العودة من الـ middleware التالي
        Console.WriteLine("After next middleware");
    }
}

// التسجيل في Program.cs
app.UseMiddleware<CustomMiddleware>();
```

**استخدام الـ Middleware:**

```csharp
// في Program.cs
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### ما الفرق بين Middleware و Filter؟

**Middleware:**

- يعمل على مستوى Application
- يتعامل مع جميع الـ requests
- ترتيب التنفيذ مهم جداً
- يمكنه منع وصول الـ request للـ MVC pipeline

**Filter:**

- يعمل على مستوى MVC فقط
- يتعامل مع Actions محددة
- أنواع مختلفة (Authorization, Action, Result, Exception)
- أكثر تخصصاً

**أنواع الـ Filters:**

```csharp
// Authorization Filter
public class CustomAuthorizationFilter : IAuthorizationFilter
{
    public void OnAuthorization(AuthorizationFilterContext context)
    {
        // التحقق من الصلاحيات
    }
}

// Action Filter
public class CustomActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
        // قبل تنفيذ الـ Action
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
        // بعد تنفيذ الـ Action
    }
}
```

### ما هو الـ Request Lifecycle في MVC؟

**المراحل بالترتيب:**

1. **HTTP Request** يصل للخادم
2. **Middleware Pipeline** يعالج الـ request
3. **Routing** يحدد الـ Controller والـ Action
4. **Model Binding** يربط البيانات بالـ parameters
5. **Authorization Filters** يتحقق من الصلاحيات
6. **Action Filters** (OnActionExecuting)
7. **Action Method** يتم تنفيذه
8. **Action Filters** (OnActionExecuted)
9. **Result Filters** (OnResultExecuting)
10. **View** يتم إنشاؤه (إذا كان ViewResult)
11. **Result Filters** (OnResultExecuted)
12. **Response** يرسل للعميل

### ما هو الـ Routing وما علاقة ترتيب الـ Middleware؟

**Routing:** آلية تحديد أي Controller و Action سيتم استدعاؤهما بناءً على الـ URL.

**أنواع الـ Routing:**

```csharp
// Convention-based Routing
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

// Attribute Routing
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet("{id}")]
    public IActionResult GetUser(int id) { }

    [HttpPost]
    public IActionResult CreateUser([FromBody] User user) { }
}
```

**ترتيب الـ Middleware مهم:**

```csharp
app.UseHttpsRedirection();  // 1
app.UseStaticFiles();       // 2
app.UseRouting();           // 3 - يجب أن يكون قبل UseAuthorization
app.UseAuthentication();    // 4
app.UseAuthorization();     // 5 - يجب أن يكون بعد UseRouting
app.MapControllers();       // 6
```

### ما هو الفرق بين ViewBag و ViewData و TempData؟

**ViewData:**

- Dictionary من نوع ViewDataDictionary
- Key-Value pairs
- متاح فقط في الـ View الحالي
- يتطلب Type Casting

```csharp
// في الـ Controller
ViewData["Message"] = "Hello World";
ViewData["Count"] = 10;

// في الـ View
<h1>@ViewData["Message"]</h1>
<p>Count: @((int)ViewData["Count"])</p>
```

**ViewBag:**

- Dynamic wrapper حول ViewData
- أسهل في الاستخدام
- لا يتطلب Type Casting
- متاح فقط في الـ View الحالي

```csharp
// في الـ Controller
ViewBag.Message = "Hello World";
ViewBag.Count = 10;

// في الـ View
<h1>@ViewBag.Message</h1>
<p>Count: @ViewBag.Count</p>
```

**TempData:**

- يستخدم Session أو Cookies
- متاح عبر Redirects
- يتم حذفه بعد القراءة (Keep لمنع الحذف)
- مناسب لرسائل النجاح/الخطأ

```csharp
// في الـ Controller
TempData["Success"] = "User created successfully";
return RedirectToAction("Index");

// في الـ View التالي
@if (TempData["Success"] != null)
{
    <div class="alert alert-success">@TempData["Success"]</div>
}
```

### ما الطرق المتاحة لنقل البيانات من View إلى Controller؟

**1. Model Binding:**

```csharp
// POST Form
[HttpPost]
public IActionResult Create(User user)
{
    // الـ user يتم ملؤه تلقائياً من الـ Form
}
```

**2. Query Parameters:**

```csharp
public IActionResult Search(string term, int page = 1)
{
    // /Search?term=john&page=2
}
```

**3. Route Parameters:**

```csharp
[HttpGet("users/{id}")]
public IActionResult GetUser(int id)
{
    // /users/123
}
```

**4. Form Data:**

```csharp
[HttpPost]
public IActionResult Submit(IFormCollection form)
{
    var value = form["fieldName"];
}
```

**5. JSON Body:**

```csharp
[HttpPost]
public IActionResult CreateUser([FromBody] User user)
{
    // JSON في الـ request body
}
```

**6. Headers:**

```csharp
public IActionResult Index([FromHeader] string authorization)
{
    // من الـ HTTP headers
}
```

### ما هو الـ Ajax وكيف أستخدمه مع MVC؟

**Ajax:** تقنية لإرسال واستقبال البيانات بدون إعادة تحميل الصفحة.

**باستخدام jQuery:**

```javascript
$.ajax({
  url: "/Users/Create",
  type: "POST",
  data: {
    name: "John Doe",
    email: "john@example.com",
  },
  success: function (result) {
    alert("User created successfully");
  },
  error: function () {
    alert("Error occurred");
  },
});
```

**في الـ Controller:**

```csharp
[HttpPost]
public IActionResult Create(User user)
{
    if (ModelState.IsValid)
    {
        // حفظ المستخدم
        return Json(new { success = true, message = "User created" });
    }
    return Json(new { success = false, errors = ModelState.Values });
}
```

**باستخدام Fetch API:**

```javascript
fetch("/Users/Create", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "John Doe",
    email: "john@example.com",
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### ما هو الـ Identity وما علاقته بالـ Token؟

**ASP.NET Identity:** نظام إدارة المستخدمين والأدوار والمصادقة المدمج في ASP.NET.

**المميزات:**

- إدارة Users و Roles
- Password hashing
- Two-factor authentication
- External login providers (Google, Facebook)
- Claims-based authentication

**الإعداد:**

```csharp
// في Program.cs
builder.Services.AddIdentity<IdentityUser, IdentityRole>()
    .AddEntityFrameworkStores<ApplicationDbContext>()
    .AddDefaultTokenProviders();

// في Controller
public class AccountController : Controller
{
    private readonly UserManager<IdentityUser> _userManager;
    private readonly SignInManager<IdentityUser> _signInManager;

    [HttpPost]
    public async Task<IActionResult> Login(LoginViewModel model)
    {
        var result = await _signInManager.PasswordSignInAsync(
            model.Email, model.Password, model.RememberMe, false);

        if (result.Succeeded)
        {
            return RedirectToAction("Index", "Home");
        }
        return View(model);
    }
}
```

### ما هو الـ JWT Token ولماذا يُستخدم؟

**JWT (JSON Web Token):** معيار لتمرير المعلومات بشكل آمن بين الأطراف.

**التركيب:**

- **Header:** نوع التوكن والخوارزمية
- **Payload:** البيانات (Claims)
- **Signature:** التوقيع للتحقق من صحة التوكن

**المميزات:**

- Stateless (لا يحتاج تخزين في الخادم)
- Cross-domain authentication
- Mobile-friendly
- يحتوي على المعلومات المطلوبة

**الإنشاء:**

```csharp
public string GenerateJwtToken(User user)
{
    var tokenHandler = new JwtSecurityTokenHandler();
    var key = Encoding.ASCII.GetBytes(_secretKey);

    var tokenDescriptor = new SecurityTokenDescriptor
    {
        Subject = new ClaimsIdentity(new[]
        {
            new Claim("id", user.Id.ToString()),
            new Claim("email", user.Email)
        }),
        Expires = DateTime.UtcNow.AddDays(7),
        SigningCredentials = new SigningCredentials(
            new SymmetricSecurityKey(key),
            SecurityAlgorithms.HmacSha256Signature)
    };

    var token = tokenHandler.CreateToken(tokenDescriptor);
    return tokenHandler.WriteToken(token);
}
```

**الإعداد:**

```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuerSigningKey = true,
            IssuerSigningKey = new SymmetricSecurityKey(key),
            ValidateIssuer = false,
            ValidateAudience = false
        };
    });
```

### ما الفرق بين Get و Post و Put و Delete في الـ API؟

**HTTP Methods:**

**GET:**

- للاستعلام عن البيانات
- Idempotent (آمن للتكرار)
- البيانات في الـ URL
- يمكن حفظه في Cache

```csharp
[HttpGet("{id}")]
public IActionResult GetUser(int id)
{
    var user = _userService.GetById(id);
    return Ok(user);
}
```

**POST:**

- لإنشاء بيانات جديدة
- ليس Idempotent
- البيانات في الـ Body
- لا يُحفظ في Cache

```csharp
[HttpPost]
public IActionResult CreateUser([FromBody] User user)
{
    var createdUser = _userService.Create(user);
    return CreatedAtAction(nameof(GetUser),
        new { id = createdUser.Id }, createdUser);
}
```

**PUT:**

- لتحديث البيانات (Replace كامل)
- Idempotent
- يتطلب إرسال جميع الخصائص

```csharp
[HttpPut("{id}")]
public IActionResult UpdateUser(int id, [FromBody] User user)
{
    if (id != user.Id) return BadRequest();

    _userService.Update(user);
    return NoContent();
}
```

**DELETE:**

- لحذف البيانات
- Idempotent
- عادة لا يحتاج Body

```csharp
[HttpDelete("{id}")]
public IActionResult DeleteUser(int id)
{
    _userService.Delete(id);
    return NoContent();
}
```

**PATCH:**

- للتحديث الجزئي
- يرسل فقط الخصائص المطلوب تحديثها

### ما هو الـ API ولماذا نستخدمه؟

**API (Application Programming Interface):** واجهة تسمح للتطبيقات بالتواصل مع بعضها البعض.

**الفوائد:**

- **Separation of Concerns:** فصل الـ Frontend عن الـ Backend
- **Reusability:** يمكن استخدام نفس الـ API لعدة تطبيقات
- **Scalability:** توسع أفضل
- **Platform Independence:** يعمل مع أي منصة
- **Mobile Support:** سهولة دعم التطبيقات المحمولة

**أنواع الـ APIs:**

- **REST API:** الأكثر شيوعاً
- **GraphQL:** مرونة أكبر في الاستعلامات
- **SOAP:** للأنظمة القديمة
- **gRPC:** عالي الأداء

### ما هو API Versioning؟

**API Versioning:** آلية إدارة إصدارات مختلفة من الـ API لضمان عدم كسر التطبيقات الموجودة.

**الطرق:**

**1. URL Path Versioning:**

```csharp
[Route("api/v1/[controller]")]
public class UsersV1Controller : ControllerBase { }

[Route("api/v2/[controller]")]
public class UsersV2Controller : ControllerBase { }
```

**2. Query Parameter:**

```csharp
[ApiVersion("1.0")]
[ApiVersion("2.0")]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet]
    [MapToApiVersion("1.0")]
    public IActionResult GetV1() { }

    [HttpGet]
    [MapToApiVersion("2.0")]
    public IActionResult GetV2() { }
}
```

**3. Header Versioning:**

```csharp
// Header: api-version: 1.0
services.AddApiVersioning(opt =>
{
    opt.ApiVersionReader = new HeaderApiVersionReader("api-version");
});
```

### ما الفرق بين In-memory Caching و Distributed Caching؟

**In-memory Caching:**

- يخزن البيانات في ذاكرة الخادم المحلي
- سريع جداً
- يفقد البيانات عند إعادة تشغيل التطبيق
- مناسب للتطبيقات ذات الخادم الواحد

```csharp
services.AddMemoryCache();

public class HomeController : Controller
{
    private readonly IMemoryCache _cache;

    public IActionResult Index()
    {
        var cacheKey = "users_list";
        if (!_cache.TryGetValue(cacheKey, out List<User> users))
        {
            users = _userService.GetAll();
            _cache.Set(cacheKey, users, TimeSpan.FromMinutes(30));
        }
        return View(users);
    }
}
```

**Distributed Caching:**

- يخزن البيانات في نظام خارجي (Redis, SQL Server)
- أبطأ من In-memory لكن مشترك بين الخوادم
- يبقى موجود عند إعادة تشغيل التطبيق
- مناسب للتطبيقات الموزعة

```csharp
services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = "localhost:6379";
});

public class HomeController : Controller
{
    private readonly IDistributedCache _cache;

    public async Task<IActionResult> Index()
    {
        var cacheKey = "users_list";
        var cachedUsers = await _cache.GetStringAsync(cacheKey);

        List<User> users;
        if (cachedUsers == null)
        {
            users = _userService.GetAll();
            var serializedUsers = JsonSerializer.Serialize(users);
            await _cache.SetStringAsync(cacheKey, serializedUsers,
                new DistributedCacheEntryOptions
                {
                    AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(30)
                });
        }
        else
        {
            users = JsonSerializer.Deserialize<List<User>>(cachedUsers);
        }

        return View(users);
    }
}
```

### ما هو Repository Pattern وما علاقة Unit of Work به؟

**Repository Pattern** هو نمط تصميم يوفر طبقة تجريد بين منطق العمل وطبقة الوصول للبيانات. يسمح بتنظيم وإدارة العمليات على البيانات بشكل منفصل عن قاعدة البيانات المحددة.

**فوائد Repository Pattern:**
- فصل منطق العمل عن طبقة البيانات
- سهولة اختبار الوحدة
- قابلية الصيانة والتوسعة
- إمكانية تغيير قاعدة البيانات دون تأثير على منطق العمل

**Unit of Work** يعمل مع Repository Pattern لإدارة المعاملات وضمان الاتساق في البيانات. يحتفظ بقائمة من الكائنات المتأثرة ويدير كتابة التغييرات وحل مشاكل التزامن.

```csharp
public interface IUnitOfWork
{
    IUserRepository Users { get; }
    IOrderRepository Orders { get; }
    Task<int> SaveChangesAsync();
}
```

## Dependency Injection

### كيف أعمل Dependency Injection وما الفرق بين AddSingleton وAddScoped وAddTransient؟

**Dependency Injection** هو نمط تصميم يحقق Inversion of Control من خلال حقن التبعيات بدلاً من إنشائها داخل الكلاس.

**أنواع دورة الحياة في DI:**

- **AddTransient**: ينشئ instance جديد في كل مرة يطلب
- **AddScoped**: ينشئ instance واحد لكل HTTP request
- **AddSingleton**: ينشئ instance واحد فقط طوال دورة حياة التطبيق

```csharp
services.AddTransient<IEmailService, EmailService>();
services.AddScoped<IUserService, UserService>();
services.AddSingleton<ICacheService, CacheService>();
```

## Architecture Patterns

### ما هو Clean Architecture وما الفرق بين N-Tier وOnion Architecture؟

**Clean Architecture** هو نهج معماري يركز على فصل الاهتمامات وجعل النظام قابل للاختبار والصيانة.

**الفروق:**

**N-Tier Architecture:**
- طبقات أفقية (Presentation, Business, Data)
- التبعيات تتجه من أعلى لأسفل
- أقل مرونة في التغيير

**Onion Architecture:**
- طبقات دائرية مع Domain في المركز
- التبعيات تتجه للداخل
- مرونة أكبر وقابلية اختبار أفضل

**Clean Architecture:**
- يجمع مزايا الأنماط السابقة
- فصل واضح للاهتمامات
- استقلالية تامة للطبقات الداخلية

### كيف أتعامل مع Service Registration؟

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Repository Pattern
    services.AddScoped<IUserRepository, UserRepository>();
    
    // Business Services
    services.AddScoped<IUserService, UserService>();
    
    // AutoMapper
    services.AddAutoMapper(typeof(MappingProfile));
    
    // Database Context
    services.AddDbContext<AppDbContext>(options =>
        options.UseSqlServer(connectionString));
}
```

## Advanced Patterns

### ما هو DDD (Domain-Driven Design)؟

**Domain-Driven Design** هو نهج لتطوير البرمجيات يركز على النمذجة المعقدة للمجال ووضع منطق المجال في قلب التطبيق.

**المكونات الأساسية:**
- **Entities**: كائنات لها هوية فريدة
- **Value Objects**: كائنات بدون هوية، تعرف بقيمها
- **Aggregates**: مجموعة من الكائنات المترابطة
- **Domain Services**: خدمات تحتوي على منطق المجال
- **Repositories**: للوصول للبيانات

### ما هو CQRS وما فائدته؟

**CQRS (Command Query Responsibility Segregation)** هو نمط يفصل بين عمليات القراءة والكتابة.

**الفوائد:**
- تحسين الأداء
- قابلية التوسع المستقلة
- مرونة في النمذجة
- أمان أفضل

```csharp
// Command
public class CreateUserCommand
{
    public string Name { get; set; }
    public string Email { get; set; }
}

// Query
public class GetUserQuery
{
    public int UserId { get; set; }
}
```

### ما هو RabbitMQ؟

**RabbitMQ** هو message broker يسمح للتطبيقات بالتواصل من خلال تمرير الرسائل.

**الاستخدامات:**
- التواصل غير المتزامن بين الخدمات
- معالجة المهام في الخلفية
- فصل المكونات المترابطة
- ضمان تسليم الرسائل

### ما هو Replication وما فائدته؟

**Database Replication** هو عملية نسخ البيانات من خادم قاعدة بيانات إلى خوادم أخرى.

**الأنواع:**
- **Master-Slave**: خادم رئيسي للكتابة وخوادم فرعية للقراءة
- **Master-Master**: عدة خوادم يمكنها الكتابة والقراءة

**الفوائد:**
- تحسين الأداء
- توفير النسخ الاحتياطية
- توزيع الحمولة
- زيادة الموثوقية

## OOP Concepts

### ما الفرق بين Abstract Class وInterface؟

| Abstract Class | Interface |
|----------------|-----------|
| يمكن أن يحتوي على implementation | فقط تعريفات (حتى C# 8.0) |
| يدعم constructors | لا يدعم constructors |
| يمكن أن يحتوي على fields | فقط properties وmethods |
| وراثة واحدة فقط | يمكن تطبيق متعدد |
| يستخدم extends | يستخدم implements |

### ما الفرق بين Overloading وOverriding؟

**Overloading (Compile-time Polymorphism):**
- نفس اسم الدالة مع parameters مختلفة
- يحدث في وقت الترجمة
- في نفس الكلاس أو كلاسات مختلفة

**Overriding (Runtime Polymorphism):**
- إعادة تعريف دالة في الكلاس الفرعي
- يحدث في وقت التشغيل
- يتطلب virtual/override

```csharp
// Overloading
public void Calculate(int a, int b) { }
public void Calculate(double a, double b) { }

// Overriding
public virtual void Display() { }
public override void Display() { }
```

### ما هو Constructor وما فائدته وما الفرق بينه وبين Destructor؟

**Constructor:**
- دالة خاصة تستدعى عند إنشاء كائن
- نفس اسم الكلاس
- لا يرجع قيمة
- يستخدم لتهيئة الكائن

**Destructor (Finalizer):**
- يستدعى قبل حذف الكائن من الذاكرة
- يبدأ بـ ~ متبوعاً باسم الكلاس
- لا يمكن استدعاؤه مباشرة
- يدار من قبل Garbage Collector

### ما الفرق بين Static Class, Sealed Class, Abstract Class؟

**Static Class:**
- لا يمكن إنشاء instance منه
- جميع الأعضاء static
- لا يمكن وراثته
- يحمل في الذاكرة طوال دورة حياة التطبيق

**Sealed Class:**
- يمكن إنشاء instance منه
- لا يمكن وراثته
- جميع أعضائه عاديين

**Abstract Class:**
- لا يمكن إنشاء instance منه مباشرة
- يجب وراثته
- يمكن أن يحتوي على abstract methods

### ما الفرق بين Static Method وStatic Variable؟

**Static Method:**
- ينتمي للكلاس وليس للكائن
- لا يمكن الوصول لأعضاء الكائن العاديين
- يستدعى باستخدام اسم الكلاس

**Static Variable:**
- مشتركة بين جميع كائنات الكلاس
- تهيأ مرة واحدة فقط
- تبقى في الذاكرة طوال دورة حياة التطبيق

### ما هو Encapsulation وكيف أحققه؟

**Encapsulation** هو إخفاء التفاصيل الداخلية للكائن وتوفير واجهة محددة للتفاعل معه.

**كيفية تحقيقه:**
- استخدام Access Modifiers
- استخدام Properties بدلاً من Fields
- إخفاء Implementation Details

```csharp
public class BankAccount
{
    private decimal _balance;
    
    public decimal Balance 
    { 
        get { return _balance; }
        private set { _balance = value; }
    }
    
    public void Deposit(decimal amount)
    {
        if (amount > 0)
            _balance += amount;
    }
}
```

### ما الفرق بين Property وField وكيف تحقق Encapsulation؟

**Field:**
- متغير عادي في الكلاس
- وصول مباشر للقيمة
- لا يوفر تحكم في العمليات

**Property:**
- واجهة للوصول للـ Field
- يحتوي على Get/Set accessors
- يوفر تحكم وvalidation

```csharp
// Field
private string _name;

// Property
public string Name
{
    get { return _name; }
    set 
    { 
        if (!string.IsNullOrEmpty(value))
            _name = value; 
    }
}
```

### ما الفرق بين Struct وClass وInterface؟

| Feature | Struct | Class | Interface |
|---------|--------|-------|-----------|
| Type | Value Type | Reference Type | Contract |
| Inheritance | لا يدعم | يدعم | يدعم تعدد |
| Default Constructor | تلقائي | يمكن تخصيصه | لا يوجد |
| Null Value | لا يمكن | يمكن | N/A |
| Performance | أسرع | أبطأ نسبياً | N/A |

### ما هو Polymorphism (Static vs Dynamic)؟

**Static Polymorphism (Compile-time):**
- Method Overloading
- Operator Overloading
- يحدد في وقت الترجمة

**Dynamic Polymorphism (Runtime):**
- Method Overriding
- Virtual Functions
- يحدد في وقت التشغيل

```csharp
// Static Polymorphism
public class Calculator
{
    public int Add(int a, int b) { return a + b; }
    public double Add(double a, double b) { return a + b; }
}

// Dynamic Polymorphism
public virtual void Draw() { }
public override void Draw() { }
```

### ما هو الفرق بين Composition وInheritance ولماذا نفضل الأولى؟

**Inheritance (Is-A Relationship):**
- علاقة "هو من نوع"
- وراثة السلوك والخصائص
- ترابط قوي

**Composition (Has-A Relationship):**
- علاقة "يحتوي على"
- تجميع كائنات مختلفة
- ترابط ضعيف

**لماذا نفضل Composition:**
- مرونة أكبر
- سهولة التغيير
- تجنب مشاكل الوراثة المتعددة
- اختبار أسهل

```csharp
// Inheritance
public class Car : Vehicle { }

// Composition
public class Car
{
    private Engine _engine;
    private Wheel[] _wheels;
}
```

### ما هو Access Modifiers؟

**أنواع Access Modifiers في C#:**

- **public**: الوصول من أي مكان
- **private**: الوصول من نفس الكلاس فقط
- **protected**: الوصول من الكلاس والكلاسات المشتقة
- **internal**: الوصول من نفس Assembly
- **protected internal**: الوصول من Assembly أو الكلاسات المشتقة
- **private protected**: الوصول من الكلاسات المشتقة في نفس Assembly

### هل كل أعضاء Class يمكن توريثهم؟

**لا، ليس جميع الأعضاء قابلون للوراثة:**

**يمكن توريثها:**
- public members
- protected members
- protected internal members

**لا يمكن توريثها:**
- private members
- Constructors
- Destructors
- static constructors

### ما هو الفرق بين Value Type وReference Type؟

**Value Type:**
- يخزن في Stack
- نسخ مباشر للقيمة
- أمثلة: int, double, struct, enum
- لا يمكن أن يكون null (إلا nullable types)

**Reference Type:**
- يخزن في Heap
- يحتوي على مرجع للقيمة
- أمثلة: class, interface, delegate, string
- يمكن أن يكون null

### ما الفرق بين Hashtable وDictionary؟

| Hashtable | Dictionary |
|-----------|------------|
| غير Generic | Generic |
| أبطأ نسبياً | أسرع |
| Thread-safe للقراءة | غير Thread-safe |
| يقبل null values | لا يقبل null keys |
| Boxing/Unboxing | No Boxing/Unboxing |

### ما الفرق بين var وdynamic؟

**var:**
- Static typing
- يحدد النوع في وقت الترجمة
- يجب تهيئته عند التصريح
- أداء أفضل

**dynamic:**
- Dynamic typing
- يحدد النوع في وقت التشغيل
- يمكن تغيير النوع
- أداء أبطأ

```csharp
var x = 10; // int
dynamic y = 10; // يمكن تغييره لاحقاً
y = "Hello"; // صالح
```

### ما هو Boxing وUnboxing؟

**Boxing:**
- تحويل Value Type إلى Reference Type
- يحدث تلقائياً
- يستهلك ذاكرة إضافية

**Unboxing:**
- تحويل Reference Type إلى Value Type
- يحتاج cast صريح
- قد يرمي exception

```csharp
// Boxing
int i = 10;
object obj = i; // Boxing

// Unboxing
int j = (int)obj; // Unboxing
```

### ما الفرق بين Early Binding وLate Binding؟

**Early Binding (Static Binding):**
- يحدد في وقت الترجمة
- أداء أفضل
- أمان أكبر في النوع
- مثال: Method Overloading

**Late Binding (Dynamic Binding):**
- يحدد في وقت التشغيل
- مرونة أكبر
- أداء أبطأ
- مثال: Method Overriding, Reflection

### ما هو Dispose وما الفرق بينه وبين Finalize؟

**Dispose:**
- يستدعى يدوياً
- لتنظيف الموارد المدارة وغير المدارة
- جزء من IDisposable interface
- سرعة في التنظيف

**Finalize:**
- يستدعى من Garbage Collector
- لتنظيف الموارد غير المدارة فقط
- بطيء ولا يمكن السيطرة على توقيته
- يؤخر حذف الكائن

```csharp
public class ResourceManager : IDisposable
{
    private bool _disposed = false;
    
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
    
    protected virtual void Dispose(bool disposing)
    {
        if (!_disposed)
        {
            if (disposing)
            {
                // تنظيف الموارد المدارة
            }
            // تنظيف الموارد غير المدارة
            _disposed = true;
        }
    }
    
    ~ResourceManager()
    {
        Dispose(false);
    }
}
```

### ما هو Method Signature؟

**Method Signature** يتكون من:
- اسم الدالة
- عدد ونوع المعاملات
- ترتيب المعاملات

**لا يشمل:**
- نوع الإرجاع
- أسماء المعاملات
- Access modifiers

```csharp
// نفس الـ Signature
public int Calculate(int a, int b)
public void Calculate(int x, int y) // خطأ - نفس الـ signature

// Signatures مختلفة
public int Calculate(int a, int b)
public int Calculate(double a, double b) // صحيح
```

### ما هي مشاكل الوراثة المفرطة؟

**مشاكل الوراثة المفرطة:**
- تعقيد في التصميم
- صعوبة في الصيانة
- ترابط قوي بين الكلاسات
- صعوبة في إجراء التغييرات
- مشاكل في الأداء
- Diamond Problem في الوراثة المتعددة

**الحلول:**
- استخدام Composition
- تطبيق SOLID principles
- تقليل عمق الوراثة
- استخدام Interfaces

### ما الفرق بين strongly typed وloosely typed في C#؟

**C# هي strongly typed language:**
- يجب تحديد نوع البيانات
- فحص الأنواع في وقت الترجمة
- لا يمكن تحويل الأنواع تلقائياً إلا في حالات محددة
- أمان أكبر وأخطاء أقل

```csharp
// Strongly typed
int number = 10;
string text = "Hello";
// number = text; // خطأ في وقت الترجمة

// استخدام dynamic للحصول على loose typing
dynamic value = 10;
value = "Hello"; // صالح
```

### ما ترتيب تنفيذ الكود عند وجود وراثة بين Parent وChild؟

**ترتيب التنفيذ:**

1. **عند إنشاء كائن Child:**
   - Static constructor للـ Parent (إن وجد)
   - Static constructor للـ Child (إن وجد)
   - Instance constructor للـ Parent
   - Instance constructor للـ Child

2. **عند استدعاء method:**
   - يبحث أولاً في Child class
   - إذا لم يجد، يبحث في Parent class
   - إذا كان virtual/override، يستدعى من Child

```csharp
public class Parent
{
    static Parent() { Console.WriteLine("Parent Static Constructor"); }
    public Parent() { Console.WriteLine("Parent Constructor"); }
    public virtual void Display() { Console.WriteLine("Parent Display"); }
}

public class Child : Parent
{
    static Child() { Console.WriteLine("Child Static Constructor"); }
    public Child() { Console.WriteLine("Child Constructor"); }
    public override void Display() { Console.WriteLine("Child Display"); }
}

// Output عند إنشاء Child:
// Parent Static Constructor
// Child Static Constructor  
// Parent Constructor
// Child Constructor
```

---
