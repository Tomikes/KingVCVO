# KingVCVO
dfdfd
kvc

- void changeName(Person *p, NSString *newName)
{
 
    // 获取值
    NSString *originalName = [p valueForKey:@"name"];
 
    // 赋值
    [p setValue:newName forKey:@"name"];

  //取对象的属性对象的属性值  该人的妻子的名字，当然他妻子也是个人，有名字
 NSString *spousesName = [p valueForKeyPath:@"spouse.name"];
 
}
－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－
kvo

- (void)viewDidLoad{
    [super viewDidLoad];

   [_SOMEOBJECT addObserver:self forKeyPath:@"hapyValue" options:NSKeyValueObservingOptionNew |NSKeyValueObservingOptionOld context:@"context"];
 
}
-(void) dealloc;
{
        [p removeObserver:self forKeyPath:@"hapyValue"];

}
//值改变了该怎么办

- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context{
  NSLog(@"%@",change);
  //通过打印change，我们可以看到对应的key
  //通过keyPath来判断不同属性的观察者
  if([keyPath isEqualToString:@"hapyValue"]){
    //这里change中有old和new的值是因为我们在调用addObserver方法时，用到了
    //NSKeyValueObservingOptionNew | NSKeyValueObservingOptionOld；想要哪一个就用哪一个
    //[change objectForKey:@"old"]是修改前的值
    NSNumber *hapyValue = [change objectForKey:@"new"];//修改之后的最新值
    NSInteger *value = [hapyValue integerValue];
    if(value < 90){
      //do something...
    }
}
－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－
