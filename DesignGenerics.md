### Generic Repository(With specification pattern)
---

##### Advantages
- Generics been around since C# 2.0 from year 2022 
- help avoid duplicate code
- Type safety
- Describes a query in an object
- Returns an IQueryable<T>
- Specification can have meaningful name.

##### Disadvantages
- XYZ

###### Normal Repository 
```
//In repository class
public StoreContext(DbContextOptions<StoreContext> options) : base(options)
{}
public DbSet<Product> Products {get; set;}

---
//In program.cs

services.AdContext<StoreContext>(x=>x.UseSqlite(_config.GetConnectionString('****')));
builder.Services.AddScoped<IProductRepository, ProductRepository>();
---
//In Interface 
 public interface IProductRepository
    {
        Task<Product> GetProductByIdAsync(int id);
        Task<IReadOnlyList<Product>> GetProductsAsync();
        Task<IReadOnlyList<ProductBrand>> GetProductBrandAsync();
        Task<IReadOnlyList<ProductType>> GetProductTypeAsync();
    }

```
###### Using generic Repository
```
//BaseEntity 
 public class BaseEntity
    {
         public int Id { get; set; }
    }
//Generic Interface
public interface IGenericRepository<T> where T : BaseEntity
    {
        Task<T> GetByIdAsync(int Id);
        Task<IReadOnlyList<T>> ListAllAsync();
        Task<T> GetEntityWithSpec(ISpecifications<T> spec);
        Task<IReadOnlyList<T>> ListAsync(ISpecifications<T> spec); 
    }

//In program.cs
builder.Services.AddScoped(typeof(IGenericRepository<>),typeof(GenericRepository<>)); 
```

 Goto Project(Shopping cart application): [Generic Repository ](../FictionShoppingCart/core/Interfaces/IGenericRepository.cs)