# ApiTracker.AspNetCore 

[![Build status](https://ci.appveyor.com/api/projects/status/o72ved788wpbabvk?svg=true)](https://ci.appveyor.com/project/seven1986/ApiTracker.AspNetCore)

PM> Install-Package ApiTracker.AspNetCore


### appsettings.json ����
```json
 "ApiTrackerSetting": {
    "ElasticConnection": "",
    "DocumentName": "",
    "TimeOut": 500
  }
```
```html
ElasticConnection: elastic��ַ������ http://localhost:9200
DocumentName:�ĵ����ƣ�Ĭ��apitracker
TimeOut:д�볬ʱʱ�䣬��λ���룬Ĭ��500
```


### Startup.cs ����

```csharp
// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
    // Add framework services.
    services.AddMvc();

    // ...����

    services.Configure<ApiTrackerSetting>(Configuration.GetSection("ApiTrackerSetting"));
    services.AddScoped<ApiTracker.ApiTracker>();
}
```


### API Controller ����

```csharp
    [Route("values")]
    [ServiceFilter(typeof(ApiTracker.ApiTracker),IsReusable = true)]
    public class ValuesController : Controller
    {
        // GET api/values
        [HttpGet]
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // POST api/values
        [HttpPost]
        [ApiTracker.ApiTrackerOptions(EnableClientIp =false)]
        public void Post([FromBody]JObject value)
        {

        }
    }
```

