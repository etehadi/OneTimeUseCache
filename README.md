# OneTimeUseCache
You can create in memory stored list of objects that each list item is available within a specific lifetime. 

Tutorial:
1. Create your class  

    public class MyOTUO : OneTimeUseCache.OneTimeUseObject
    {
        public override string Key { get; set; }
        public string SomeOtherValues { get; set; }        
    }
    
2. Set cache item lifetime:
    OTUCContext<MyOTUO>.LifeTime = new TimeSpan(0, 0, 3);
  
3.Add an instance of created class
            var key = Guid.NewGuid().ToString();
            var someOtherValues = DateTime.Now.ToString("O");
            var obj = new MyOTUO()
            {
                Key = key,
                SomeOtherValues = someOtherValues
            };
           OTUCContext<MyOTUO>.Current.Add(obj);
  
4.Get it from the cache by specified key whenever you need it. If you get it in it's lifetime you will get it, Otherwise you will get null value.
        var result = OTUCContext<MyOTUO>.Current.Get(key);
  
