# README.md

## دليل الأسئلة والأجوبة - .NET Interview questions

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

### 1. ما الفرق بين ASP.NET MVC و ASP.NET Core؟

**ASP.NET MVC:**

- جزء من .NET Framework
- يعمل فقط على Windows
- مرتبط بـ IIS
- أقل في الأداء

**ASP.NET Core:**

- مبني على .NET Core/.NET 5+
- متعدد المنصات (Windows, Linux, macOS)
- خفيف وسريع
- مفتوح المصدر
- يدعم Cloud-native applications
- Dependency Injection مدمج بشكل افتراضي

---

### 2. ما هو الـ Middleware وكيف أكتبه؟

**الـ Middleware** هو مكونات تشكل pipeline لمعالجة HTTP requests والاستجابة لها.

### كتابة Middleware مخصص:

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
        // معالجة قبل Request
        Console.WriteLine("Before request");

        await _next(context); // استدعاء الـ middleware التالي

        // معالجة بعد Response
        Console.WriteLine("After response");
    }
}

// في Program.cs
app.UseMiddleware<CustomMiddleware>();
```

---

## 3. ما الفرق بين Middleware و Filter؟

| Middleware                    | Filter                           |
| ----------------------------- | -------------------------------- |
| يعمل على مستوى Application    | يعمل على مستوى Controller/Action |
| يمكنه التعامل مع جميع الطلبات | يعمل فقط مع MVC requests         |
| ترتيب التنفيذ حسب الإضافة     | ترتيب محدد مسبقاً                |
| يمكنه قطع Pipeline            | لا يمكنه قطع Pipeline بالكامل    |

**أنواع Filters:**

- Authorization Filters
- Action Filters
- Result Filters
- Exception Filters

---

## 4. ما هو الـ Request Lifecycle في MVC؟

1. **HTTP Request** يصل للخادم
2. **Routing** يحدد Controller و Action
3. **Controller Instantiation** إنشاء مثيل من Controller
4. **Model Binding** ربط البيانات بالـ Model
5. **Action Execution** تنفيذ الـ Action
6. **Result Execution** تنفيذ النتيجة (View, JSON, etc.)
7. **Response** إرسال الاستجابة للعميل

---

## 5. ما هو الـ Routing وما علاقة ترتيب الـ Middleware؟

**الـ Routing** هو نظام توجيه الطلبات إلى Controllers و Actions المناسبة.

### أنواع Routing:

```csharp
// Convention-based Routing
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

// Attribute Routing
[Route("api/[controller]")]
[HttpGet("{id}")]
public ActionResult Get(int id) { }
```

### ترتيب Middleware مهم:

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.UseHttpsRedirection();    // 1
app.UseStaticFiles();         // 2
app.UseRouting();            // 3
app.UseAuthentication();     // 4
app.UseAuthorization();      // 5
app.MapControllers();        // 6
```

---

## 6. ما الفرق بين ViewBag و ViewData و TempData؟

| الخاصية   | ViewBag           | ViewData              | TempData              |
| --------- | ----------------- | --------------------- | --------------------- |
| النوع     | dynamic           | Dictionary            | Dictionary            |
| النطاق    | Controller → View | Controller → View     | Request → Request     |
| البقاء    | Request واحد      | Request واحد          | عدة Requests          |
| الاستخدام | `ViewBag.Message` | `ViewData["Message"]` | `TempData["Message"]` |

### مثال:

```csharp
// في Controller
ViewBag.Title = "الصفحة الرئيسية";
ViewData["Message"] = "مرحباً";
TempData["Success"] = "تم الحفظ بنجاح";

// في View
<h1>@ViewBag.Title</h1>
<p>@ViewData["Message"]</p>
<div>@TempData["Success"]</div>
```

---

## 7. ما الطرق المتاحة لنقل البيانات من View إلى Controller؟

1. **Model Binding**: ربط البيانات تلقائياً
2. **Form Data**: بيانات النماذج
3. **Query String**: معاملات URL
4. **Route Data**: بيانات المسار
5. **Request Body**: محتوى الطلب

### مثال:

```csharp
[HttpPost]
public ActionResult Create(UserModel model) // Model Binding
{
    string name = Request.Form["Name"];      // Form Data
    string id = Request.Query["id"];         // Query String
    return View();
}
```

---

## 8. ما هو الـ Ajax وكيف أستخدمه مع MVC؟

**AJAX** (Asynchronous JavaScript and XML) يسمح بإرسال طلبات غير متزامنة للخادم.

### مثال باستخدام jQuery:

```javascript
$.ajax({
  url: "/Home/GetData",
  type: "GET",
  dataType: "json",
  success: function (data) {
    console.log(data);
  },
  error: function () {
    alert("حدث خطأ");
  },
});
```

### في Controller:

```csharp
[HttpGet]
public JsonResult GetData()
{
    var data = new { Message = "البيانات", Count = 10 };
    return Json(data);
}
```

---

## 9. ما هو الـ Identity وما علاقته بالـ Token؟

**ASP.NET Identity** هو نظام إدارة المستخدمين والمصادقة.

### الميزات:

- إدارة المستخدمين
- المصادقة والتفويض
- إدارة الأدوار
- كلمات المرور
- المصادقة الخارجية

### مع JWT Token:

```csharp
[HttpPost("login")]
public async Task<IActionResult> Login(LoginModel model)
{
    var user = await _userManager.FindByEmailAsync(model.Email);
    if (user != null && await _userManager.CheckPasswordAsync(user, model.Password))
    {
        var token = GenerateJwtToken(user);
        return Ok(new { Token = token });
    }
    return Unauthorized();
}
```

---

## 10. ما هو الـ JWT Token ولماذا يُستخدم؟

**JWT (JSON Web Token)** هو معيار لنقل المعلومات بشكل آمن.

### المكونات:

1. **Header**: نوع التوكن والخوارزمية
2. **Payload**: البيانات (Claims)
3. **Signature**: التوقيع للتحقق

### المزايا:

- لا حاجة لحفظ Session
- يمكن التحقق منه محلياً
- مناسب للـ APIs
- يدعم Cross-domain

### إنشاء JWT:

```csharp
private string GenerateJwtToken(ApplicationUser user)
{
    var tokenHandler = new JwtSecurityTokenHandler();
    var key = Encoding.ASCII.GetBytes(_secretKey);
    var tokenDescriptor = new SecurityTokenDescriptor
    {
        Subject = new ClaimsIdentity(new[]
        {
            new Claim(ClaimTypes.Name, user.UserName),
            new Claim(ClaimTypes.Email, user.Email)
        }),
        Expires = DateTime.UtcNow.AddHours(1),
        SigningCredentials = new SigningCredentials(new SymmetricSecurityKey(key),
            SecurityAlgorithms.HmacSha256Signature)
    };
    var token = tokenHandler.CreateToken(tokenDescriptor);
    return tokenHandler.WriteToken(token);
}
```

---

## 11. ما الفرق بين Get، Post، Put، Delete في الـ API؟

| HTTP Verb  | الغرض            | الاستخدام     | Idempotent |
| ---------- | ---------------- | ------------- | ---------- |
| **GET**    | استرجاع البيانات | قراءة الموارد | نعم        |
| **POST**   | إنشاء جديد       | إضافة مورد    | لا         |
| **PUT**    | تحديث كامل       | تعديل المورد  | نعم        |
| **DELETE** | حذف              | إزالة المورد  | نعم        |

### مثال:

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet]
    public ActionResult<IEnumerable<User>> Get() { }

    [HttpGet("{id}")]
    public ActionResult<User> Get(int id) { }

    [HttpPost]
    public ActionResult<User> Post([FromBody] User user) { }

    [HttpPut("{id}")]
    public IActionResult Put(int id, [FromBody] User user) { }

    [HttpDelete("{id}")]
    public IActionResult Delete(int id) { }
}
```

---

## 12. ما هو الـ API ولماذا نستخدمه؟

**API (Application Programming Interface)** هو واجهة برمجية تسمح للتطبيقات بالتواصل.

### المزايا:

- فصل Frontend عن Backend
- إعادة الاستخدام
- المرونة في التطوير
- دعم منصات متعددة
- سهولة الصيانة

### أنواع APIs:

- **REST API**: الأكثر شيوعاً
- **GraphQL**: استعلامات مرنة
- **SOAP**: بروتوكول قديم
- **gRPC**: عالي الأداء

---

## 13. ما هو API Versioning؟

**API Versioning** هو إدارة إصدارات مختلفة من الـ API للحفاظ على التوافق.

### طرق Versioning:

#### 1. URL Path:

```csharp
[Route("api/v1/[controller]")]
[Route("api/v2/[controller]")]
```

#### 2. Query Parameter:

```csharp
[HttpGet]
[MapToApiVersion("1.0")]
public ActionResult GetV1() { }

[HttpGet]
[MapToApiVersion("2.0")]
public ActionResult GetV2() { }
```

#### 3. Header:

```csharp
// Request Header: X-Version: 1.0
services.AddApiVersioning(opt =>
{
    opt.ApiVersionReader = new HeaderApiVersionReader("X-Version");
});
```

---

## 14. ما الفرق بين In-memory Caching و Distributed Caching؟

| In-Memory Caching | Distributed Caching |
| ----------------- | ------------------- |
| داخل التطبيق      | خارج التطبيق        |
| سريع جداً         | أبطأ نسبياً         |
| مؤقت              | دائم نسبياً         |
| خادم واحد         | عدة خوادم           |

### In-Memory Caching:

```csharp
services.AddMemoryCache();

public class HomeController : Controller
{
    private readonly IMemoryCache _cache;

    public HomeController(IMemoryCache cache)
    {
        _cache = cache;
    }

    public IActionResult Index()
    {
        if (!_cache.TryGetValue("data", out string cachedData))
        {
            cachedData = GetDataFromDatabase();
            _cache.Set("data", cachedData, TimeSpan.FromMinutes(30));
        }
        return View(cachedData);
    }
}
```

### Distributed Caching (Redis):

```csharp
services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = "localhost:6379";
});

private readonly IDistributedCache _distributedCache;

public async Task<string> GetDataAsync()
{
    var cachedData = await _distributedCache.GetStringAsync("key");
    if (cachedData == null)
    {
        cachedData = GetDataFromDatabase();
        await _distributedCache.SetStringAsync("key", cachedData,
            new DistributedCacheEntryOptions
            {
                AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(30)
            });
    }
    return cachedData;
}
```

---

## خلاصة

هذه أهم المفاهيم في ASP.NET Core/MVC التي يجب على كل مطور معرفتها. التطبيق العملي والممارسة هما المفتاح لإتقان هذه التقنيات.

**نصائح مهمة:**

- استخدم Dependency Injection بشكل صحيح
- اهتم بـ Security والـ Authentication
- طبق مبادئ REST في APIs
- استخدم Caching لتحسين الأداء
- اتبع أفضل الممارسات في التطوير
